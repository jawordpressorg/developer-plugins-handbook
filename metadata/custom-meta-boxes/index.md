<!-- 
# Custom Meta Boxes
 -->
# カスタム・メタボックス

<!-- 
## What is a Meta Box?
 -->
## メタボックスとは ?

<!-- 
When a user edits a post, the edit screen is composed of several default boxes: Editor, Publish, Categories, Tags, etc. These boxes are meta boxes. Plugins can add custom meta boxes to an edit screen of any post type.
 -->
ユーザーが投稿を編集する際、編集画面はいくつかのデフォルトボックスで構成されます: Editor、Publish、Categories、Tags、等です。これらのボックスはメタボックスです。プラグインは、任意の投稿タイプの編集画面にカスタムメタボックスを追加できます。

<!-- 
The content of custom meta boxes are usually HTML form elements where the user enters data related to a Plugin's purpose, but the content can be practically any HTML you desire.
 -->
カスタム・メタボックスの内容は、通常、プラグインの目的に関連したデータをユーザーが入力する HTML フォーム要素ですが、実質的にはどんな HTML でもかまいません。

<!-- 
## Why Use Meta Boxes?
 -->
## なぜメタボックスを使うの ?

<!-- 
Meta boxes are handy, flexible, modular edit screen elements that can be used to collect information related to the post being edited. Your custom meta box will be on the same screen as all the other post related information; so a clear relationship is established.
 -->
メタボックスは、編集中の投稿に関連する情報を収集するために使用できる、便利で柔軟なモジュール式の編集画面要素です。カスタム・メタボックスは、他のすべての投稿関連情報と同じ画面に表示されるため、明確な関係が確立されます。

<!-- 
Meta boxes are easily hidden from users that do not need to see them, and displayed to those that do. Meta boxes can be user-arranged on the edit screen. The users are free to arrange the edit screen in a way that suits them, giving users control over their editing environment.
 -->
メタボックスは、見る必要のないユーザーには簡単に非表示にでき、見る必要のあるユーザーには表示されます。メタボックスは編集画面上でユーザーが配置できます。ユーザーは自分に合った方法で編集画面を自由に配置でき、編集環境をコントロールできます。

<!-- 
[alert]All examples on this page are for illustration purposes only. The code is not suitable for production environments.
 -->
[alert]このページに掲載されている例はすべて、説明のためのものです。コードは本番環境には適していません。

