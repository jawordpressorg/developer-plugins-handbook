<!-- 
# How to Internationalize Your Plugin
 -->
# プラグインを国際化する方法

<!-- 
In order to make a string translatable in your application you have to wrap the original string in a call to one of a set of special functions. These functions collectively are known as "gettext".
 -->
アプリケーションで文字列を翻訳可能にするには、原文の文字列を特殊な関数の呼び出しでラップする必要があります。これらの関数を総称して「gettext」と呼びます。

<!-- 
## Introduction to Gettext
 -->
## Gettext の紹介

<!-- 
WordPress uses the [gettext](https://www.gnu.org/software/gettext/) libraries and tools for i18n, but not directly: there are a set of special functions created just for the purpose of enabling string translation. These functions are listed below. These are the functions you should use within your plugin.
 -->
WordPress は国際化のために [gettext](https://www.gnu.org/software/gettext/) ライブラリとツールを使用しますが、直接的には使用しません: 文字列の翻訳を可能にするためだけに作られた特別な関数のセットがあります。これらの関数を以下に示します。これらはプラグインで使うべき関数です。

<!-- 
For a deeper dive into gettext, read the [gettext online manual](https://www.gnu.org/software/gettext/manual/html_node/).
 -->
gettext をもっと深く知りたい人は、[gettext オンラインマニュアル](https://www.gnu.org/software/gettext/manual/html_node/)をお読みください。

<!-- 
## Text Domains
 -->
## テキスト・ドメイン

<!-- 
Use a _text domain_ to denote all text belonging to your plugin. The text domain is a unique identifier to ensure WordPress can distinguish between all loaded translations. This increases portability and plays better with already existing WordPress tools.
 -->
プラグインに属するすべてのテキストを示すために「テキスト・ドメイン」を使用してください。テキスト・ドメインとは、WordPress がすべての読み込まれた翻訳を区別できる様にするための一意の識別子です。これにより、移植性が向上し、既存の WordPress ツールとの相性も良くなります。

<!-- 
The text domain must match the `slug` of the plugin. If your plugin is a single file called `my-plugin.php` or it is contained in a folder called `my-plugin` the domain name must be `my-plugin`. If your plugin is hosted on wordpress.org it must be the slug portion of your plugin URL (`wordpress.org/plugins/my-plugin`).
 -->
テキスト・ドメインは、プラグインの `スラッグ` と一致しなければなりません。プラグインが `my-plugin.php` という単一のファイルであるか、`my-plugin` というフォルダーに含まれている場合、ドメイン名は `my-plugin` でなければなりません。プラグインが wordpress.org でホストされている場合は、プラグイン URL のスラッグ部分 (`wordpress.org/plugins/my-plugin`) でなければなりません。

<!-- 
The text domain name must use dashes and not underscores, be lower case, and have no spaces.
 -->
テキスト・ドメイン名は、アンダースコアではなくダッシュを使用し、小文字で、スペースを含まないものでなければなりません。

<!-- 
The text domain also needs to be added to the plugin header. WordPress uses it to internationalize your plugin metadata even when the plugin is disabled. The text domain should be same as the one used when [loading the text domain](https://developer.wordpress.org/plugins/internationalization/how-to-internationalize-your-plugin/#loading-text-domain).
 -->
テキスト・ドメインも、プラグインヘッダーに追加する必要があります。WordPress は、プラグインが無効になっている場合でも、プラグインのメタデータを国際化するためにこれを使用します。テキスト・ドメインは、[テキスト・ドメインを読み込む](https://developer.wordpress.org/plugins/internationalization/how-to-internationalize-your-plugin/#loading-text-domain)ときに使用したものと同じでなければなりません。

<!-- 
### Header example
 -->
### ヘッダー例

```
/* 
 * Plugin Name: My Plugin
 * Author: Plugin Author
 * Text Domain: my-plugin
 */
```

<!-- 
[info]Again, change "my-plugin" to the slug of your plugin.[/info]
 -->
[info]もう一度、"my-plugin" をプラグインのスラッグに変更します。[/info]

<!-- 
[info]Since WordPress 4.6 the `Text Domain` header is optional because it must be the same as the plugin slug. There is no harm in including it, but it is not required.[/info]
 -->
[info]WordPress 4.6以降、`Text Domain` ヘッダーはプラグインのスラッグと同じでなければならないため、省略可能です。含めても害はありませんが、必須ではありません。[/info]

<!-- 
## Domain Path
 -->
## ドメイン・パス

<!-- 
The domain path defines the location for a plugin's translation. This has a few uses, notably so that WordPress knows where to find the translation even when the plugin is disabled. This defaults to the folder in which your plugin is found.
 -->
ドメイン・パスは、プラグインの翻訳の場所を定義します。これにはいくつかの使い道があり、特にプラグインが無効になっているときでも WordPress が翻訳の場所を知っている様にします。デフォルトは、プラグインがあるフォルダーです。

<!-- 
For example, if the translation is located in a folder called `languages` within your plugin, then the Domain Path is `/languages` and must be written with the first slash:
 -->
たとえば、翻訳がプラグイン内の `languages` というフォルダーにある場合、ドメイン・パスは `/languages` となり、最初のスラッシュと一緒に記述する必要があります:

<!-- 
### Header example
 -->
### ヘッダー例

```
/*
 * Plugin Name: My Plugin
 * Author: Plugin Author
 * Text Domain: my-plugin
 * Domain Path: /languages
 */
```

<!-- 
[info]The `Domain Path` header can be omitted if the plugin is in the official WordPress Plugin Directory.[/info]
 -->
[info]プラグインが公式 WordPress プラグインディレクトリにある場合、`Domain Path` ヘッダーは省略できます。[/info]

<!-- 
## Basic strings
 -->
## 基本文字列

<!-- 
For basic strings (meaning strings without placeholders or plurals) use [`__()`](https://developer.wordpress.org/reference/functions/__/). It returns the translation of its argument:
 -->
基本文字列 (プレースホルダーや複数形のない文字列のこと) には、[`__()`](https://developer.wordpress.org/reference/functions/__/) を使います。これは引数の翻訳を返します:

```
__( 'Blog Options', 'my-plugin' );
```

<!-- 
[warning]Do not use variable names or constants for the text domain portion of a gettext function. For example: Do not do this as a shortcut:

`__( 'Translate me.' , $text_domain );`[/warning]
 -->
[warning]gettext 関数のテキスト・ドメイン部分には、変数名や定数を使用しないでください。たとえば: ショートカットとしてこれを使用しないでください:

`__( 'Translate me.' , $text_domain );`[/warning]

<!-- 
To echo a retrieved tranlsation, use [`_e()`](https://developer.wordpress.org/reference/functions/_e/). So instead of writing:
 -->
取得した翻訳を出力するには、[`_e()`](https://developer.wordpress.org/reference/functions/_e/) を使います。つまり、以下のように書く代わりに:

```
echo __( 'WordPress is the best!', 'my-plugin' );
```

<!-- 
you can use:
 -->
以下のように、書くことができます:

```
_e( 'WordPress is the best!', 'my-plugin' );
```

<!-- 
## Variables
 -->
## 変数

<!-- 
What if you have a string like the following:
 -->
もし次のような文字列があったら、どうでしょう:

```
echo 'Your city is $city.'
```

<!-- 
In this case, the `$city` is a variable and should not be part of the translation. The solution is to use placeholders for the variable, along with the `printf` family of functions. Especially helpful are [`printf`](https://www.php.net/manual/en/function.printf.php) and [`sprintf`](https://www.php.net/manual/en/function.sprintf). Here is what the right solution looks like:
 -->
この場合、`$city` は変数であり、翻訳の一部であってはなりません。解決策としては、関数の `printf` ファミリーとともに変数のプレースホルダーを使うことです。特に便利なのは [`printf`](https://www.php.net/manual/en/function.printf.php) と [`sprintf`](https://www.php.net/manual/en/function.sprintf) です。これが適切な解決方法です:

```
printf(
  /* translators: %s: Name of a city */
  __( 'Your city is %s.', 'my-plugin' ),
  $city
);
```

<!-- 
Notice that here the string for translation is just the template `"Your city is %s."`, which is the same both in the source and at run-time.
 -->
ここでは、翻訳のための文字列はテンプレート `"Your city is %s."` だけであり、ソースでもランタイムでも同じであることに注意してください。

<!-- 
Also note that there is a hint for translators so that they know the context of the placeholder.
 -->
また、翻訳者がプレースホルダーの文脈を知るためのヒントもあります。

<!-- 
If you have more than one placeholder in a string, it is recommended that you use [argument swapping](http://www.php.net/manual/en/function.sprintf.php). In this case, single quotes (`'`) around the string are mandatory because double quotes (`"`) will tell php to interpret the `$s` as the `s` variable, which is not what we want.
 -->
文字列内に複数のプレースホルダーがある場合は、[引数の入れ替え](http://www.php.net/manual/en/function.sprintf.php) を使用することを推奨します。この場合、文字列をシングルクオート (`'`) で囲むことが必須で、ダブルクオート (`"`) を使用すると、php が `$s` を変数 `s` として解釈してしまうからです。

```
printf(
  /* translators: 1: Name of a city 2: ZIP code */
  __( 'Your city is %1$s, and your zip code is %2$s.', 'my-plugin' ),
  $city,
  $zipcode
);
```

<!-- 
Here the zip code is being displayed after the city name. In some languages displaying the zip code and city in opposite order would be more appropriate. Using %s prefix in the above example, allows for such a case. A translation can thereby be written:
 -->
ここでは、郵便番号が都市名の後に表示されています。言語によっては、郵便番号と都市名を逆の順序で表示するほうが適切な場合もあります。上の例で接頭辞 %s を使うことで、そのようなケースに対応できます。これにより、翻訳は次のように書くことができます:

```
printf(
  /* translators: 1: Name of a city 2: ZIP code */
  __( 'Your zip code is %2$s, and your city is %1$s.', 'my-plugin' ),
  $city,
  $zipcode
);
```

<!-- 
**Important!** The following code is incorrect:
 -->
**重要 !** 以下のコードは間違っています:

```
// This is incorrect do not use.
_e( "Your city is $city.", 'my-plugin' );
```

<!-- 
The strings for translation are extracted from the sources, so the translators will get this phrase to translate: `"Your city is $city."`.
 -->
翻訳用の文字列はソースから抽出されるので、翻訳者はこのフレーズを翻訳することになります: `"Your city is $city."`。

<!-- 
However in the application `_e` will be called with an argument like `"Your city is London."` and `gettext` won't find a suitable translation of this one and will return its argument: `"Your city is London."`. Unfortunately, it isn't translated correctly.
 -->
しかし、アプリケーションでは `_e` は `"Your city is London."` のような引数で呼び出され、`gettext` はこの引数の適切な翻訳を見つけられず、引数 `"Your city is London."` を返します。残念ながら、これは正しく翻訳されていません。

<!-- 
## Plurals
 -->
## 複数形

<!-- 
### Basic Pluralization
 -->
### 基本的な複数形化

<!-- 
If you have string that changes when the number of items changes, you'll need a way to reflect this in your translations. For example, in English you have `"One comment"` and `"Two comments"`. In other languages you can have multiple plural forms. To handle this in WordPress use the [`_n()`](https://developer.wordpress.org/reference/functions/_n/) function.
 -->
アイテム数が変わると変化する文字列がある場合、翻訳に反映させる方法が必要になります。たとえば、英語では `"One comment"` と `"Two comments"` があります。他の言語では複数の複数形があります。WordPress でこれを処理するには、[`_n()`](https://developer.wordpress.org/reference/functions/_n/) 関数を使います。

```
printf(
  _n(
    '%s comment',
    '%s comments',
    get_comments_number(),
    'my-plugin'
  ),
  number_format_i18n( get_comments_number() )
);
```

<!-- 
`_n()` accepts 4 arguments:
 -->
`_n()` は4つの引数を受け付けます:

<!-- 
- singular – the singular form of the string (note that it can be used for numbers other than one in some languages, so `'%s item'` should be used instead of `'One item'`).
- plural – the plural form of the string.
- count – the number of objects, which will determine whether the singular or the plural form should be returned (there are languages, which have far more than 2 forms).
- text domain – the plugins text domain.
 -->
- singular – 文字列の単数形 (言語によっては1以外の数にも使えるので、`'One item'` の代わりに `'%s item'` を使うべきであることに注意)。
- plural – 文字列の複数形。
- count – 単数形と複数形のどちらを返すかを決定する、オブジェクトの数 (2つ以上の形式を持つ言語もあります)。
- text domain – プラグインのテキスト・ドメイン。

<!-- 
The return value of the functions is the correct translated form, corresponding to the given count.
 -->
関数の戻り値は、与えられた数に対応する正しい翻訳形です。

<!-- 
Note that some languages use the singular form for other numbers (e.g. 21, 31 and so on, much like '21st', '31st' in English). If you would like to special case the singular, check for it specifically:
 -->
言語によっては、他の数に単数形を使うものもあります (たとえば、英語の「21st」や「31st」のように、21、31など)。単数形を特別扱いしたい場合は、特に確認してください:

```
if ( 1 === $count ) {
  printf( esc_html__( 'Last thing!', 'my-text-domain' ), $count );
} else {
  printf( esc_html( _n( '%d thing.', '%d things.', $count, 'my-text-domain' ) ), $count );
}
```

<!-- 
Also note that the `$count` parameter is often used twice. First `$count` is passed to `_n()` to determine which translated string to use, and then `$count` is passed to `printf()` to substitute the number into the translated string.
 -->
また、パラメータ `$count` は、しばしば2回使用されることに注意してください。まず `$count` を `_n()` に渡して、どの翻訳文字列を使うかを決定し、続いて `$count` を `printf()` に渡して、翻訳文字列に数値を代入します。

<!-- 
### Pluralization done later
 -->
### 後で行われる複数形化

<!-- 
You first set the plural strings with [`_n_noop()`](https://developer.wordpress.org/reference/functions/_n_noop/) or [`_nx_noop()`](https://developer.wordpress.org/reference/functions/_nx_noop/).
 -->
まず [`_n_noop()`](https://developer.wordpress.org/reference/functions/_n_noop/) または [`_nx_noop()`](https://developer.wordpress.org/reference/functions/_nx_noop/) で複数の文字列を設定します。

```
$comments_plural = _n_noop(
  '%s comment.',
  '%s comments.'
);
```

<!-- 
Then at a later point in the code you can use [`translate_nooped_plural()`](https://developer.wordpress.org/reference/functions/translate_nooped_plural/) to load the strings.
 -->
続いてコードの後の方で、[`translate_nooped_plural()`](https://developer.wordpress.org/reference/functions/translate_nooped_plural/) を使って文字列を読み込むことができます。

```
printf(
  translate_nooped_plural(
    $comments_plural,
    get_comments_number(),
    'my-plugin'
  ),
  number_format_i18n( get_comments_number() )
);
```

<!-- 
## Disambiguation by context
 -->
## context によるあいまいさ回避

<!-- 
Sometimes one term is used in several contexts and although it is one and the same word in English it has to be translated differently in other languages. For example the word `Post` can be used both as a verb `"Click here to post your comment"` and as a noun `"Edit this post"`. In such cases the `_x()` or `_ex()` function should be used. It is similar to `__()` and `_e()`, but it has an additional argument — the context:
 -->
一つの単語が複数の文脈で使われることがあり、英語では一つの同じ単語であっても、他の言語では異なる翻訳をしなければならないことがあります。たとえば、`Post` という単語は、動詞 `"Click here to post your comment"` としても、名詞 `"Edit this post"` としても使えます。このような場合は `_x()` または `_ex()` 関数を使用します。これは `__()` や `_e()` と似ているが、追加の引数 — コンテキスト — があります:

```
_x( 'Post', 'noun', 'my-plugin' );
_x( 'Post', 'verb', 'my-plugin' );
```

<!-- 
Using this method in both cases we will get the string Comment for the original version, but the translators will see two Comment strings for translation, each in the different contexts.
 -->
両方のケースでこの方法を使うと、原文の文字列 Comment は得られますが、翻訳者には翻訳用の2つの Comment 文字列が、それぞれ異なる文脈で表示されることになります。

<!-- 
Note that similarly to `__()`, `_x()` has an `echo` version: `_ex()`. The previous example could be written as:
 -->
`__()` と同様に、`_x()` にも `echo` 版があることに注意してください: `_ex()` です。前の例は次のように書けます:

```
_ex( 'Post', 'noun', 'my-plugin' );
_ex( 'Post', 'verb', 'my-plugin' );
```

<!-- 
Use whichever you feel enhances legibility and ease-of-coding.
 -->
読みやすさとコーディングのしやすさを高めるとあなたが思うほうを使いましょう。

<!-- 
## Descriptions
 -->
## 説明

<!-- 
So that translators know how to translate a string like `__( 'g:i:s a' )` you can add a clarifying comment in the source code. It has to start with the words `translators:` and to be the last PHP comment before the gettext call. Here is an example:
 -->
翻訳者が `__( 'g:i:s a' )` のような文字列をどのように翻訳すればよいのかわかる様に、ソースコードに明確なコメントを追加できます。これは gettext 呼び出しの直前に、単語 `translators:` で始まる、PHP コメントでなければなりません。以下に例を示します:

```
/* translators: draft saved date format, see http://php.net/date */
$saved_date_format = __( 'g:i:s a' );
```

<!-- 
It's also used to explain placeholders in a string like `_n_noop( '<strong>Version %1$s</strong> addressed %2$s bug.','<strong>Version %1$s</strong> addressed %2$s bugs.' )`.
 -->
また、`_n_noop( '<strong>Version %1$s</strong> addressed %2$s bug.', '<strong>Version %1$s</strong> addressed %2$s bugs.' )` のように、文字列のプレースホルダーを説明するためにも使われます。

```
/* translators: 1: WordPress version number, 2: plural number of bugs. */
_n_noop( '<strong>Version %1$s</strong> addressed %2$s bug.','<strong>Version %1$s</strong>strong> addressed %2$s bugs.' );
```

<!-- 
## Newline characters
 -->
## 改行文字

<!-- 
Gettext doesn't like `r` (ASCII code: 13) in translatable strings, so please avoid it and use `n` instead.
 -->
Gettext は、翻訳対象の文字列内に `r` (ASCII コード: 13) を好まないので、これを避けて代わりに `n` を使ってください。

<!-- 
## Empty strings
 -->
## 空文字列

<!-- 
The empty string is reserved for internal Gettext usage and you must not try to internationalize the empty string. It also doesn't make any sense, because the translators won't see any context.
 -->
空文字列は、Gettext 内部で使用するために予約されているので、空文字列を国際化しようとしてはいけません。また、翻訳者はコンテキストを確認しないので、意味がありません。

<!-- 
If you have a valid use-case to internationalize an empty string, add context to both help translators and be in peace with the Gettext system.
 -->
空文字列を国際化する正当なユースケースがある場合は、翻訳者を助けると同時に Gettext システムと共存するためにコンテキストを追加します。

<!-- 
## Escaping strings
 -->
## エスケープ文字列

<!-- 
It is good to escape all of your strings, this way the translators cannot run malicious code. There are a few escape functions that are integrated with internationalization functions.
 -->
すべての文字列をエスケープしておくと、翻訳者が悪意あるコードを実行することはありません。国際化関数と統合されたエスケープ関数がいくつかあります。

<!-- 
## Localization functions
 -->
## ローカライゼーション関数

<!-- 
### Basic functions
 -->
### 基本関数

- [`__()`](https://developer.wordpress.org/reference/functions/__/)
- [`_e()`](https://developer.wordpress.org/reference/functions/_e/)
- [`_x()`](https://developer.wordpress.org/reference/functions/_x/)
- [`_ex()`](https://developer.wordpress.org/reference/functions/_ex/)
- [`_n()`](https://developer.wordpress.org/reference/functions/_n/)
- [`_nx()`](https://developer.wordpress.org/reference/functions/_nx/)
- [`_n_noop()`](https://developer.wordpress.org/reference/functions/_n_noop/)
- [`_nx_noop()`](https://developer.wordpress.org/reference/functions/_nx_noop/)
- [`translate_nooped_plural()`](https://developer.wordpress.org/reference/functions/translate_nooped_plural/)

<!-- 
### Translate & Escape functions 
 -->
### 翻訳とエスケープ関数

<!-- 
Strings that require translation and is used in attributes of html tags must be escaped.
 -->
翻訳が必要な文字列や、html タグの属性で使用されている文字列は、エスケープする必要があります。

- [`esc_html__()`](https://developer.wordpress.org/reference/functions/esc_html__/)
- [`esc_html_e()`](https://developer.wordpress.org/reference/functions/esc_html_e/)
- [`esc_html_x()`](https://developer.wordpress.org/reference/functions/esc_html_x/)
- [`esc_attr__()`](https://developer.wordpress.org/reference/functions/esc_attr__/)
- [`esc_attr_e()`](https://developer.wordpress.org/reference/functions/esc_attr_e/)
- [`esc_attr_x()`](https://developer.wordpress.org/reference/functions/esc_attr_x/)

<!-- 
### Date and number functions
 -->
### 日付および数値関数

- [`number_format_i18n()`](https://developer.wordpress.org/reference/functions/number_format_i18n/)
- [`date_i18n()`](https://developer.wordpress.org/reference/functions/date_i18n/)

<!-- 
## Best Practices for writing strings
 -->
## 文字列の書き方のベストプラクティス

<!-- 
Here are the best practices for writing strings
 -->
文字列を書く際のベスト・プラクティスは、以下のようになります。

<!-- 
- Use decent English style – minimize slang and abbreviations.
- Use entire sentences – in most languages word order is different than that in English.
- Split at paragraphs – merge related sentences, but do not include a whole page of text in one string.
- Do not leave leading or trailing whitespace in a translatable phrase.
- Assume strings can double in length when translated.
- Avoid unusual markup and unusual control characters – do not include tags that surround your text.
- Do not put unnecessary HTML markup into the translated string.
- Do not leave URLs for translation, unless they could have a version in another language.
- Add the variables as placeholders to the string as in some languages the placeholders change position.
 -->
- 適切な英語スタイルを使用する – スラングや略語は最小限にとどめましょう.
- 文章全体を使う – ほとんどの言語では、語順は英語とは異なります。
- 段落を分ける – 関連する文章を一つにまとめるが、1ページ分の文章を一つの文字列に含めないでください。
- 翻訳可能なフレーズの先頭や末尾に、空白を残さないようにしましょう。
- 文字列は、翻訳されると2倍の長さになる可能性があります。
- 変則的なマークアップや 変則的な制御文字を避ける – テキストを囲むタグを含めないでください。
- 翻訳された文字列に不必要な HTML マークアップを入れないでください。
- 他の言語のバージョンがある場合を除き、URL は翻訳用に含めないでください。
- 言語によってはプレースホルダーの位置が変わるので、文字列にプレースホルダーとして変数を追加する様にしてください。

```
printf(
  __( 'Search results for: %s', 'my-plugin' ),
  get_search_query()
);
```

<!-- 
- Use format strings instead of string concatenation – translate phrases and not words – `printf( __( 'Your city is %1$s, and your zip code is %2$s.', 'my-plugin' ), $city, $zipcode );` is always better than: `__( 'Your city is ', 'my-plugin' ) . $city . __( ', and your zip code is ', 'my-plugin' ) . $zipcode;`.
- Try to use the same words and same symbols so not multiple strings needs to be translated e.g. `__( 'Posts:', 'my-plugin' );` and `__( 'Posts', 'my-plugin' );`.
 -->
- 文字列連結の代わりにフォーマット文字列を使用する – 単語ではなくフレーズを翻訳する – `printf( __( 'Your city is %1$s, and your zip code is %2$s.', 'my-plugin' ), $city, $zipcode );` は `__( 'Your city is ', 'my-plugin' ) . $city . __( ', and your zip code is ', 'my-plugin' ) . $zipcode;` より優れています。
- `__( 'Posts:', 'my-plugin' );` と `__( 'Posts', 'my-plugin' );` のように、複数の文字列を翻訳する必要がない様、同じ単語と同じ記号を使う様にしてください。

<!-- 
### Add Text Domain to strings
 -->
### 文字列へのテキスト・ドメインの追加

<!-- 
You must add your Text domain as an argument to every `__()`, `_e()` and `__n()` gettext call, or your translations won't work.
 -->
`__()`、`_e()`、`__n()` の gettext 呼び出しの引数として、テキスト・ドメインを追加する必要があり、さもないと翻訳が正常に機能しません。

<!-- 
Examples:
 -->
例:

<!-- 
- `__( 'Post' )` should become `__( 'Post', 'my-theme' )`.
- `_e( 'Post' )` should become `_e( 'Post', 'my-theme' )`.
- `_n( '%s post', '%s posts', $count )` should become `_n( '%s post', '%s posts', $count, 'my-theme' )`.
 -->
- `__( 'Post' )` は `__( 'Post', 'my-theme' )` になるはずです。
- `_e( 'Post' )` は `_e( 'Post', 'my-theme' )` になるはずです。
- `_n( '%s post', '%s posts', $count )` は `_n( '%s post', '%s posts', $count, 'my-theme' )` になるはずです。

<!-- 
If there are strings in your plugin that are also used in WordPress core (e.g. 'Settings'), you should still add your own text domain to them, otherwise they'll become untranslated if the core string changes (which happens).
 -->
WordPress のコア (例: 設定) でも使用されている文字列がプラグインにある場合でも、独自のテキストドメインを追加する必要があり、そうしないと、コアの文字列が変更された場合 (これはよくあること)、翻訳されなくなります。

<!-- 
Adding the text domain by hand can be a burden if not done continuously when writing code and that's why you can do it automatically:
 -->
コードを書くとき、手作業でテキスト・ドメインを追加するのは、継続して行わなければ重荷になりかねないからこそ、自動的に行うことができるのです:

<!-- 
- Download the [`add-textdomain.php`](https://develop.svn.wordpress.org/branches/5.2/tools/i18n/add-textdomain.php) script to the folder where the file is you want to add the text domain
- In command line move to the directory where the file is.
- Run this command to create a new file with the text domain added:
 -->
- テキスト・ドメインを追加したいファイルがあるフォルダーに、スクリプト [`add-textdomain.php`](https://develop.svn.wordpress.org/branches/5.2/tools/i18n/add-textdomain.php) をダウンロードします。
- コマンドラインで、ファイルのあるディレクトリに移動します。
- このコマンドを実行すると、テキスト・ドメインが追加された新しいファイルが作成されます:

```
php add-textdomain.php my-plugin my-plugin.php > new-my-plugin.php
```

<!-- 
If you wish to have the `add-textdomain.php` in a different folder you just need to define the location in the command.
 -->
`add-textdomain.php` を別のフォルダーに置きたい場合は、コマンドで場所を定義するだけです。

```
php /path/to/add-textdomain.php my-plugin my-plugin.php > new-my-plugin.php
```

<!-- 
Use this command if you don't want a new file outputted:
 -->
新しいファイルを出力したくない場合は、このコマンドを使います:

```
php add-textdomain.php -i my-plugin my-plugin.php
```

<!-- 
If you want to change multiple files in a directory you can also pass a directory to the script:
 -->
ディレクトリ内の複数のファイルを変更したい場合は、スクリプトにディレクトリを渡すこともできます:

```
php add-textdomain.php -i my-plugin my-plugin-directory
```

<!-- 
After it's done, the text domain will be added to the end of all gettext calls in the file. If there is an existing text domain it will not be replaced.
 -->
これが終わると、ファイル内のすべての gettext 呼び出しの最後にテキスト・ドメインが追加されます。既存のテキスト・ドメインがある場合は、置き換えられません。

<!-- 
## Loading Text Domain
 -->
## テキスト・ドメインの読み込み

<!-- 
Translations can be loaded using `load_plugin_textdomain`, for example:
 -->
たとえば、翻訳は、`load_plugin_textdomain` を使って読み込むことができます:

```
add_action( 'init', 'wpdocs_load_textdomain' );

function wpdocs_load_textdomain() {
  load_plugin_textdomain( 'wpdocs_textdomain', false, dirname( plugin_basename( __FILE__ ) ) . '/languages' );
}
```

<!-- 
## Plugins on WordPress.org
 -->
## WordPress.org のプラグイン

<!-- 
[info]Since WordPress 4.6 translations now take [translate.wordpress.org](https://translate.wordpress.org/) as priority and so plugins that are translated via translate.wordpress.org do not necessary require `load_plugin_textdomain()` anymore. If you don't want to add a `load_plugin_textdomain()` call to your plugin you have to set the `Requires at least:` field in your readme.txt to 4.6 or more.[/info]
 -->
[info]WordPress 4.6以降、翻訳は [translate.wordpress.org](https://translate.wordpress.org/) を優先するようになったので、translate.wordpress.org 経由で翻訳されるプラグインは `load_plugin_textdomain()` を必要としなくなりました。プラグインに `load_plugin_textdomain()` 呼び出しを追加したくない場合は、readme.txt の `Requires at least:` フィールドを4.6以上に設定する必要があります。[/info]

<!-- 
If you still want to load your own translations and not the ones from translate, you will have to use a hook filter named `load_textdomain_mofile`.  
 -->
translate からではなく、自分の翻訳をロードしたい場合は、`load_textdomain_mofile` というフックフィルターを使う必要があります。
<!-- 
**Example** with a .mo file in the `/languages/` directory of your plugin, with this code inserted in the main plugin file:
 -->
**例** プラグインの `/languages/` ディレクトリに .mo ファイルを作成し、メインのプラグインファイルに、このコードを挿入します:

```
function my_plugin_load_my_own_textdomain( $mofile, $domain ) {
  if ( 'my-domain' === $domain && false !== strpos( $mofile, WP_LANG_DIR . '/plugins/' ) ) {
    $locale = apply_filters( 'plugin_locale', determine_locale(), $domain );
    $mofile = WP_PLUGIN_DIR . '/' . dirname( plugin_basename( __FILE__ ) ) . '/languages/' . $domain . '-' . $locale . '.mo';
  }
  return $mofile;
}
add_filter( 'load_textdomain_mofile', 'my_plugin_load_my_own_textdomain', 10, 2 );
```

<!-- 
## Handling JavaScript files
 -->
## JavaScript ファイルの取り扱い

<!-- 
Check the [Internationalizing javascript](https://developer.wordpress.org/apis/internationalization/#internationalizing-javascript) section of the [Common APIs Handbook](https://developer.wordpress.org/apis/) to see how to properly load your translation files. There is also the [Gutenburg plugin docs page](https://github.com/WordPress/gutenberg/blob/trunk/docs/how-to-guides/internationalization.md).
 -->
[共通 API ハンドブック](https://developer.wordpress.org/apis/) の [javascript の国際化](https://developer.wordpress.org/apis/internationalization/#internationalizing-javascript) セクションをチェックして、翻訳ファイルを正しく読み込む方法を確認してください。[Gutenburg プラグインのドキュメントページ](https://github.com/WordPress/gutenberg/blob/trunk/docs/how-to-guides/internationalization.md)もあります。

<!-- 
## Language Packs
 -->
## 言語パック

<!-- 
If you're interested in language packs and how the import to [translate.wordpress.org](https://translate.wordpress.org/) is working, please read the [Meta Handbook page about Translations](https://make.wordpress.org/meta/handbook/tutorials-guides/translations/).
 -->
言語パックや [translate.wordpress.org](https://translate.wordpress.org/) へのインポートに興味があるなら、[翻訳についてのメタハンドブックのページ](https://make.wordpress.org/meta/handbook/tutorials-guides/translations/)を読んでください。

<!-- 
Also refer [Plugin/Theme Authors Guide in Polyglots Handbooks](https://make.wordpress.org/polyglots/handbook/plugin-theme-authors-guide/) for getting your project translated.
 -->
あなたのプロジェクトを翻訳するために [Polyglots ハンドブックのプラグイン/テーマ作者ガイド](https://make.wordpress.org/polyglots/handbook/plugin-theme-authors-guide/)も参照してください。