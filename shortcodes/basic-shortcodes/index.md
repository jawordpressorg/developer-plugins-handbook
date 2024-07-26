<!-- 
# Basic Shortcodes
 -->
# 基本のショートコード

<!-- 
## Add a Shortcode
 -->
## ショートコードの追加

<!-- 
It is possible to add your own shortcodes by using the Shortcode API. The process involves registering a callback `$func` to a shortcode `$tag` using `add_shortcode()`.
 -->
ショートコード API を使用して、独自のショートコードを追加できます。その手順としては、`add_shortcode()` を使って、ショートコード `$tag` にコールバック `$func` を登録します。

```
add_shortcode(
  string $tag,
  callable $func
);
```

<!-- 
`[wporg]` is your new shortcode. The use of the shortcode will trigger the `wporg_shortcode` callback function.
 -->
`[wporg]` は、あなたの新しいショートコードです。このショートコードを使うと、コールバック関数 `wporg_shortcode` が起動します。

```
add_shortcode( 'wporg', 'wporg_shortcode' );
function wporg_shortcode( $atts = [], $content = null) {
  // do something to $content
  // always return
  return $content;
}
```

<!-- 
## Remove a Shortcode
 -->
## ショートコードの削除

<!-- 
It is possible to remove shortcodes by using the Shortcode API. The process involves removing a registered `$tag` using [`remove_shortcode()`](https://developer.wordpress.org/reference/functions/remove_shortcode/).
 -->
ショートコード API を使用して、ショートコードを削除できます。その手順としては、[`remove_shortcode()`](https://developer.wordpress.org/reference/functions/remove_shortcode/) を使って、登録されている `$tag` を削除します。

```
remove_shortcode(
  string $tag
);
```

<!-- 
Make sure that the shortcode have been registered before attempting to remove. Specify a higher priority number for [`add_action()`](https://developer.wordpress.org/reference/functions/add_action/) or hook into an action hook that is run later.
 -->
削除する前に、ショートコードが登録されていることを確認してください。[`add_action()`](https://developer.wordpress.org/reference/functions/add_action/) に高い優先順位を指定するか、後で実行されるアクションフックにフックしてください。

<!-- 
## Check if a Shortcode Exists
 -->
## ショートコードが存在するか否かのチェック

<!-- 
To check whether a shortcode has been registered use [`shortcode_exists()`](https://developer.wordpress.org/reference/functions/shortcode_exists/).
 -->
ショートコードが登録されているか否かを確認するには、[`shortcode_exists()`](https://developer.wordpress.org/reference/functions/shortcode_exists/) を使用します。