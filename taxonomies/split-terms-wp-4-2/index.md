<!-- 
# Term Splitting (WordPress 4.2)
 -->
# ターム分割 (WordPress 4.2)

<!-- 
This information is here for historical purposes. If you're not interested in how terms worked prior to 2015, you can skip this section.
 -->
この情報は、歴史的な目的のためにここにあります。2015年以前のタームのしくみに興味がない場合、このセクションを読み飛ばしていただいて結構です。

<!-- 
## Prior to WordPress 4.2
 -->
## WordPress 4.2以前

<!-- 
Terms in different taxonomies with the same slug shared a single term ID. For instance, a tag and a category with the slug "news" had the same term ID.
 -->
同じスラッグを持つ異なるタクソノミーのタームは、同じターム ID を共有していました。たとえば、「news」というスラッグを持つタグとカテゴリーは、同じターム ID を持ちます。

<!-- 
## WordPress 4.2+
 -->
## WordPress 4.2以降

<!-- 
Beginning with 4.2, when one of these shared terms is updated, it will be split: the updated term will be assigned a new term ID.
 -->
4.2以降、これらの共有タームの1つが更新されると、そのタームは分割されます。更新されたタームには新しいターム ID が割り当てられます。

<!-- 
## What does it mean for you?
 -->
## あなたにとって、それはどういう意味 ?

<!-- 
In the vast majority of situations, this update was seamless and uneventful. However, some plugins and themes who store term IDs in options, post meta, user meta, or elsewhere might have been affected.
 -->
ほとんどの場合、このアップデートはシームレスで問題ありませんでした。しかし、オプション、投稿メタ、ユーザーメタなどにターム ID を格納している一部のプラグインやテーマは影響を受けたかもしれません。

<!-- 
## Handling the Split
 -->
## 分割の処理

<!-- 
WordPress 4.2 includes two different tools to help authors of plugins and themes with the transition.
 -->
WordPress 4.2には、プラグインやテーマの作者の移行を支援する2つの異なるツールが含まれています。

<!-- 
### The `split_shared_term` hook
 -->
### `split_shared_term` フック

<!-- 
When a shared term is assigned a new term ID, a new `split_shared_term` action is fired.
 -->
共有タームに新しいターム ID が割り当てられると、新しいアクション `split_shared_term` が発生します。

<!-- 
Here are a few examples of how plugin and theme authors can leverage this hook to ensure that stored term IDs are updated.
 -->
以下は、プラグインやテーマの作者がこのフックを活用して、格納されているターム ID を確実に更新する方法の例です。

<!-- 
#### Term ID stored in an option
 -->
#### オプションに格納されているターム ID

<!-- 
Let's say your plugin stores an option called `featured_tags` that contains an array of term IDs (`[4, 6, 10]`) that serve as the query parameter for your homepage featured posts section.
 -->
あなたのプラグインがオプション `featured_tags` を保存しており、ホームページの注目投稿セクションのクエリーパラメータとして利用されるターム ID の配列 (`[4, 6, 10]`) を含んでいるとしましょう。

<!-- 
In this example, you'll hook to `split_shared_term` action, check whether the updated term ID is in the array, and update if necessary.
 -->
この例では、アクション `split_shared_term` にフックし、更新されたターム ID が配列内にあるかどうかをチェックし、必要であれば更新します。

```
/**
 * Update featured_tags option when a shared term gets split.
 *
 * @param int    $term_id          ID of the formerly shared term.
 * @param int    $new_term_id      ID of the new term created for the $term_taxonomy_id.
 * @param int    $term_taxonomy_id ID for the term_taxonomy row affected by the split.
 * @param string $taxonomy         Taxonomy for the split term.
 */
function wporg_featured_tags_split( int $term_id, int $new_term_id, int $term_taxonomy_id, string $taxonomy ): void {
  // we only care about tags, so we'll first verify that the taxonomy is post_tag.
  if ( 'post_tag' === $taxonomy ) {

    // get the currently featured tags.
    $featured_tags = get_option( 'featured_tags' );

    // if the updated term is in the array, note the array key.
    $found_term = array_search( $term_id, $featured_tags, true );
    if ( false !== $found_term ) {

      // the updated term is a featured tag! replace it in the array, save the new array.
      $featured_tags[ $found_term ] = $new_term_id;
      update_option( 'featured_tags', $featured_tags );
    }
  }
}
add_action( 'split_shared_term', 'wporg_featured_tags_split', 10, 4 );
```

