<!-- 
# Working with Custom Post Types
 -->
# カスタム投稿タイプの操作

<!-- 
## Custom Post Type Templates
 -->
## カスタム投稿タイプのテンプレート

<!-- 
You can create custom [templates](https://developer.wordpress.org/themes/core-concepts/theme-structure/) for your custom post types. In the same way posts and their archives can be displayed using `single.php` and `archive.php`, you can create the templates:
 -->
カスタム投稿タイプ用にカスタム[テンプレート](https://developer.wordpress.org/themes/core-concepts/theme-structure/)を作成できます。`single.php` と `archive.php` を使用して投稿とそのアーカイブを表示できるのと同じように、テンプレートを作成できます:

<!-- 
- `single-{post_type}.php` – for single posts of a custom post type
- `archive-{post_type}.php` – for the archive
 -->
- `single-{post_type}.php` – カスタム投稿タイプの個別投稿用
- `archive-{post_type}.php` – アーカイブ用

<!-- 
Where `{post_type}` is the post type identifier, used as the `$post_type` argument of the `register_post_type()` function.
 -->
`{post_type}` は投稿タイプ識別子で、`register_post_type()` 関数の引数 `$post_type` として使用されます。

<!-- 
Building upon what we’ve learned previously, you could create `single-wporg_product.php` and `archive-wporg_product.php` template files for single product posts and the archive.
 -->
過去に学んだことをもとに、個別の商品投稿とアーカイブ用に、テンプレートファイル `single-wporg_product.php` と `archive-wporg_product.php` を作成できます。

<!-- 
Alternatively, you can use the [`is_post_type_archive()`](https://developer.wordpress.org/reference/functions/is_post_type_archive/) function in any template file to check if the query shows an archive page of a given post type, and the [`post_type_archive_title()`](https://developer.wordpress.org/reference/functions/post_type_archive_title/)  function to display the post type title.
 -->
あるいは、任意のテンプレートファイルで [`is_post_type_archive()`](https://developer.wordpress.org/reference/functions/is_post_type_archive/) 関数を使用して、クエリーが指定された投稿タイプのアーカイブページを表示しているかどうかをチェックし、[`post_type_archive_title()`](https://developer.wordpress.org/reference/functions/post_type_archive_title/) 関数を使用して投稿タイプのタイトルを表示できます。

<!-- 
## Querying by Post Type
 -->
## 投稿タイプによるクエリー

<!-- 
You can query posts of a specific type by passing the `post_type` key in the arguments array of the `WP_Query` class constructor.
 -->
`WP_Query` クラスのコンストラクタの引数配列に キー `post_type` を渡すことで、特定の型の投稿をクエリーできます。

```
<?php
$args = array(
  'post_type'      => 'product',
  'posts_per_page' => 10,
);
$loop = new WP_Query($args);
while ( $loop->have_posts() ) {
  $loop->the_post();
  ?>
  <div class="entry-content">
    <?php the_title(); ?>
    <?php the_content(); ?>
  </div>
  <?php
}
```

<!-- 
This loops through the latest ten product posts and displays the title and content of them one by one.
 -->
これは、最新の10件の商品投稿をループし、タイトルと内容を1件ずつ表示します。

<!-- 
## Altering the Main Query
 -->
## メインクエリーの変更

<!-- 
Registering a custom post type does not mean it gets added to the main query automatically.
 -->
カスタム投稿タイプを登録しても、それが自動的にメインクエリーに追加される訳ではありません。

<!-- 
If you want your custom post type posts to show up on standard archives or include them on your home page mixed up with other post types, use the [`pre_get_posts`](https://developer.wordpress.org/reference/hooks/pre_get_posts/) action hook.
 -->
カスタム投稿タイプの投稿を標準のアーカイブに表示させたり、他の投稿タイプに混じってトップページに表示させたい場合は、[`pre_get_posts`](https://developer.wordpress.org/reference/hooks/pre_get_posts/) アクションフックを使います。

<!-- 
The next example will show posts from `post`, `page` and `movie` post types on the home page:
 -->
次の例では、投稿タイプ `post`、`page`、`movie` の投稿をホームページに表示します:

```
function wporg_add_custom_post_types($query) {
  if ( is_home() && $query->is_main_query() ) {
    $query->set( 'post_type', array( 'post', 'page', 'movie' ) );
  }
  return $query;
}
add_action('pre_get_posts', 'wporg_add_custom_post_types');
```