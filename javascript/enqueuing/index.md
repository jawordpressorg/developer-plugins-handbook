<!--
# Server Side PHP and Enqueuing
-->

# サーバーサイド PHP とエンキュー

<!--
There are two parts to the server side PHP script that are needed to implement AJAX communication. First we need to enqueue the jQuery script on the web page and localize any PHP values that the jQuery script needs. Second is the actual handling of the AJAX request.
-->

サーバーサイドの PHP スクリプトには、AJAX 通信を実装するために必要な2つの部分があります。一つは、jQuery スクリプトを Web ページ上でエンキューし、jQuery スクリプトが必要とする PHP の値をローカライズすることです。もう一つは、実際の AJAX リクエストの処理です。

<!--
## Enqueue Script
-->

## スクリプトのエンキュー

<!--
This section covers the two major quirks of AJAX in WordPress that trip up experienced coders new to WordPress. One is the need to enqueue scripts in order to get meta links to appear correctly in the page's head section. The other is that **all** AJAX requests need to be sent through `wp-admin/admin-ajax.php`. Never send requests directly to your plugin pages.
-->

このセクションでは、WordPress を初めて使用する経験豊富なコーダーがつまずく、WordPress における AJAX の2つの大きな癖について説明します。ひとつは、ページの head セクションにメタリンクを正しく表示するために、スクリプトをエンキューする必要があることです。もうひとつは、**すべての** AJAX リクエストは `wp-admin/admin-ajax.php` を通して送られる必要があるということです。プラグインのページに直接リクエストを送ってはいけません。

<!--
### Enqueue
-->

### エンキュー

