<!-- 
# Enclosing Shortcodes
 -->
# ショートコードの包含

<!-- 
The are two scenarios for using shortcodes:
 -->
ショートコードを使用するシナリオには2種類あります:

<!-- 
- The shortcode is a self-closing tag like we seen in the [Basic Shortcodes](https://developer.wordpress.org/plugins/shortcodes/basic-shortcodes/) section.
- The shortcode is enclosing content.
 -->
- ショートコードは、[基本のショートコード](https://developer.wordpress.org/plugins/shortcodes/basic-shortcodes/)のセクションで見たように、自己完結型のタグです。
- ショートコードは、コンテンツを包含するタグ。

<!-- 
## Enclosing Content
 -->
## コンテンツの包含

<!-- 
Enclosing content with a shortcode allows manipulations on the enclosed content.
 -->
ショートコードでコンテンツを包含することで、包含コンテンツに対する操作が可能になります。

```
[wporg]content to manipulate[/wporg]
```

<!-- 
As seen above, all you need to do in order to enclose a section of content is add a beginning `[$tag]` and an end `[/$tag]`, similar to HTML.
 -->
上で見たように、コンテンツのセクションを包含するために必要なことは、HTML と同じように、始まりの `[$tag]` と終わりの `[/$tag]` を追加することです。

<!-- 
## Processing Enclosed Content
 -->
## 包含コンテンツの処理

<!-- 
Lets get back to our original `[wporg]` shortcode code:
 -->
元のショートコード `[wporg]` に戻りましょう:

```
function wporg_shortcode( $atts = array(), $content = null ) {
  // do something to $content
  // always return
  return $content;
}
add_shortcode( 'wporg', 'wporg_shortcode' );
```

<!-- 
Looking at the callback function we see that we chose to accept two parameters, `$atts` and `$content`. The `$content` parameter is going to hold our enclosed content. We will talk about `$atts` later.
 -->
コールバック関数を見ると、`$atts` と `$content` の2つのパラメータを受け取るようにしたことがわかります。パラメータ `$content` は、包含した内容を保持します。`$atts` については後で説明します。

<!-- 
The default value of `$content` is set to `null` so we can differentiate between a self-closing tag and enclosing tags by using PHP function [`is_null()`](https://www.php.net/manual/en/function.is-null.php).
 -->
`$content` のデフォルト値は `null` に設定されているので、PHP 関数 [`is_null()`](https://www.php.net/manual/en/function.is-null.php) を使うことで、自己完結型タグと内包型タグを区別できます。

<!-- 
The shortcode `[$tag]`, including its content and the end `[/$tag]` will be replaced with the **return value** of the handler function.
 -->
ショートコード `[$tag]` は、その内容と末尾の `[/$tag]` も含めて、ハンドラ関数の **戻り値** に置き換えられます。

<!-- 
[alert]It is the responsibility of the handler function to [secure the output](https://developer.wordpress.org/plugins/security/securing-output/).[/alert]
 -->
[alert][出力の安全確保](https://developer.wordpress.org/plugins/security/securing-output/)は、ハンドラ関数の責任です。[/alert]

<!-- 
## Shortcode-ception
 -->
## 入れ子状態のショートコード

<!-- 
The shortcode parser performs a **single pass** on the content of the post.
 -->
ショートコード・パーサーは、投稿のコンテンツに対して **シングルパス** を実行します。

<!-- 
This means that if the `$content` parameter of a shortcode handler contains another shortcode, it won’t be parsed. In this example, `[shortcode]` will not be processed:
 -->
つまり、ショートコード・ハンドラの `$content` パラメータに、別のショートコードが含まれている場合、そのショートコードは解析されません。この例では、`[shortcode]` は、処理されません:

```
[wporg]another [shortcode] is included[/wporg]
```

<!-- 
Using shortcodes inside other shortcodes is possible by calling `do_shortcode()` on the **final return value** of the handler function.
 -->
ハンドラ関数の **最終戻り値** で `do_shortcode()` を呼び出すことで、他のショートコードの中でショートコードを使用できます。

```
function wporg_shortcode( $atts = array(), $content = null ) {
  // do something to $content
  // run shortcode parser recursively
  $content = do_shortcode( $content );
  // always return
  return $content;
}
add_shortcode( 'wporg', 'wporg_shortcode' );
```

<!-- 
## Limitations
 -->
## 制限事項

<!-- 
The shortcode parser is unable to handle mixing of enclosing and non-enclosing forms of the same `[$tag]`.
 -->
ショートコード・パーサーは、同じ `[$tag]` を包含する形式と包含しない形式を混在させて扱うことができません。

```
[wporg] non-enclosed content [wporg]enclosed content[/wporg]
```

<!-- 
Instead of being treated as two shortcodes separated by the text "`non-enclosed content`", the parser treats this as a single shortcode enclosing "`non-enclosed content [wporg]enclosed content`".
 -->
パーサーは、「`non-enclosed content`」というテキストで区切られた2つのショートコードとして扱われる代わりに、これを「`non-enclosed content [wporg]enclosed content`」を包含する1つのショートコードとして扱います。
