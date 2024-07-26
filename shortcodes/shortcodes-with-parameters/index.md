<!-- 
# Shortcodes with Parameters
 -->
# パラメータを持つショートコード

<!-- 
Now that we know how to create a [basic shortcode](https://developer.wordpress.org/plugins/shortcodes/basic-shortcodes/) and how to use it as [self-closing and enclosing](https://developer.wordpress.org/plugins/shortcodes/enclosing-shortcodes/), we will look at using parameters in shortcode `[$tag]` and handler function.
 -->
[基本のショートコード](https://developer.wordpress.org/plugins/shortcodes/basic-shortcodes/)の作成方法と、[自己完結型と包含型](https://developer.wordpress.org/plugins/shortcodes/enclosing-shortcodes/)の使い方が分かったところで、ショートコード `[$tag]` とハンドラ関数でパラメータを使用する方法を説明します。

<!-- 
Shortcode `[$tag]` can accept parameters, known as attributes:
 -->
ショートコード `[$tag]` は、属性と呼ばれるパラメータを受け取ることができます:

```
[wporg title="WordPress.org"]
  Having fun with WordPress.org shortcodes.
[/wporg]
```

<!-- 
Shortcode handler function can accept 3 parameters:
 -->
ショートコード・ハンドラ関数は、3つのパラメータを受け取ることができます:

<!-- 
- `$atts` – array – `[$tag]` attributes
- `$content` – string – The content inside your shortcode. In the exampe above, it will be "Having fun with WordPress.org shortcodes".
- `$tag` – string – the name of the `[$tag]` (i.e. the name of the shortcode)
 -->
- `$atts` – 配列 – `[$tag]` 属性。
- `$content` – 文字列 – ショートコードの内容。上の例では、「Having fun with WordPress.org shortcodes」となります。
- `$tag` – 文字列 – `[$tag]` の名前です (つまりショートコードの名前)。

```
function wporg_shortcode( $atts = array(), $content = null, $tag = '' ) {}
```

<!-- 
## Parsing Attributes
 -->
## 属性のパース (構文解析)

<!-- 
For the user, shortcodes are just strings with square brackets inside the post content. The user have no idea which attributes are available and what happens behind the scenes.
 -->
ユーザーにとって、ショートコードは投稿コンテンツの中にある、角括弧 [] 付きの文字列でしかありません。ユーザーは、どの属性が利用可能で、舞台裏で何が起こっているのか分かりません。

<!-- 
For plugin developers, there is no way to enforce a policy on the use of attributes. The user may include one attribute, two or none at all.
 -->
プラグイン開発者にとって、属性の使用に関するポリシーを強制する方法はありません。ユーザーは、属性を1つ含めることも、2つ含めることも、まったく含めないこともできます。

<!-- 
To gain control of how the shortcodes are used:
 -->
ショートコードの使用方法を制御するには:

<!-- 
- Declare default parameters for the handler function.
- Performing normalization of the key case for the attributes array with [`array_change_key_case()`](https://www.php.net/manual/en/function.array-change-key-case.php).
- Parse attributes using [`shortcode_atts()`](https://developer.wordpress.org/reference/functions/shortcode_atts/) providing default values array and user `$atts`.
- [Secure the output](https://developer.wordpress.org/apis/security/escaping/) before returning it.
 -->
- ハンドラ関数用のデフォルトパラメータを宣言しましょう。
- [`array_change_key_case()`](https://www.php.net/manual/en/function.array-change-key-case.php) で属性配列用のキーケースを正規化しましょう。
- [`shortcode_atts()`](https://developer.wordpress.org/reference/functions/shortcode_atts/) を使用して属性を構文解析し、デフォルト値の配列とユーザー `$atts` を提供しましょう。
- 出力を返す前に、[出力の安全確保](https://developer.wordpress.org/apis/security/escaping/)をしましょう。

<!-- 
## Complete Example
 -->
## 完全な例

<!-- 
Complete example using a basic shortcode structure, taking care of self-closing and enclosing scenarios and securing output.
 -->
基本的なショートコード構造、自己完結型と包含型のシナリオ、出力の安全確保、を使用した完全な例です。

<!-- 
A `[wporg]` shortcode that will accept a title and will display a box that we can style with CSS.
 -->
ショートコード `[wporg]` は、タイトルを受け取り、CSS でスタイルを設定できるボックスを表示します。

```
/**
 * The [wporg] shortcode.
 *
 * Accepts a title and will display a box.
 *
 * @param array  $atts    Shortcode attributes. Default empty.
 * @param string $content Shortcode content. Default null.
 * @param string $tag     Shortcode tag (name). Default empty.
 * @return string Shortcode output.
 */
function wporg_shortcode( $atts = [], $content = null, $tag = '' ) {
  // normalize attribute keys, lowercase
  $atts = array_change_key_case( (array) $atts, CASE_LOWER );

  // override default attributes with user attributes
  $wporg_atts = shortcode_atts(
    array(
      'title' => 'WordPress.org',
    ), $atts, $tag
  );

  // start box
  $o = '<div class="wporg-box">';

  // title
  $o .= '<h2>' . esc_html( $wporg_atts['title'] ) . '</h2>';

  // enclosing tags
  if ( ! is_null( $content ) ) {
    // $content here holds everything in between the opening and the closing tags of your shortcode. eg.g [my-shortcode]content[/my-shortcode].
    // Depending on what your shortcode supports, you will parse and append the content to your output in different ways.
    // In this example, we just secure output by executing the_content filter hook on $content.
    $o .= apply_filters( 'the_content', $content );
  }

  // end box
  $o .= '</div>';

  // return output
  return $o;
}

/**
 * Central location to create all shortcodes.
 */
function wporg_shortcodes_init() {
  add_shortcode( 'wporg', 'wporg_shortcode' );
}

add_action( 'init', 'wporg_shortcodes_init' );
```