<!-- 
Operations such as [securing input](https://developer.wordpress.org/apis/security/sanitizing/), [user capabilities](https://developer.wordpress.org/plugins/security/checking-user-capabilities/), [nonces](https://developer.wordpress.org/apis/security/nonces/), and [internationalization](https://developer.wordpress.org/plugins/internationalization/) have been intentionally omitted. Be sure to always address these important operations.[/alert]
 -->
[入力の安全確保](https://developer.wordpress.org/apis/security/sanitizing/)、[ユーザー権限](https://developer.wordpress.org/plugins/security/checking-user-capabilities/)、[nonce](https://developer.wordpress.org/apis/security/nonces/)、[国際化](https://developer.wordpress.org/plugins/internationalization/)などの操作は、意図的に省略されています。これらの重要な操作には必ず対処してください。[/alert]

<!-- 
## Adding Meta Boxes
 -->
## メタボックスの追加

<!-- 
To create a meta box use the [`add_meta_box()`](https://developer.wordpress.org/reference/functions/add_meta_box/) function and plug its execution to the [`add_meta_boxes`](https://developer.wordpress.org/reference/hooks/add_meta_boxes/) action hook.
 -->
メタボックスを作成するには、[`add_meta_box()`](https://developer.wordpress.org/reference/functions/add_meta_box/) 関数を使用し、その実行を [`add_meta_boxes`](https://developer.wordpress.org/reference/hooks/add_meta_boxes/) アクションフックに接続します。

<!-- 
The following example is adding a meta box to the `post` edit screen and the `wporg_cpt` edit screen.
 -->
次の例は、`post` 編集画面と `wporg_cpt` 編集画面にメタボックスを追加するものです。

```
function wporg_add_custom_box() {
  $screens = [ 'post', 'wporg_cpt' ];
  foreach ( $screens as $screen ) {
    add_meta_box(
      'wporg_box_id',                 // Unique ID
      'Custom Meta Box Title',      // Box title
      'wporg_custom_box_html',  // Content callback, must be of type callable
      $screen                            // Post type
    );
  }
}
add_action( 'add_meta_boxes', 'wporg_add_custom_box' );
```

<!-- 
The `wporg_custom_box_html` function will hold the HTML for the meta box.
 -->
`wporg_custom_box_html` 関数は、メタボックス用の HTML を保持します。

<!-- 
The following example is adding form elements, labels, and other HTML elements.
 -->
次の例では、フォーム要素、ラベル、その他の HTML 要素を追加しています。

```
function wporg_custom_box_html( $post ) {
  ?>
  <label for="wporg_field">Description for this field</label>
  <select name="wporg_field" id="wporg_field" class="postbox">
    <option value="">Select something...</option>
    <option value="something">Something</option>
    <option value="else">Else</option>
  </select>
  <?php
}
```

<!-- 
[info]**Note there are no submit buttons in meta boxes.** The meta box HTML is included inside the edit screen's form tags, all the post data including meta box values are transfered via `POST` when the user clicks on the Publish or Update buttons.[/info]
 -->
[info]**メタボックスには、送信ボタンがないことに注意してください。** メタボックスの HTML は編集画面のフォームタグの中に含まれ、ユーザーが公開または更新ボタンをクリックすると、メタボックスの値を含むすべての投稿データが `POST` 経由で転送されます。[/info]

<!-- 
The example shown here only contains one form field, a drop down list. You may create as many as needed in any particular meta box. If you have a lot of fields to display, consider using multiple meta boxes, grouping similar fields together in each meta box. This helps keep the page more organized and visually appealing.
 -->
ここに示した例には、1つのフォームフィールド、1つのドロップダウンリストしかありません。メタボックスには必要な数だけフィールドを作成できます。大量の表示フィールドがある場合は、複数のメタボックスを使用し、各メタボックスで類似のフィールドをグループ化することを検討してください。ページはより整理され、より視覚的にアピールできます。

<!-- 
### Getting Values
 -->
### 値の取得

<!-- 
To retrieve saved user data and make use of it, you need to get it from wherever you saved it initially. If it was stored in the `postmeta` table, you may get the data with [`get_post_meta()`](https://developer.wordpress.org/reference/functions/get_post_meta/).
 -->
保存したユーザーデータを取得して利用するには、最初に保存した場所から取得する必要があります。`postmeta` テーブルに保存されている場合は、[`get_post_meta()`](https://developer.wordpress.org/reference/functions/get_post_meta/) でデータを取得できます。

<!-- 
The following example enhances the previous form elements with pre-populated data based on saved meta box values. You will learn how to save meta box values in the next section.
 -->
次の例では、保存されたメタ・ボックスの値にもとづいてあらかじめ入力されたデータで、以前のフォーム要素を拡張しています。メタボックスの値を保存する方法については、次のセクションで説明します。

```
function wporg_custom_box_html( $post ) {
  $value = get_post_meta( $post->ID, '_wporg_meta_key', true );
  ?>
  <label for="wporg_field">Description for this field</label>
    <select name="wporg_field" id="wporg_field" class="postbox">
      <option value="">Select something...</option>
      <option value="something" <?php selected( $value, 'something' ); ?>>Something</option>
      <option value="else" <?php selected( $value, 'else' ); ?>>Else</option>
    </select>
    <?php
}
```

<!-- 
More on the [`selected()`](https://developer.wordpress.org/reference/functions/selected/) function.
 -->
[`selected()`](https://developer.wordpress.org/reference/functions/selected/) 関数について。

<!-- 
### Saving Values
 -->
### 値の保存

<!-- 
When a post type is saved or updated, several actions fire, any of which might be appropriate to hook into in order to save the entered values. In this example we use the `save_post` action hook but other hooks may be more appropriate for certain situations. Be aware that `save_post` may fire more than once for a single update event. Structure your approach to saving data accordingly.
 -->
投稿タイプが保存または更新されると、いくつかのアクションが発生します。入力された値を保存するには、そのどれかにフックするのが適切でしょう。この例では `save_post` アクションフックを使用していますが、状況によっては他のフックの方が適切かもしれません。一つの更新イベントに対して複数回 `save_post` が発生する可能性があることに注意してください。こうした条件を念頭に、データを保存する方法を構築してください。

<!-- 
You may save the entered data anywhere you want, even outside WordPress. Since you are probably dealing with data related to the post, the `postmeta` table is often a good place to store data.
 -->
入力されたデータは、WordPress の外であっても、好きな場所に保存できます。おそらく投稿に関連するデータを扱うので、`postmeta` テーブルはデータを格納するのに都合の良い場所になることが多いです。

<!-- 
The following example will save the `wporg_field` field value in the `_wporg_meta_key` meta key, which is hidden.
 -->
次の例は、`wporg_field` フィールドの値を、非表示の `_wporg_meta_key` メタ・キーに保存します。

```
function wporg_save_postdata( $post_id ) {
  if ( array_key_exists( 'wporg_field', $_POST ) ) {
    update_post_meta(
      $post_id,
      '_wporg_meta_key',
      $_POST['wporg_field']
    );
  }
}
add_action( 'save_post', 'wporg_save_postdata' );
```

<!-- 
In production code, remember to follow the security measures outlined in the info box!
 -->
実運用コードでは、情報ボックスに概説されているセキュリティ対策に従うことを忘れないでください !

<!-- 
## Behind the Scenes
 -->
## 舞台裏

<!-- 
You don't normally need to be concerned about what happens behind the scenes. This section was added for completeness.
 -->
通常、舞台裏で何が起こっているのかを気にする必要はありません。このセクションは完全を期すために追加されました。

<!-- 
When a post edit screen wants to display all the meta boxes that were added to it, it calls the [`do_meta_boxes()`](https://developer.wordpress.org/reference/functions/do_meta_boxes/) function. This function loops through all meta boxes and invokes the `callback` associated with each.
 -->
投稿編集画面が、追加されたすべてのメタボックスを表示したい場合、[`do_meta_boxes()`](https://developer.wordpress.org/reference/functions/do_meta_boxes/) 関数を呼び出します。この関数はすべてのメタボックスをループし、それぞれに関連付けられた `callback` を呼び出します。

<!-- 
In between each call, intervening markup (such as divs, titles, etc.) is added.
 -->
それぞれの呼び出しの間に、(div やタイトルなどの) 付随するマークアップが追加されます。

<!-- 
## Removing Meta Boxes
 -->
## メタボックスの削除

<!-- 
To remove an existing meta box from an edit screen use the [`remove_meta_box()`](https://developer.wordpress.org/reference/functions/remove_meta_box/) function. The passed parameters must exactly match those used to add the meta box with [`add_meta_box()`](https://developer.wordpress.org/reference/functions/add_meta_box/).
 -->
編集画面から既存のメタボックスを削除するには、[`remove_meta_box()`](https://developer.wordpress.org/reference/functions/remove_meta_box/) 関数を使用します。渡されるパラメータは、[`add_meta_box()`](https://developer.wordpress.org/reference/functions/add_meta_box/) でメタボックスを追加する際に使用したパラメータと完全に一致しなければなりません。

<!-- 
To remove default meta boxes check the source code for the parameters used. The default [`add_meta_box()`](https://developer.wordpress.org/reference/functions/add_meta_box/) calls are made from `wp-includes/edit-form-advanced.php`.
 -->
デフォルトのメタボックスを削除するには、使用されているパラメータのソースコードを確認してください。デフォルトの [`add_meta_box()`](https://developer.wordpress.org/reference/functions/add_meta_box/) 呼び出しは、`wp-includes/edit-form-advanced.php` から行われます。

<!-- 
## Implementation Variants
 -->
## 実装のバリエーション

<!-- 
So far we've been using the procedural technique of implementing meta boxes. Many plugin developers find the need to implement meta boxes using various other techniques.
 -->
これまで、メタボックスの実装には手続き的なテクニックを使ってきました。多くのプラグイン開発者は、他のさまざまなテクニックを使ってメタボックスを実装する必要性を感じています。

<!-- 
### OOP
 -->
### OOP (オブジェクト指向プログラミング)

<!-- 
Adding meta boxes using OOP is easy and saves you from having to worry about naming collisions in the global namespace.
 -->
OOP (オブジェクト指向プログラミング) を使ったメタボックスの追加は簡単で、グローバル名前空間での名前の衝突を心配する必要もありません。

<!-- 
To save memory and allow easier implementation, the following example uses an abstract Class with static methods.
 -->
メモリを節約し、実装を容易にするために、以下の例では静的メソッドを持つ抽象クラスを使用しています。

```
abstract class WPOrg_Meta_Box {

  /**
   * Set up and add the meta box.
   */
  public static function add() {
    $screens = [ 'post', 'wporg_cpt' ];
    foreach ( $screens as $screen ) {
      add_meta_box(
        'wporg_box_id',          // Unique ID
        'Custom Meta Box Title', // Box title
        [ self::class, 'html' ],   // Content callback, must be of type callable
        $screen                  // Post type
      );
    }
  }

  /**
   * Save the meta box selections.
   *
   * @param int $post_id  The post ID.
   */
  public static function save( int $post_id ) {
    if ( array_key_exists( 'wporg_field', $_POST ) ) {
      update_post_meta(
        $post_id,
        '_wporg_meta_key',
        $_POST['wporg_field']
      );
    }
  }

  /**
   * Display the meta box HTML to the user.
   *
   * @param WP_Post $post   Post object.
   */
  public static function html( $post ) {
    $value = get_post_meta( $post->ID, '_wporg_meta_key', true );
    ?>
    <label for="wporg_field">Description for this field</label>
    <select name="wporg_field" id="wporg_field" class="postbox">
      <option value="">Select something...</option>
      <option value="something" <?php selected( $value, 'something' ); ?>>Something</option>
      <option value="else" <?php selected( $value, 'else' ); ?>>Else</option>
    </select>
    <?php
  }
}

add_action( 'add_meta_boxes', [ 'WPOrg_Meta_Box', 'add' ] );
add_action( 'save_post', [ 'WPOrg_Meta_Box', 'save' ] );
```

<!-- 
### AJAX
 -->
### AJAX (非同期の JavaScript と XML)

<!-- 
Since the HTML elements of the meta box are inside the `form` tags of the edit screen, the default behavior is to parse meta box values from the `$_POST` super global _after the user have submitted the page_.
 -->
メタボックスの HTML 要素は編集画面の `form` タグの中にあるので、デフォルトの挙動としては、_ユーザーがページを投稿した後_ に、`$_POST` スーパーグローバルからメタボックスの値をパース (解析) します。

<!-- 
You can enhance the default experience with AJAX; this allows to perform actions based on user input and behavior; regardless if they've submitted the page.
 -->
AJAX を使ってデフォルトの体験を向上させることができます。これにより、(ユーザーがページを送信したかどうかに関係なく) ユーザーの入力と行動にもとづいてアクションを起こすことができます。

<!-- 
#### Define a Trigger
 -->
#### トリガーの定義

<!-- 
First, you must define the trigger, this can be a link click, a change of a value or any other JavaScript event.
 -->
まず、トリガーを定義する必要があります。これは、リンクのクリック、値の変更、または他の JavaScript イベントでもかまいません。

<!-- 
In the example below we will define `change` as our trigger for performing an AJAX request.
 -->
以下の例では、AJAX リクエストを実行するトリガーとして `change` を定義します。

```
/*jslint browser: true, plusplus: true */
(function ($, window, document) {
  'use strict';
  // execute when the DOM is ready
  $(document).ready(function () {
    // js 'change' event triggered on the wporg_field form field
    $('#wporg_field').on('change', function () {
      // our code
    });
  });
}(jQuery, window, document));
```
<!-- 
#### Client Side Code
 -->
#### クライアントサイドのコード

<!-- 
Next, we need to define what we want the trigger to do, in other words we need to write our client side code.
 -->
次に、トリガーに何をさせたいかを定義する必要があります。つまり、クライアントサイドのコードを書く必要があります。

<!-- 
In the example below we will make a `POST` request, the response will either be success or failure, this will indicate wither the value of the `wporg_field` is valid.
 -->
以下の例では `POST` リクエストを行い、レスポンスは成功か失敗のどちらかで、`wporg_field` の値が有効か否かを示します。

```
/*jslint browser: true, plusplus: true */
(function ($, window, document) {
  'use strict';
  // execute when the DOM is ready
  $(document).ready(function () {
    // js 'change' event triggered on the wporg_field form field
    $('#wporg_field').on('change', function () {
      // jQuery post method, a shorthand for $.ajax with POST
      $.post(wporg_meta_box_obj.url,                        // or ajaxurl
        {
          action: 'wporg_ajax_change',                // POST data, action
          wporg_field_value: $('#wporg_field').val(), // POST data, wporg_field_value
          post_ID: jQuery('#post_ID').val()           // The ID of the post currently being edited
        }, function (data) {
          // handle response data
          if (data === 'success') {
            // perform our success logic
          } else if (data === 'failure') {
            // perform our failure logic
          } else {
            // do nothing
          }
        }
      );
    });
  });
}(jQuery, window, document));
```

<!-- 
We took the WordPress AJAX file URL dynamically from the `wporg_meta_box_obj` JavaScript custom object that we will create in the next step.
 -->
WordPress の AJAX ファイルの URL は、次のステップで作成する JavaScript カスタムオブジェクト `wporg_meta_box_obj` から動的に取得します。

<!-- 
[info]If your meta box only requires the WordPress AJAX file URL; instead of creating a new custom JavaScript object you could use the `ajaxurl` predefined JavaScript variable.
 -->
[info]メタボックスが WordPress の AJAX ファイル URL のみを必要とする場合、新しいカスタム JavaScript オブジェクトを作成する代わりに、定義済みの JavaScript 変数 `ajaxurl` を使用できます。

<!-- 
**Available only in the WordPress Administration.** Make sure it is not empty before performing any logic.[/info]
 -->
**WordPress の管理画面でのみ利用可能です。** ロジックを実行する前に、空でないことを確認してください。[/info]

<!-- 
#### Enqueue Client Side Code
 -->
#### クライアントサイドのコードをエンキューする

<!-- 
Next step is to put our code into a script file and enqueue it on our edit screens.
 -->
次のステップは、コードをスクリプト・ファイルに入れ、編集画面でそれをエンキューすることです。

<!-- 
In the example below we will add the AJAX functionality to the edit screens of the following post types: post, `wporg_cpt`.
 -->
以下の例では、右記の投稿タイプの編集画面に AJAX 機能を追加します: post、`wporg_cpt`。

<!-- 
The script file will reside at `/plugin-name/admin/meta-boxes/js/admin.js`, `plugin-name` being the main plugin folder, `/plugin-name/plugin.php` the file calling the function.
 -->
スクリプトファイルは `/plugin-name/admin/meta-boxes/js/admin.js` に置かれ、`plugin-name` はメインのプラグインフォルダー、`/plugin-name/plugin.php` は関数を呼び出すファイルです。

```
function wporg_meta_box_scripts() {
  // get current admin screen, or null
  $screen = get_current_screen();
  // verify admin screen object
  if (is_object($screen)) {
    // enqueue only for specific post types
    if (in_array($screen->post_type, ['post', 'wporg_cpt'])) {
      // enqueue script
      wp_enqueue_script('wporg_meta_box_script', plugin_dir_url(__FILE__) . 'admin/meta-boxes/js/admin.js', ['jquery']);
      // localize script, create a custom js object
      wp_localize_script(
        'wporg_meta_box_script',
        'wporg_meta_box_obj',
        [
          'url' => admin_url('admin-ajax.php'),
        ]
      );
    }
  }
}
add_action('admin_enqueue_scripts', 'wporg_meta_box_scripts');
```

<!-- 
#### Server Side Code
 -->
#### サーバーサイドのコード

<!-- 
The last step is to write our server side code that is going to handle the request.
 -->
最後のステップは、リクエストを処理するサーバーサイドのコードを書くことです。

```
// The piece after `wp_ajax_`  matches the action argument being sent in the POST request.
add_action( 'wp_ajax_wporg_ajax_change', 'my_ajax_handler' );

/**
 * Handles my AJAX request.
 */
function my_ajax_handler() {
  // Handle the ajax request here
  if ( array_key_exists( 'wporg_field_value', $_POST ) ) {
    $post_id = (int) $_POST['post_ID'];
    if ( current_user_can( 'edit_post', $post_id ) ) {
      update_post_meta(
        $post_id,
        '_wporg_meta_key',
        $_POST['wporg_field_value']
      );
    }
  }

  wp_die(); // All ajax handlers die when finished
}
```

<!-- 
As a final reminder, the code illustrated on this page lacks important operations that take care of security. Be sure your production code includes such operations.
 -->
最後の注意点として、このページで説明されているコードには、セキュリティに配慮した重要な操作が欠けています。本番のコードには、そのような操作が含まれていることを確認してください。

<!-- 
See [Handbook's AJAX Chapter](https://developer.wordpress.org/plugins/javascript/ajax/) and the [Codex](https://codex.wordpress.org/AJAX_in_Plugins) for more on AJAX.
 -->
AJAX については、[ハンドブックの AJAX の章](https://developer.wordpress.org/plugins/javascript/ajax/)と [Codex](https://codex.wordpress.org/AJAX_in_Plugins) を参照してください。

<!-- 
## More Information
 -->
## 詳細情報

<!-- 
- [Complex Meta Boxes in WordPress](https://www.wproots.com/complex-meta-boxes-in-wordpress/)
- [How To Create Custom Post Meta Boxes In WordPress](https://www.smashingmagazine.com/2011/10/create-custom-post-meta-boxes-wordpress/)
- [WordPress Meta Boxes: a Comprehensive Developer's Guide](https://themefoundation.com/wordpress-meta-boxes-guide/)
 -->
- [WordPress における複雑なメタボックス](https://www.wproots.com/complex-meta-boxes-in-wordpress/)
- [WordPress でカスタム投稿メタボックスを作成する方法](https://www.smashingmagazine.com/2011/10/create-custom-post-meta-boxes-wordpress/)
- [WordPress メタボックス: 包括的な開発者ガイド](https://themefoundation.com/wordpress-meta-boxes-guide/)
