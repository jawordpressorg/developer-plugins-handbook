<!--
# Top-Level Menus
-->

# トップレベルメニュー

<!--
## Add a Top-Level Menu
-->

## トップレベルメニューの追加

<!--
To add a new Top-level menu to WordPress Administration, use the [`add_menu_page()`](https://developer.wordpress.org/reference/functions/add_menu_page/) function.
-->

WordPress の管理画面に新しいトップレベルメニューを追加するには、[`add_menu_page()`](https://developer.wordpress.org/reference/functions/add_menu_page/) 関数を使用します。

```
add_menu_page(
  string $page_title,
  string $menu_title,
  string $capability,
  string $menu_slug,
  callable $function = '',
  string $icon_url = '',
  int $position = null
);
```

<!--
### Example
-->

### 例

<!--
Lets say we want to add a new Top-level menu called "WPOrg".
-->

たとえば、「WPOrg」という新しいトップレベルメニューを追加したいとします。

<!--
**The first step** will be creating a function which will output the HTML. In this function we will perform the necessary security checks and render the options we've registered using the [Settings API](https://developer.wordpress.org/plugins/settings/).
-->

**第一のステップ** では、HTML を出力する関数を作成します。この関数では、必要なセキュリティチェックを行い、[設定 API](https://developer.wordpress.org/plugins/settings/) を使って登録したオプションを書き出します。

<!--
[info]We recommend wrapping your HTML using a `<div>` with a class of `wrap`.[/info]
-->

[info]HTML をラップするには、クラスが `wrap` の `<div>` を使用することをおすすめします。[/info]

```
function wporg_options_page_html() {
?>
  <div class="wrap">
    <h1><?php echo esc_html( get_admin_page_title() ); ?></h1>
    <form action="options.php" method="post">
      <?php
      // output security fields for the registered setting "wporg_options"
      settings_fields( 'wporg_options' );
      // output setting sections and their fields
      // (sections are registered for "wporg", each field is registered to a specific section)
      do_settings_sections( 'wporg' );
      // output save settings button
      submit_button( __( 'Save Settings', 'textdomain' ) );
      ?>
    </form>
  </div>
<?php
}
```

<!--
**The second step** will be registering our WPOrg menu. The registration needs to occur during the `admin_menu` action hook.
-->

**第二のステップ** では、WPOrg メニューを登録します。この登録は `admin_menu` アクションフックで行う必要があります。

```
add_action( 'admin_menu', 'wporg_options_page' );
function wporg_options_page() {
  add_menu_page(
    'WPOrg',
    'WPOrg Options',
    'manage_options',
    'wporg',
    'wporg_options_page_html',
    plugin_dir_url(__FILE__) . 'images/icon_wporg.png',
    20
  );
}
```

<!--
For a list of parameters and what each do please see the [`add_menu_page()`](https://developer.wordpress.org/reference/functions/add_menu_page/) in the reference.
-->

パラメータのリストとそれぞれの役割については、リファレンスの [`add_menu_page()`](https://developer.wordpress.org/reference/functions/add_menu_page/) を参照してください。

<!--
### Using a PHP File for HTML
-->

### HTML 用 PHP ファイルの使用

<!--
The best practice for portable code would be to create a Callback that requires/includes your PHP file.
-->

移植可能なコードを作成するためのベストプラクティスは、PHP ファイルを require/include するコールバックを作成することです。

<!--
For the sake of completeness and helping you understand legacy code, we will show another way: passing a `PHP file path` as the `$menu_slug` parameter with an `null` `$function` parameter.
-->

完璧を期すため、またレガシーコードを理解してもらうため、別の方法を示しましょう: これは、`PHP ファイルパス` を `$menu_slug` パラメータとして渡し、`null` `$function` パラメータを渡すものです。

```
add_action( 'admin_menu', 'wporg_options_page' );
function wporg_options_page() {
  add_menu_page(
    'WPOrg',
    'WPOrg Options',
    'manage_options',
    plugin_dir_path(__FILE__) . 'admin/view.php',
    null,
    plugin_dir_url(__FILE__) . 'images/icon_wporg.png',
    20
  );
}
```

<!--
## Remove a Top-Level Menu
-->

## トップレベルメニューの削除

<!--
To remove a registered menu from WordPress Administration, use the [`remove_menu_page()`](https://developer.wordpress.org/reference/functions/remove_menu_page/) function.
-->

WordPress の管理画面から登録したメニューを削除するには、[`remove_menu_page()`](https://developer.wordpress.org/reference/functions/remove_menu_page/) 関数を使用します。

```
remove_menu_page(
  string $menu_slug
);
```

<!--
[warning]Removing menus won't prevent users accessing them directly.
This should never be used as a way to restrict [user capabilities](https://developer.wordpress.org/plugins/users/roles-and-capabilities/).[/warning]
-->

[warning]メニューを削除しても、ユーザーが直接メニューにアクセスすることは防げません。
[ユーザーの権限](https://developer.wordpress.org/plugins/users/roles-and-capabilities/)を制限する方法として、これは決して使用されるべきではありません。[/warning]

<!--
### Example
-->

### 例

<!--
Lets say we want to remove the "Tools" menu from.
-->

たとえば、「ツール」メニューを削除したいとします。

```
add_action( 'admin_menu', 'wporg_remove_options_page', 99 );
function wporg_remove_options_page() {
  remove_menu_page( 'tools.php' );
}
```

<!--
Make sure that the menu have been registered with the `admin_menu` hook before attempting to remove, specify a higher priority number for [`add_action()`](https://developer.wordpress.org/reference/functions/add_action/).
-->

メニューが `admin_menu` フックに登録されていることを確認してから削除を試み、[`add_action()`](https://developer.wordpress.org/reference/functions/add_action/) に高い優先順位を指定してください。

<!--
## Submitting forms
-->

## フォームの送信

<!--
To process the submissions of forms on options pages, you will need two things:
-->

オプションページでフォームの送信を処理するには、2つのものが必要です:

<!--
1. Use the URL of the page as the `action` attribute of the form.
2. Add a hook with the slug, returned by `add_menu_page`.
-->

1. フォームの `action` 属性としてページの URL を使用する。
2. `add_menu_page` が返すスラッグをフックに追加する。

<!--
[info]You only need to follow those steps if you are manually creating forms in the back-end. The [Settings API](https://developer.wordpress.org/plugins/settings/) is the recommended way to do this.[/info]
-->

[info]バックエンドでフォームを手動で作成する場合のみ、これらの手順を踏む必要があります。[設定 API](https://developer.wordpress.org/plugins/settings/) を使用することをおすすめします。[/info]

<!--
### Form action attribute
-->

### フォームのアクション属性

<!--
Use the `$menu_slug` parameter of the options page as the first parameter of [`menu_page_url()`](https://developer.wordpress.org/reference/functions/menu_page_url/). By the function will automatically escape URL and echo it by default, so you can directly use it within the `<form>` tag:
-->

オプションページの `$menu_slug` パラメータを [`menu_page_url()`](https://developer.wordpress.org/reference/functions/menu_page_url/) の最初のパラメータとして使用します。この関数はデフォルトで自動的に URL をエスケープして出力するので、`<form>` タグ内で直接使用できます:

```
<form action="<?php menu_page_url( 'wporg' ) ?>" method="post">
```

<!--
### Processing the form
-->

### フォームの処理

<!--
The `$function` you specify while adding the page will only be called once it is time to display the page, which makes it inappropriate if you need to send headers (ex. redirects) back to the browser.
-->

ページを追加するときに指定した `$function` は、ページを表示するときに初めて呼び出されるため、ブラウザーにヘッダー (リダイレクトなど) を送り返す必要がある場合には不適切です。

<!--
`add_menu_page` returns a `$hookname`, and WordPress triggers the `"load-$hookname"` action before any HTML output. You can use this to assign a function, which could process the form.
-->

`add_menu_page` は `$hookname` を返し、WordPress は HTML が出力される前に `"load-$hookname"` アクションをトリガーします。これを利用して、フォームを処理する関数を割り当てることができます。

<!--
[info]`"load-$hookname"` will be executed every time before an options page will be displayed, even when the form is not being submitted.[/info]
-->

[info]`"load-$hookname"` は、フォームが送信されていないときでも、オプションページが表示される前に毎回実行されます。[/info]

<!--
With the return parameter and action in mind, the example from above would like this:
-->

リターン・パラメータとアクションを念頭に置くと、上記の例は次のようになります:

```
add_action( 'admin_menu', 'wporg_options_page' );
function wporg_options_page() {
  $hookname = add_menu_page(
    'WPOrg',
    'WPOrg Options',
    'manage_options',
    'wporg',
    'wporg_options_page_html',
    plugin_dir_url(__FILE__) . 'images/icon_wporg.png',
    20
  );

  add_action( 'load-' . $hookname, 'wporg_options_page_submit' );
}
```

<!--
You can program `wporg_options_page_submit` according to your needs, but keep in mind that you must manually perform all necessary checks, including:
-->

`wporg_options_page_submit` は、必要に応じてプログラムできますが、以下のような必要なチェックをすべて手動で行わなければならないことを覚えておいてください:

<!--
1. Whether the form is being submitted (`'POST' === $_SERVER['REQUEST_METHOD']`).
2. [CSRF verification](https://developer.wordpress.org/apis/security/nonces/)
3. Validation
4. Sanitization
-->

1. フォームが送信されているかどうか (`'POST' === $_SERVER['REQUEST_METHOD']`)
2. [CSRF 検証](https://developer.wordpress.org/apis/security/nonces/)
3. バリデーション
4. サニタイゼーション
