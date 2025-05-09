<!--
# Sub-Menus
-->

# サブメニュー

<!--
## Add a Sub-Menu
-->

## サブメニューの追加

<!--
To add a new Sub-menu to WordPress Administration, use the `add_submenu_page()` function.
-->

WordPress の管理画面に新しいサブメニューを追加するには、`add_submenu_page()` 関数を使用します。

```
add_submenu_page(
  string $parent_slug,
  string $page_title,
  string $menu_title,
  string $capability,
  string $menu_slug,
  callable $function = ''
);
```

<!--
### Example
-->

### 例

<!--
Lets say we want to add a Sub-menu "WPOrg Options" to the "Tools" Top-level menu.
-->

たとえば、「ツール」のトップレベルメニューに "WPOrg Options" というサブメニューを追加したいとします。

<!--
**The first step** will be creating a function which will output the HTML. In this function we will perform the necessary security checks and render the options we’ve registered using the [Settings API](https://developer.wordpress.org/plugins/settings/).
-->

**第一のステップ** では、HTML を出力する関数を作成します。この関数では、必要なセキュリティチェックを行い、[設定 API](https://ja.wordpress.org/team/handbook/plugin-development/settings/) を使って登録したオプションを書き出します。

<!--
[info]We recommend wrapping your HTML using a `<div>` with a class of `wrap`.[/info]
-->

[info]HTML をラップするには、クラスが `wrap` の `<div>` を使用することをおすすめします。[/info]

```
function wporg_options_page_html() {
  // check user capabilities
  if ( ! current_user_can( 'manage_options' ) ) {
    return;
  }
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
**The second step** will be registering our WPOrg Options Sub-menu. The registration needs to occur during the `admin_menu` action hook.
-->

**第二のステップ** では、WPOrg オプションサブメニューを登録します。この登録は `admin_menu` アクションフックで行う必要があります。

```
function wporg_options_page() {
  add_submenu_page(
    'tools.php',
    'WPOrg Options',
    'WPOrg Options',
    'manage_options',
    'wporg',
    'wporg_options_page_html'
  );
}
add_action( 'admin_menu', 'wporg_options_page' );
```

<!--
For a list of parameters and what each do please see the [`add_submenu_page()`](https://developer.wordpress.org/reference/functions/add_submenu_page/) in the reference.
-->

パラメータのリストとそれぞれの役割については、リファレンスの [`add_submenu_page()`](https://developer.wordpress.org/reference/functions/add_submenu_page/) を参照してください。

<!--
## Predefined Sub-Menus
-->

## 定義済みサブメニュー

<!--
Wouldn’t it be nice if we had helper functions that define the `$parent_slug` for WordPress built-in Top-level menus and save us from manually searching it through the source code?
-->

WordPress 組込みトップレベルメニューの `$parent_slug` を定義するヘルパー関数があれば、ソースコードから手作業で探す手間が省けていいと思いませんか ?

<!--
Below is a list of parent slugs and their helper functions:
-->

以下は、親スラッグとそのヘルパー関数のリストです:

<!--
- [`add_dashboard_page()`](https://developer.wordpress.org/reference/functions/add_dashboard_page/) – `index.php`
- [`add_posts_page()`](https://developer.wordpress.org/reference/functions/add_posts_page/) – `edit.php`
- [`add_media_page()`](https://developer.wordpress.org/reference/functions/add_media_page/) – `upload.php`
- [`add_pages_page()`](https://developer.wordpress.org/reference/functions/add_pages_page/) – `edit.php?post_type=page`
- [`add_comments_page()`](https://developer.wordpress.org/reference/functions/add_comments_page/) – `edit-comments.php`
- [`add_theme_page()`](https://developer.wordpress.org/reference/functions/add_theme_page/) – `themes.php`
- [`add_plugins_page()`](https://developer.wordpress.org/reference/functions/add_plugins_page/) – `plugins.php`
- [`add_users_page()`](hhttps://developer.wordpress.org/reference/functions/add_users_page/) – `users.php`
- [`add_management_page()`](https://developer.wordpress.org/reference/functions/add_management_page/) – `tools.php`
- [`add_options_page()`](https://developer.wordpress.org/reference/functions/add_options_page/) – `options-general.php`
- [`add_options_page()`](https://developer.wordpress.org/reference/functions/add_options_page/) – `settings.php`
- [`add_links_page()`](https://developer.wordpress.org/reference/functions/add_links_page/) – `link-manager.php` – requires a plugin since WP 3.5+
- Custom Post Type – `edit.php?post_type=wporg_post_type`
- Network Admin – `settings.php`
-->

- [`add_dashboard_page()`](https://developer.wordpress.org/reference/functions/add_dashboard_page/) – `index.php`
- [`add_posts_page()`](https://developer.wordpress.org/reference/functions/add_posts_page/) – `edit.php`
- [`add_media_page()`](https://developer.wordpress.org/reference/functions/add_media_page/) – `upload.php`
- [`add_pages_page()`](https://developer.wordpress.org/reference/functions/add_pages_page/) – `edit.php?post_type=page`
- [`add_comments_page()`](https://developer.wordpress.org/reference/functions/add_comments_page/) – `edit-comments.php`
- [`add_theme_page()`](https://developer.wordpress.org/reference/functions/add_theme_page/) – `themes.php`
- [`add_plugins_page()`](https://developer.wordpress.org/reference/functions/add_plugins_page/) – `plugins.php`
- [`add_users_page()`](https://developer.wordpress.org/reference/functions/add_users_page/) – `users.php`
- [`add_management_page()`](https://developer.wordpress.org/reference/functions/add_management_page/) – `tools.php`
- [`add_options_page()`](https://developer.wordpress.org/reference/functions/add_options_page/) – `options-general.php`
- [`add_options_page()`](https://developer.wordpress.org/reference/functions/add_options_page/) – `settings.php`
- [`add_links_page()`](https://developer.wordpress.org/reference/functions/add_links_page/) – `link-manager.php` – WordPress 3.5以降ではプラグインが必要です。
- カスタム投稿タイプ – `edit.php?post_type=wporg_post_type`
- ネットワーク管理 – `settings.php`

<!--
## Remove a Sub-Menu
-->

## サブメニューの削除

<!--
The process of removing Sub-menus is exactly the same as [removing Top-level menus](https://developer.wordpress.org/plugins/administration-menus/top-level-menus/#remove-a-top-level-menu).
-->

サブメニューの削除方法は、[トップレベルメニューの削除方法](https://ja.wordpress.org/team/handbook/plugin-development/administration-menus/top-level-menus/#remove-a-top-level-menu)とまったく同じです。

<!--
## Submitting forms
-->

## フォームの送信

<!--
The process of handling form submissions within Sub-menus is exactly the same as [Submitting forms within Top-Level Menus](https://developer.wordpress.org/plugins/administration-menus/top-level-menus/#submitting-forms).
-->

サブメニュー内でのフォーム送信の処理は、[トップレベルメニュー内でのフォーム送信](https://ja.wordpress.org/team/handbook/plugin-development/administration-menus/top-level-menus/#submitting-forms)とまったく同じです。

<!--
`add_submenu_page()` along with all functions for pre-defined sub-menus (`add_dashboard_page`, `add_posts_page`, etc.) will return a `$hookname`, which you can use as the first parameter of `add_action` in order to handle the submission of forms within custom pages:
-->

`add_submenu_page()` は、定義済みのサブメニュー (`add_dashboard_page`、`add_posts_page` など) のすべての関数と一緒に `$hookname` を返し、カスタムページ内のフォーム送信を処理するために `add_action` の最初のパラメータとして使用できます:

```
function wporg_options_page() {
  $hookname = add_submenu_page(
    'tools.php',
    'WPOrg Options',
    'WPOrg Options',
    'manage_options',
    'wporg',
    'wporg_options_page_html'
    );

  add_action( 'load-' . $hookname, 'wporg_options_page_html_submit' );
}

add_action( 'admin_menu', 'wporg_options_page' );
```

<!--
As always, do not forget to check whether the form is being submitted, do CSRF verification, [validation](https://developer.wordpress.org/apis/security/data-validation/), and [sanitization](https://developer.wordpress.org/apis/security/sanitizing/).
-->

例によって、フォームが送信されているかどうかのチェック、CSRF の検証、[バリデーション](https://developer.wordpress.org/apis/security/data-validation/)、[サニタイズ](https://developer.wordpress.org/apis/security/sanitizing/)を忘れないでください。