<!-- 
#### Term ID stored in post meta
 -->
#### 投稿メタに格納されているターム ID

<!-- 
Let's say your plugin stores a term ID in post meta for pages so that you can show related posts for a certain page.
 -->
あるページの関連記事を表示できるように、プラグインがページの投稿メタにターム ID を格納しているとしましょう。

<!-- 
In this case, you need to use the `get_posts()` function to get the pages with your `meta_key` and update the `meta_value` matching the split term ID.
 -->
この場合、`get_posts()` 関数を使用して `meta_key` のページを取得し、分割されたターム ID に一致する `meta_value` を更新する必要があります。

```
/**
 * Update related posts term ID for pages
 *
 * @param int    $term_id          ID of the formerly shared term.
 * @param int    $new_term_id      ID of the new term created for the $term_taxonomy_id.
 * @param int    $term_taxonomy_id ID for the term_taxonomy row affected by the split.
 * @param string $taxonomy         Taxonomy for the split term.
 */
function wporg_page_related_posts_split( int $term_id, int $new_term_id, int $term_taxonomy_id, string $taxonomy ): void {
  // find all the pages where meta_value matches the old term ID.
  $page_ids = get_posts(
    array(
      'post_type'  => 'page',
      'fields'     => 'ids',
      'meta_key'   => 'meta_key',
      'meta_value' => $term_id,
    )
  );

  // if such pages exist, update the term ID for each page.
  if ( $page_ids ) {
    foreach ( $page_ids as $id ) {
      update_post_meta( $id, 'meta_key', $new_term_id, $term_id );
    }
  }
}
add_action( 'split_shared_term', 'wporg_page_related_posts_split', 10, 4 );
```

<!-- 
### The `wp_get_split_term` function
 -->
### `wp_get_split_term` 関数

<!-- 
[info]Using the `split_shared_term` hook is the preferred method for processing Term ID changes.
 -->
[info]ターム ID の変更処理にはフック `split_shared_term` を使うのが望ましいです。

<!-- 
However, there may be cases where Terms are split without your plugin having a chance to hook to the `split_shared_term` action.[/info]
 -->
しかし、プラグインがアクション `split_shared_term` にフックする機会がないまま、タームが分割される場合があるかもしれません。[/info]

<!-- 
WordPress 4.2 stores information about taxonomy terms that have been split, and provides the `wp_get_split_term()` utility function to help developers retrieve this information.
 -->
WordPress 4.2は、分割されたタクソノミータームに関する情報を格納し、開発者がこの情報を取得するのに役立つユーティリティ関数 `wp_get_split_term()` を提供します。

<!-- 
Consider the case above, where your plugin stores term IDs in an option named `featured_tags`. You may want to build a function that validates these tag IDs (perhaps to be run on plugin update), to be sure that none of the featured tags has been split:
 -->
上記のケースを考えてみると、プラグインはターム ID をオプション `featured_tags` に格納します。これらのタグ ID を検証する関数 (プラグイン更新時におそらく実行される) を作り、特集タグが分割されていないことを確認したいかもしれません:

```
/**
 * Retrieve information about split terms and udpates the featured_tags option with the new term IDs.
 *
 * @return void
 */
function wporg_featured_tags_check_split() {
  $featured_tag_ids = get_option( 'featured_tags', array() );

  // check to see whether any IDs correspond to post_tag terms that have been split.
  foreach ( $featured_tag_ids as $index => $featured_tag_id ) {
    $new_term_id = wp_get_split_term( $featured_tag_id, 'post_tag' );

    if ( $new_term_id ) {
      $featured_tag_ids[ $index ] = $new_term_id;
    }
  }

  // save
  update_option( 'featured_tags', $featured_tag_ids );
}
```

<!-- 
Note that `wp_get_split_term()` takes two parameters, `$old_term_id` and `$taxonomy` and returns an integer.
 -->
`wp_get_split_term()` は2つのパラメータ、`$old_term_id` と `$taxonomy`、を取り、整数を返すことに注意してください。

<!-- 
If you need to retrieve a list of all split terms associated with an old Term ID, regardless of taxonomy, use `wp_get_split_terms()`.
 -->
タクソノミーに関係なく、古いターム ID に関連付けられたすべての分割タームのリストを取得する必要がある場合は、`wp_get_split_terms()` を使用します。