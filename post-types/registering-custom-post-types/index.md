<!-- 
# Registering Custom Post Types
 -->
# カスタム投稿タイプの登録

<!-- 
WordPress comes with five default post types: `post`, `page`, `attachment`, `revision`, and `menu`.
 -->
WordPress には、デフォルトで5つの投稿タイプが用意されています: `post`、`page`、`attachment`、`revision`、`menu`。

<!-- 
While developing your plugin, you may need to create your own specific content type: for example, products for an e-commerce website, assignments for an e-learning website, or movies for a review website.
 -->
プラグインを開発する際に、独自のコンテンツタイプを作成する必要があるかもしれません。たとえば、e コマースサイトの商品、e ラーニングサイトの課題、レビューサイトのムービーなどです。

<!-- 
Using Custom Post Types, you can register your own post type. Once a custom post type is registered, it gets a new top-level administrative screen that can be used to manage and create posts of that type.
 -->
カスタム投稿タイプを使用すると、独自の投稿タイプを登録できます。カスタム投稿タイプが登録されると、そのタイプの投稿を管理・作成するための新しいトップレベルの管理画面が表示されます。

<!-- 
To register a new post type, you use the [`register_post_type()`](https://developer.wordpress.org/reference/functions/register_post_type/) function.
 -->
新しい投稿タイプを登録するには、[`register_post_type()`](https://developer.wordpress.org/reference/functions/register_post_type/) 関数を使用します。

<!-- 
[alert]We recommend that you put custom post types in a plugin rather than a theme. This ensures that user content remains portable even if the theme is changed.[/alert]
 -->
[alert]カスタム投稿タイプは、テーマではなくプラグインに入れることをおすすめします。これにより、テーマが変更されてもユーザーコンテンツが移植可能なままであることが保証されます。[/alert]

<!-- 
The following minimal example registers a new post type, Products, which is identified in the database as `wporg_product`.
 -->
以下の最小限の例では、データベースで `wporg_product` として識別される、新しい投稿タイプ Products を登録しています。

```
function wporg_custom_post_type() {
  register_post_type('wporg_product',
    array(
      'labels'      => array(
        'name'          => __('Products', 'textdomain'),
        'singular_name' => __('Product', 'textdomain'),
      ),
      'public'      => true,
      'has_archive' => true,
    )
  );
}
add_action('init', 'wporg_custom_post_type');
```

<!-- 
Please visit the reference page for [`register_post_type()`](https://developer.wordpress.org/reference/functions/register_post_type/) for the description of arguments.
 -->
引数の説明は、[`register_post_type()`](https://developer.wordpress.org/reference/functions/register_post_type/) のリファレンスページを参照してください。

<!-- 
[warning]You must call `register_post_type()` before the [`admin_init`](https://developer.wordpress.org/reference/hooks/admin_init/) hook and after the [`after_setup_theme`](https://developer.wordpress.org/reference/hooks/after_setup_theme/) hook. A good hook to use is the [`init`](https://developer.wordpress.org/reference/hooks/init/) action hook.[/warning]
 -->
[warning]`register_post_type()` は、[`after_setup_theme`](https://developer.wordpress.org/reference/hooks/after_setup_theme/) フックの後、[`admin_init`](https://developer.wordpress.org/reference/hooks/admin_init/) フックの前、に呼び出す必要があります。使用するフックとしては、[`init`](https://developer.wordpress.org/reference/hooks/init/) アクションフックが良いでしょう。[/warning]

<!-- 
## Naming Best Practices
 -->
## ネーミングのベスト・プラクティス

<!-- 
It is important that you prefix your post type functions and identifiers with a short prefix that corresponds to your plugin, theme, or website.
 -->
投稿タイプの関数や識別子には、プラグインやテーマ、Web サイトに対応する短い接頭辞をつけることが重要です。

<!-- 
[warning]**Make sure your custom post type identifier does not exceed 20 characters** as the `post_type` column in the database is currently a VARCHAR field of that length.[/warning]
 -->
[warning]現在のデータベースの VARCHAR 型フィールド、`post_type` カラム長は20ですので、**カスタム投稿タイプの識別子は、20文字を超えないようにしてください。**[/warning]

<!-- 
[warning]**To ensure forward compatibility**, do not use `wp_` as your identifier — it is being used by WordPress core.[/warning]
 -->
[warning]**前方互換性を確保するため、**識別子として `wp_` を使用しないでください — これは WordPress コアで使用されています。[/warning]

<!-- 
[warning]If your identifier is too generic (for example: `product`), it may conflict with other plugins or themes that have chosen to use that same identifier.[/warning]
 -->
[warning]識別子が一般的すぎる場合 (例: `product`)、同じ識別子を使用している他のプラグインやテーマと競合する可能性があります。[/warning]

<!-- 
[info]**Solving duplicate post type identifiers is not possible without disabling one of the conflicting post types.**[/info]
 -->
[info]**投稿タイプ識別子の重複を解決するには、競合する投稿タイプのいずれかを無効にしなければなりません。**[/info]

<!-- 
## URLs
 -->
## URL

<!-- 
A custom post type gets its own slug within the site URL structure.
 -->
カスタム投稿タイプは、サイトの URL 構造内で独自のスラッグを取得します。

<!-- 
A post of type `wporg_product` will use the following URL structure by default: `https://example.com/wporg_product/%product_name%`.
 -->
タイプ `wporg_product` の投稿は、デフォルトで右に示す URL 構造を使用します: `https://example.com/wporg_product/%product_name%`

<!-- 
`wporg_product` is the slug of your custom post type and `%product_name%` is the slug of your particular product.
 -->
`wporg_product` はカスタム投稿タイプのスラッグで、`%product_name%` は特定の商品のスラッグです。

<!-- 
The final permalink would be: `https://example.com/wporg_product/wporg-is-awesome`.
 -->
最終的なパーマリンクは、こうなります: `https://example.com/wporg_product/wporg-is-awesome`

<!-- 
You can see the permalink on the edit screen for your custom post type, just like with default post types.
 -->
カスタム投稿タイプの編集画面では、デフォルトの投稿タイプと同じようにパーマリンクを見ることができます。

<!-- 
### A Custom Slug for a Custom Post Type
 -->
### カスタム投稿タイプ用のカスタムスラッグ

<!-- 
To set a custom slug for the slug of your custom post type all you need to do is add a key => value pair to the `rewrite` key in the `register_post_type()` arguments array.
 -->
カスタム投稿タイプのスラッグにカスタムスラッグを設定するには、引数配列 `register_post_type()` のキー `rewrite` に、KVP (キー => 値 ペア) を追加するだけです。

<!-- 
Example:
 -->
例:

```
function wporg_custom_post_type() {
  register_post_type('wporg_product',
    array(
      'labels'      => array(
        'name'          => __( 'Products', 'textdomain' ),
        'singular_name' => __( 'Product', 'textdomain' ),
      ),
      'public'      => true,
      'has_archive' => true,
      'rewrite'     => array( 'slug' => 'products' ), // my custom slug
    )
  );
}
add_action('init', 'wporg_custom_post_type');
```

<!-- 
The above will result in the following URL structure: `https://example.com/products/%product_name%`
 -->
上記の結果、URL 構造は次のようになります: `https://example.com/products/%product_name%`

<!-- 
[warning]Using a generic slug like `products` can potentially conflict with other plugins or themes, so try to use one that is more specific to your content.[/warning]
 -->
[warning]`products` のような一般的なスラッグを使用すると、他のプラグインやテーマと競合する可能性があるため、よりコンテンツに特化したものを使用するようにしましょう。[/warning]

<!-- 
[info]Unlike the custom post type identifiers, the duplicate slug problem can be solved easily by changing the slug for one of the conflicting post types.[/info]
 -->
[info]カスタム投稿タイプの識別子とは異なり、スラッグの重複問題は、競合する投稿タイプの1つのスラッグを変更することで、簡単に解決できます。[/info]

<!-- 
If the plugin author included an `apply_filters()` call on the arguments, this can be done programmatically by overriding the arguments submitted via the `register_post_type()` function.
 -->
プラグインの作者が引数に `apply_filters()` コールを含んでいた場合、`register_post_type()` 関数を介して、送信された引数をオーバーライドすることでプログラム的に行うことができます。