<!--
Use the function [`wp_enqueue_script()`](https://developer.wordpress.org/reference/functions/wp_enqueue_script/) to get WordPress to insert a meta link to your script in the page's section. Never hardcode such links in the header template. As a plugin developer, you do not have ready access to the header template, but this rule bears mentioning anyway.
-->

[`wp_enqueue_script()`](https://developer.wordpress.org/reference/functions/wp_enqueue_script/) 関数を使って、WordPress にあなたのスクリプトへのメタリンクをページのセクションに挿入してもらいましょう。このようなリンクをヘッダーテンプレートにハードコードしないでください。プラグイン開発者として、あなたはヘッダーテンプレートにすぐにアクセスできませんが、このルールについては言及しておく価値があります。

<!--
The enqueue function accepts five parameters as follows:
-->

エンキュー関数は、以下の5つのパラメータを受け付けます:

<!--
- `$handle` is the name for the script.
- `$src` defines where the script is located. For portability, use `plugins_url()` to build the proper URL. If you are enqueuing the script for something besides a plugin, use some related function to create a proper URL – never hardcode it.
- `$deps` is an array that can handle any script that your new script depends on, such as jQuery. Since we are using jQuery to send an AJAX request, you will at least need to list `'jquery'` in the array.
- `$ver` lets you list a version number.
- `$args` an array of arguments that define footer printing (via an `in_footer` key) and script loading strategies (via a `strategy` key) such as `defer` or `async`. This replaces/overloads the `$in_footer` parameter as of WordPress version 6.3.
-->

- `$handle` は、スクリプトの名前です。
- `$src` は、スクリプトの場所を定義します。移植性のために、`plugins_url()` を使用して適切な URL を作成してください。プラグイン以外のスクリプトをエンキューする場合は、関連する関数を使用して適切な URL を作成してください – 決してハードコードしないでください。
- `$deps` は、配列で、新しいスクリプトが依存するスクリプト (jQuery など) を処理できます。jQuery を使用して AJAX リクエストを送信するので、少なくとも配列に `'jquery'` をリストアップする必要があります。
- `$ver` は、バージョン番号をリストアップします。
- `$args` は、(`in_footer` キーを介して) フッターの出力や、`defer` や `async` など (`strategy` キーを介して) スクリプトを読み込む方法を定義する引数の配列です。これは WordPress バージョン6.3のパラメータ `$in_footer` を置き換え/オーバーロードします。

```
wp_enqueue_script(
  'ajax-script',
  plugins_url( '/js/myjquery.js', __FILE__ ),
  array( 'jquery' ),
  '1.0.,0',
  array(
    'in_footer' => true,
  )
);
```

<!--
You cannot enqueue scripts directly from your plugin code page when it is loaded. Scripts must be enqueued from one of a few action hooks – which one depends on what sort of page the script needs to be linked to. For administration pages, use `admin_enqueue_scripts`. For front-end pages use `wp_enqueue_scripts`, except for the login page, in which case use `login_enqueue_scripts`.
-->

プラグインのコードページが読み込まれたときに、そこから直接スクリプトをエンキューできません。スクリプトは、いくつかのアクションフックのいずれかからエンキューする必要があります。どれを使うかは、スクリプトがどのようなページにリンクされる必要があるかによって決まります。管理ページには `admin_enqueue_scripts` を使います。ログインページを除き、フロントエンドのページでは `wp_enqueue_scripts` を使い、ログインページの場合は `login_enqueue_scripts` を使います。

<!--
The `admin_enqueue_scripts` hook passes the current page filename to your callback. Use this information to only enqueue your script on pages where it is needed. The front-end version does not pass anything. In that case, use template tags such as `is_home()`, `is_single()`, etc. to ensure that you only enqueue your script where it is needed. This is the complete enqueue code for our example:
-->

フック `admin_enqueue_scripts` は、現在のページのファイル名をコールバックに渡します。この情報を使って、スクリプトが必要なページでのみスクリプトをエンキューします。フロントエンド版は、何も渡しません。その場合は、`is_home()`、`is_single()` などのテンプレートタグを使い、スクリプトを必要な場所にだけエンキューします。これが今回の例の完全なエンキューコードです:

```
add_action( 'admin_enqueue_scripts', 'my_enqueue' );
function my_enqueue( $hook ) {
  if ( 'myplugin_settings.php' !== $hook ) {
    return;
  }
  wp_enqueue_script(
    'ajax-script',
    plugins_url( '/js/myjquery.js', __FILE__ ),
    array( 'jquery' ),
    '1.0.0',
    array(
      'in_footer' => true,
    )
  );
}
```

<!--
Why do we use a named function here but use anonymous functions with jQuery? Because closures are only recently supported by PHP. jQuery has supported them for quite some time. Since some people may still be running older versions of PHP, we always use named functions for maximum compatibility. If you have a recent PHP version and are developing only for your own installation, go ahead and use closures if you like.
-->

なぜここでは名前付き関数を使うのに、jQuery では匿名関数を使うのでしょうか ? クロージャが PHP でサポートされたのは最近のことだからです。jQuery ではかなり以前からサポートされていました。古いバージョンの PHP を使用している人もいるかもしれないので、互換性を最大化するために常に名前付き関数を使用しています。PHP のバージョンが最近のもので、自分のインストールのためだけに開発するのであれば、どうぞお好きな様にクロージャを使ってください。

<!--
#### Register vs. Enqueue
-->

#### 登録とエンキュー

<!--
You will see examples in other tutorials that religiously use [`wp_register_script()`](https://developer.wordpress.org/reference/functions/wp_register_script/). This is fine, but its use is optional. What is not optional is `wp_enqueue_script()`. This function must be called in order for your script file to be properly linked on the web page. So why register scripts? It creates a useful tag or handle with which you can easily reference the script in various parts of your code as needed. If you just need your script loaded and are not referencing it elsewhere in your code, there is no need to register it.
-->

他のチュートリアルでは、[`wp_register_script()`](https://developer.wordpress.org/reference/functions/wp_register_script/) を使用する例をよく見かけます。これは問題ありませんが、使用は任意です。任意ではないのは `wp_enqueue_script()` です。この関数は、スクリプトファイルが Web ページに正しくリンクされるために呼び出されなければなりません。では、なぜスクリプトを登録するのでしょうか ? スクリプトを登録すると、便利なタグやハンドルが作成され、必要に応じてコードのさまざまな部分でスクリプトを簡単に参照できる様になります。スクリプトを読み込むだけで、コード内の他の場所でスクリプトを参照しない場合は、スクリプトを登録する必要はありません。

<!--
#### Delayed Script Loading
-->

#### スクリプトの遅延読み込み

<!--
WordPress provides support for specifying a script loading strategy via the `wp_register_script()` and `wp_enqueue_script()` functions, by way of the `strategy` key within the new `$args` array parameter introduced in WordPress 6.3.
-->

WordPress は、WordPress 6.3で導入された新しい配列パラメータ `$args` 内のキー `strategy` によって、`wp_register_script()` 関数と `wp_enqueue_script()` 関数を介して、スクリプトを読み込む方法を指定するためのサポートを提供します。

<!--
Supported strategies are as follows:
-->

サポートされているオプションは、以下の通りです:

<!--
- **defer**
  - Added by specifying an array key value pair of `'strategy' => 'defer'` to the $args parameter.
  - Scripts marked for deferred execution — via the defer script attribute — are only executed once the DOM tree has fully loaded (but before the `DOMContentLoaded` and window load events). Deferred scripts are executed in the same order they were printed/added in the DOM, unlike asynchronous scripts.
- **async**
  - Added by specifying an array key value pair of `'strategy' => 'async'` to the `$args` parameter.
  - Scripts marked for asynchronous execution — via the `async` script attribute — are executed as soon as they are loaded by the browser. Asynchronous scripts do not have a guaranteed execution order, as script B (although added to the DOM after script A) may execute first given that it may complete loading prior to script A. Such scripts may execute either before the DOM has been fully constructed or after the `DOMContentLoaded` event.
-->

- **defer**
  - パラメータ `$args` に、`'strategy' => 'defer'` の配列キーと値のペアを指定して追加されます。
  - スクリプト属性 defer を介して遅延実行と指定されたスクリプトは、DOM ツリーが完全に読み込まれた後 (ただし `DOMContentLoaded` イベントやウィンドウロードイベントの前) に実行されます。遅延されたスクリプトは、非同期スクリプトとは異なり、DOM に出力/追加された順番に実行されます。
- **async**
  - パラメータ `$args` に、`'strategy' => 'async'` の配列キーと値のペアを指定することで追加されます。
  - スクリプト属性 `async` を介して非同期実行と指定されたスクリプトは、ブラウザに読み込まれるとすぐに実行されます。非同期スクリプトは実行順序が保証されていません。スクリプト B は (スクリプト A の後に DOM に追加されたが) スクリプト A よりも先に読み込みが完了する可能性があるため、最初に実行される可能性があります。このようなスクリプトは、DOM が完全に構築される前に実行されることもあれば、`DOMContentLoaded` イベントの後に実行されることもあります。

<!--
Following is an example of specifying a loading strategy for an additional script enqueue within our plugin:
-->

以下は、プラグイン内の追加スクリプト・エンキューの読み込み方法を指定する例です:

```
wp_register_script(
  'ajax-script-two',
  plugins_url( '/js/myscript.js', __FILE__ ),
  array( ajax-script ),
  '1.0.,0',
  array(
    'strategy' => 'defer',
  )
);
```

<!--
The same approach applies when using `wp_enqueue_script()`. In the example above, we indicate that we intend to load the `'ajax-script-two'` script in a deferred manner.
-->

`wp_enqueue_script()` を使う場合も、同じアプローチが適用されます。上の例では、遅延処理でスクリプト `'ajax-script-two'` を読み込むことを示しています。

<!--
When specifying a delayed script loading strategy, consideration of the script's dependency tree (its dependencies and/or dependents) is taken into account when deciding on an “eligible strategy” so as not to result in application of a strategy that is valid for one script but detrimental to others in the tree by causing an unintended out of order of execution. As a result of such logic, the intended loading strategy that you pass via the `$args` parameter may not be the final (chosen) strategy, but it will never be detrimental to (or stricter than) the intended strategy.
-->

遅延スクリプトを読み込む方法を指定する場合、スクリプトの依存関係ツリー (その依存関係および / または従属関係) を考慮することで、あるスクリプトには有効だが、ツリー内の他のスクリプトには有害な手順を適用して、意図しない実行順序のずれを引き起こさない様に、「適格な方法」を決定します。このようなロジックの結果、パラメータ `$args` を介して渡された意図した読み込み方法は、最終的な (選択された) 順序にはならないかもしれないが、意図した方法に対して不利になる (または意図した方法よりも厳しくなる) ことはありません。

### Nonce

<!--
You need to create a nonce so that the jQuery AJAX request can be validated as a legitimate request instead of a potentially nefarious request from some unknown bad actor. Only your PHP script and your jQuery script will know this value. When the request is received, you can verify it is the same value created here. This is how to create a nonce for our example:
-->

jQuery AJAX リクエストを検証できるように、nonce を作成する必要があります。そうすることで、jQuery の AJAX リクエストを、未知の悪意のあるリクエストではなく、正当なリクエストとして検証できる様になります。この値を知っているのは、PHP スクリプトと jQuery スクリプトだけです。リクエストを受け取ったときに、ここで作成したのと同じ値であることを検証できます。これは、nonce を作成する一つの方法です:

```
$title_nonce = wp_create_nonce( 'title_example' );
```

<!--
The parameter `title_example` can be any arbitrary string. It's suggested the string be related to what the nonce is used for, but it can really be anything that suits you.
-->

パラメータ `title_example` には、任意の文字列を指定できます。この文字列は nonce が何に使われるかに関連したものであることが推奨されるが、何でもかまいません。

<!--
### Localize
-->

### ローカライズ

<!--
If you recall from the [jQuery Section](https://developer.wordpress.org/plugins/javascript/jquery/), data created by PHP for use by jQuery was passed in a global object named `my_ajax_obj`. In our example, this data was a nonce and the complete URL to `admin-ajax.php`. The process of assigning object properties and creating the global jQuery object is called **localizing**. This is the localizing code used in our example which uses [`wp_localize_script()`](https://developer.wordpress.org/reference/functions/wp_localize_script/).
-->

[jQuery セクション](https://ja.wordpress.org/team/handbook/plugin-development/javascript/jquery/)を思い起こせば、jQuery で使用するために PHP が作成したデータは、`my_ajax_obj` という名前のグローバルオブジェクトで渡されました。私たちの例では、このデータは nonce と `admin-ajax.php` への完全な URL でした。オブジェクトのプロパティを割り当て、グローバルな jQuery オブジェクトを作成するプロセスを「ローカライズ」と呼びます。これは、[`wp_localize_script()`](https://developer.wordpress.org/reference/functions/wp_localize_script/) を使用した例で使用したローカライズのコードです。

```
wp_localize_script(
  'ajax-script',
  'my_ajax_obj',
  array(
    'ajax_url' => admin_url( 'admin-ajax.php' ),
    'nonce'    => $title_nonce,
  )
);
```

<!--
Note how our script handle `ajax-script` is used so that the global object is assigned to the right script. The object is global to our script, not to all scripts. Localization can also be called from the same hook that is used to enqueue scripts. The same goes for creating a nonce, though that particular function can be called virtually anywhere. All of that combined together in a single hook callback looks like this:
-->

スクリプトハンドル `ajax-script` がどのように使用され、グローバルオブジェクトが正しいスクリプトに割り当てられるかに注意してください。このオブジェクトは、すべてのスクリプトに対してではなく、私たちのスクリプトに対してグローバルです。ローカライズは、スクリプトをエンキューするのと同じフックから呼び出すこともできます。nonce の作成も同様ですが、この特定の関数は事実上どこでも呼び出すことができます。これらすべてを1つのフック・コールバックにまとめると、次のようになります:

```
add_action( 'admin_enqueue_scripts', 'my_enqueue' );

/**
 * Enqueue my scripts and assets.
 *
 * @param $hook
 */
function my_enqueue( $hook ) {
  if ( 'myplugin_settings.php' !== $hook ) {
    return;
  }
  wp_enqueue_script(
    'ajax-script',
    plugins_url( '/js/myjquery.js', __FILE__ ),
    array( 'jquery' ),
    '1.0.0',
    true
  );

  wp_localize_script(
    'ajax-script',
    'my_ajax_obj',
    array(
      'ajax_url' => admin_url( 'admin-ajax.php' ),
      'nonce'    => wp_create_nonce( 'title_example' ),
    )
  );
}
```

<!--
[info]Remember to only add this nonce localization to the needed pages, do not display a nonce to someone who should not use it. And remember to use `current_user_can()` with a capability or role to complete the security.[/info]
-->

[info]この nonce のローカライズは必要なページにのみ追加し、nonce を使うべきでない人には表示しないでください。また、セキュリティを完全にするために、権限や権限グループと一緒に `current_user_can()` を使用することを忘れないでください。[/info]

<!--
## AJAX Action
-->

## AJAX アクション

<!--
The other major part of the server side PHP code is the actual AJAX handler that receives the POSTed data, does something with it, then sends an appropriate response back to the browser. This takes on the form of a WordPress [action hook](https://developer.wordpress.org/plugins/hooks/actions/). Which hook tag you use depends on whether the user is logged in or not and what value your jQuery script passed as the _action:_ value.
-->

サーバーサイドの PHP コードのもう一つの主要な部分は、POST されたデータを受け取り、それを使って何かを行い、適切なレスポンスをブラウザに送り返す実際の AJAX ハンドラです。これは WordPress の[アクションフック](https://ja.wordpress.org/team/handbook/plugin-development/hooks/actions/)の形を採ります。どのフックタグを使うかは、ユーザーがログインしているかどうか、そして jQuery スクリプトが _action:_ の値としてどのような値を渡したかによって決まります。

<!--
[info]`$_GET`, `$_POST`, and `$_COOKIE` vs. `$_REQUEST`
-->

[info]`$_GET`、`$_POST`、`$_COOKIE` vs. `$_REQUEST`

<!--
You've probably used one or more of the PHP super globals such as `$_GET` or `$_POST` to retrieve values from forms or cookies (using `$_COOKIE`). Maybe you prefer `$_REQUEST` instead, or at least have seen it used. It's kind of cool – regardless of the request method, `POST` or `GET`, it will have the form values. Works great for pages that use both methods. On top of that, it has cookie values as well. One stop shopping! Therein lies its tragic flaw. In the case of a name conflict, the cookie value will override any form values. Thus it is ridiculously easy for a bad actor to craft a counterfeit cookie on their browser, which will overwrite any form value you might be expecting from the request. `$_REQUEST` is an easy route for hackers to inject arbitrary data into your form values. To be extra safe, stick to the specific variables and avoid the one size fits all.[/info]
-->

`$_GET` や `$_POST` のような PHP のスーパーグローバルを使って、フォームや (`$_COOKIE` を使って) Cookie から値を取得したことがあるでしょう。もしかすると、代わりに `$_REQUEST` を使用することを好むかもしれませんし、少なくとも使用されているのを見たことがあるかもしれません。ちょっと格好よく – リクエストメソッド (`POST` または `GET`) に関係なく、フォームの値を取得できます。両方のメソッドを使用するページには最適です。その上、Cookie の値も取得できます。非常に便利ですが、そこに悲劇的な欠点があります。名前が衝突した場合、Cookie の値がフォームの値を上書きします。従って、悪意ある誰かがブラウザ上で偽造 Cookie を作成するのはとんでもなく簡単で、リクエストから期待されるかもしれないフォームの値を上書きしてしまいます。`$_REQUEST` は、ハッカーにとって フォームの値に任意のデータを注入する簡単なルートです。安全性を高めるために、特定の変数に固執し、1つの方法ですべてを満たすことは避けてください。[/info]

<!--
Since our AJAX exchange is for the plugin's settings page, the user must be logged in. If you recall from the [jQuery section](https://developer.wordpress.org/plugins/javascript/jquery/), the `action:` value is `"my_tag_count"`. This means our action hook tag will be `wp_ajax_my_tag_count`. If our AJAX exchange were to be utilized by users who were not currently logged in, the action hook tag would be `wp_ajax_nopriv_my_tag_count` The basic code used to hook the action looks like this:
-->

AJAX 交換はプラグインの設定ページに対して行われるので、ユーザーはログインしている必要があります。[jQuery セクション](https://ja.wordpress.org/team/handbook/plugin-development/javascript/jquery/)を思い起こしてほしいのですが、`action:` の値は `"my_tag_count"` です。つまり、アクションフックタグは `wp_ajax_my_tag_count` になることを意味します。AJAX 交換が現在のログインしていないユーザーによって利用される場合、アクションフックタグは `wp_ajax_nopriv_my_tag_count` となります。アクションをフックするための基本的なコードは次のようになります:

```
add_action( 'wp_ajax_my_tag_count', 'my_ajax_handler' );

/**
 * Handles my AJAX request.
 */
function my_ajax_handler() {
  // Handle the ajax request here

  wp_die(); // All ajax handlers die when finished
}
```

<!--
The first thing your AJAX handler should do is verify the nonce sent by jQuery with [`check_ajax_referer()`](https://developer.wordpress.org/reference/functions/check_ajax_referer/), which should be the same value that was localized when the script was enqueued.
-->

AJAX ハンドラが最初に行うべきことは、jQuery が送信した nonce を[`check_ajax_referer()`](https://developer.wordpress.org/reference/functions/check_ajax_referer/)で確認することで、スクリプトがエンキューされたときにローカライズされた値と同じでなければなりません。

```
check_ajax_referer( 'title_example' );
```

<!--
The provided parameter must be identical to the parameter provided [earlier](https://developer.wordpress.org/plugins/javascript/enqueuing/#php-nonce) to `wp_create_nonce()`. The function simply dies if the nonce does not check out. If this were a true nonce, now that it was used, the value is no longer any good. You would then generate a new one and send it to the callback script so that it can be used for the next request. But since WordPress nonces are good for twenty-four hours, you needn't do anything but check it.
-->

提供されるパラメータは、`wp_create_nonce()` に [以前に](https://ja.wordpress.org/team/handbook/plugin-development/javascript/enqueuing/#php-nonce)提供されたパラメータと同じでなければなりません。nonce がチェックアウトされない場合、この関数は単に強制終了します。これが真の nonce であった場合、それが使用されたので、その値はもはや無意味です。新しい nonce を生成してコールバックスクリプトに送り、次のリクエストで使えるようにします。しかし、WordPress の nonce は24時間有効ですので、それをチェックする以外には何もする必要はありません。

<!--
### Data
-->

### データ

<!--
With the nonce out of the way, our handler can deal with the data sent by the jQuery script contained in `$_POST['title']`. First we assign the value to a new variable, after running it through [`wp_unslash()`](https://developer.wordpress.org/reference/functions/wp_unslash/) to remove any unexpected quotes.
-->

nonce を避けて、ハンドラは、`$_POST['title']` に含まれる jQuery スクリプトによって送信されたデータを処理できます。まず、値を新しい変数に代入し、[`wp_unslash()`](https://developer.wordpress.org/reference/functions/wp_unslash/) を通して予期しない引用符を削除します。

```
$title = wp_unslash( $_POST['title'] );
```

<!--
We can save the user's selection in user meta by using [`update_user_meta()`](https://developer.wordpress.org/reference/functions/update_user_meta/).
-->

ユーザーが選択した内容は、[`update_user_meta()`](https://developer.wordpress.org/reference/functions/update_user_meta/) を使ってユーザーメタに保存できます。

```
update_user_meta( get_current_user_id(), 'title_preference', sanitize_post_title( $title ) );
```

<!--
Then we build a query in order to get the post count for the selected title tag.
-->

次に、選択したタイトルタグの投稿数を取得するためのクエリーを作成します。

```
$args      = array(
  'tag' => $title,
);
$the_query = new WP_Query( $args );
```

<!--
Finally we can send the response back to the jQuery script. There's several ways to transmit data. Let's look at some of the options before we deal with the specifics of our example.
-->

最後に、レスポンスを jQuery スクリプトに送り返します。データを送信するにはいくつかの方法があります。この例の詳細を説明する前に、いくつかのオプションを見てみましょう。

#### XML

<!--
PHP support for XML leaves something to be desired. Fortunately, WordPress provides the [`WP_Ajax_Response`](https://developer.wordpress.org/reference/classes/wp_ajax_response/) class to make the task easier. The [`WP_Ajax_Response`](https://developer.wordpress.org/reference/classes/wp_ajax_response/) class will generate an XML-formatted response, set the correct content type for the header, output the response xml, then die — ensuring a proper XML response.
-->

PHP による XML のサポートには改善の余地があります。幸いなことに、WordPress は [`WP_Ajax_Response`](https://developer.wordpress.org/reference/classes/wp_ajax_response/) クラスを提供しており、このタスクを簡単に行うことができます。[`WP_Ajax_Response`](https://developer.wordpress.org/reference/classes/wp_ajax_response/) クラスは、XML フォーマットのレスポンスを生成し、ヘッダーに正しいコンテンツタイプを設定し、レスポンス xml を出力して終了し — 適切な XML レスポンスを保証します。

#### JSON

<!--
This format is lightweight and easy to use, and WordPress provides the [`wp_send_json`](https://developer.wordpress.org/reference/functions/wp_send_json/) function to json-encode your response, print it, and die — effectively replacing [`WP_Ajax_Response`](https://developer.wordpress.org/reference/classes/wp_ajax_response/). WordPress also provides the [`wp_send_json_success`](https://developer.wordpress.org/reference/functions/wp_send_json_success/) and [`wp_send_json_error`](https://developer.wordpress.org/reference/functions/wp_send_json_error/) functions, which allow the appropriate done() or fail() callbacks to fire in JS.
-->

このフォーマットは軽量で使いやすく、WordPress はレスポンスを json エンコードして表示し、終了し - 効果的に [`WP_Ajax_Response`](https://developer.wordpress.org/reference/classes/wp_ajax_response/) を置き換えることができる [`wp_send_json`](https://developer.wordpress.org/reference/functions/wp_send_json/) 関数を提供しています。WordPress はまた、[`wp_send_json_success`](https://developer.wordpress.org/reference/functions/wp_send_json_success/) 関数と [`wp_send_json_error`](https://developer.wordpress.org/reference/functions/wp_send_json_error/) 関数を提供し、適切な done() または fail() コールバックを JS で発生させることができます。

<!--
#### Other
-->

#### その他

<!--
You can transfer data any way you like, as long as the sender and receiver are coordinated. Text formats like comma delimited or tab delimited are one of many possibilities. For small amounts of data, sending the raw stream may be adequate. That is what we will do with our example – we will send the actual replacement HTML, nothing else.
-->

送出側と受信側が協調している限り、どのような方法でもデータを転送できます。カンマ区切りやタブ区切りのようなテキストフォーマットは、多くの選択肢の一つです。少量のデータであれば、生のストリームを送信すれば十分かもしれません。この例ではそうします – 実際の置き換え HTML を送るだけで、他には何もしません。

```
echo esc_html( $title ) . ' (' . $the_query->post_count . ') ';
```

<!--
In a real world application, you must account for the possibility that the action could fail for some reason–for instance, maybe the database server is down. The response should allow for this contingency, and the jQuery script receiving the response should act accordingly, perhaps telling the user to try again later.
-->

実際のアプリケーションでは、何らかの理由でアクションが失敗する可能性、たとえば、データベースサーバーがダウンしている場合など、を考慮しなければなりません。レスポンスは、この不測の事態を許容するものでなければならず、そして、レスポンスを受け取った jQuery スクリプトは、それに応じて動作する必要があり、おそらく、後で再試行するようにユーザーに伝えることでしょう。

<!--
### Die
-->

### 終了

<!--
When the handler has finished all of its tasks, it needs to die. If you are using the [`WP_Ajax_Response`](https://developer.wordpress.org/reference/classes/wp_ajax_response/) or `wp_send_json*` functions, this is automatically handled for you. If not, simply use the WordPress [`wp_die()`](https://developer.wordpress.org/reference/functions/wp_die/) function.
-->

ハンドラがすべてのタスクを終了したら、終了する必要があります。[`WP_Ajax_Response`](https://developer.wordpress.org/reference/classes/wp_ajax_response/) または `wp_send_json*` 関数を使用している場合、これは自動的に処理されます。そうでない場合は、WordPress の [`wp_die()`](https://developer.wordpress.org/reference/functions/wp_die/) 関数を使用するだけです。

<!--
### AJAX Handler Summary
-->

### AJAX ハンドラの概要

<!--
The complete AJAX handler for our example looks like this:
-->

この例の完全な AJAX ハンドラは、次のようになります:

```
/**
 * AJAX handler using JSON
 */
function my_ajax_handler__json() {
  check_ajax_referer( 'title_example' );
  $title = wp_unslash( $_POST['title'] );

  update_user_meta( get_current_user_id(), 'title_preference', sanitize_post_title( $title ) );

  $args      = array(
    'tag' => $title,
  );
  $the_query = new WP_Query( $args );
  wp_send_json( esc_html( $title ) . ' (' . $the_query->post_count . ') ' );
}

/**
 * AJAX handler not using JSON.
 */
function my_ajax_handler() {
  check_ajax_referer( 'title_example' );
  $title = wp_unslash( $_POST['title'] );

  update_user_meta( get_current_user_id(), 'title_preference', sanitize_post_title( $title ) );

  $args      = array(
    'tag' => $title,
  );
  $the_query = new WP_Query( $args );
  echo esc_html( $title ) . ' (' . $the_query->post_count . ') ';
  wp_die(); // All ajax handlers should die when finished
}
```
