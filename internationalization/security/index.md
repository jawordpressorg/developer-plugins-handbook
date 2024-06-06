<!-- 
Internationalization Security
 -->
国際化セキュリティ
-----------------------------

<!-- 
Security is often overlooked when talking about internationalization, but there are a few important things to keep in mind.
 -->
国際化について語るとき、セキュリティは見落とされがちだが、留意すべき重要なことがいくつかあります。

<!-- 
## Check for Spam and Other Malicious Strings
 -->
## スパムやその他の悪意ある文字列のチェック

<!-- 
When a translator submits a localization to you, always check to make sure they didn't include spam or other malicious words in their translation. You can use [Google Translate](https://translate.google.com/) to translate their translation back into your native language so that you can easily compare the original and translated strings.
 -->
翻訳者がローカライズを提出する際には、翻訳にスパムやその他の悪意ある単語が含まれていないか、必ず確認してください。原文の文字列と翻訳した文字列を簡単に比較できるように、[Google 翻訳](https://translate.google.com/)を使って翻訳者の翻訳をあなたの母国語に翻訳し直すことができます。

<!-- 
## Escape Internationalized Strings
 -->
## 国際化された文字列のエスケープ

<!-- 
You can't trust that a translator will only add benign text to their localization; if they want to, they could add malicious JavaScript or other code instead. To protect against that, it's important to treat internationalized strings like you would any other untrusted input.
 -->
翻訳者がローカライズに良性のテキストだけを加えるとは限りません ; その気になれば、悪意ある JavaScript やその他のコードを追加することも可能です。そのような事態から守るためには、国際化された文字列を、他の信頼できない入力と同じように扱うことが重要です。

<!-- 
If you're outputting the strings, then they should be escaped.
 -->
文字列を出力するのであれば、エスケープすべきです。

<!-- 
**Insecure**
 -->
**危険**

```
_e( 'The REST API content endpoints were added in WordPress 4.7.', 'your-text-domain' );
```

<!-- 
**Secure**
 -->
**安全**

```
esc_html_e( 'The REST API content endpoints were added in WordPress 4.7.', 'your-text-domain' );
```

<!-- 
Alternatively, some people choose to rely on a translation verification mechanism, rather than adding escaping to their code. One example of a verification mechanism is [the editor roles](https://make.wordpress.org/polyglots/handbook/glossary/#project-translation-editor) that the WordPress Polyglots team uses for [translate.wordpress.org](https://translate.wordpress.org/). This ensures that any translation submitted by an untrusted contributor has been verified by a trusted editor before being accepted.
 -->
もしくは、コードにエスケープを追加するのではなく、翻訳検証メカニズムに依存することを選択する人もいます。検証メカニズムの一例として、WordPress Polyglots チームが [translate.wordpress.org](https://translate.wordpress.org/) で使用している[エディターの役割](https://make.wordpress.org/polyglots/handbook/glossary/#project-translation-editor)があります。これにより、信頼されていないコントリビューターによって投稿された翻訳が受理される前に、信頼されたエディターによって検証されることが保証されます。

<!-- 
## Use Placeholders for URLs
 -->
## URL にプレースホルダーの使用

<!-- 
Don't include URLs in internationalized strings, because a malicious translator could change them to point to a different URL. Instead, use placeholders for [`printf()`](https://www.php.net/manual/en/function.printf.php) or [`sprintf()`](https://www.php.net/manual/en/function.sprintf.php).
 -->
悪意ある翻訳者が、別の URL を指すように変えてしまう可能性があるから、国際化された文字列には URL を含めないでください。代わりに、[`printf()`](https://www.php.net/manual/en/function.printf.php) または [`sprintf()`](https://www.php.net/manual/en/function.sprintf.php) のプレースホルダを使用してください。

<!-- 
**Insecure**
 -->
**危険**

```
_e(
  'Please <a href="https://login.wordpress.org/register"> register for a WordPress.org account</a>.',
  'your-text-domain'
);
```

<!-- 
**Secure**
 -->
**安全**

```
printf(
  esc_html__( 'Please %1$s register for a WordPress.org account %2$s.', 'your-text-domain' ),
  '<a href="https://login.wordpress.org/register">',
  '</a>'
);
```

<!-- 
## Compile Your Own .mo Binaries
 -->
## 独自 .mo バイナリーのコンパイル

<!-- 
Often translators will send the compiled .mo file along with the plaintext .po file, but you should discard their .mo file and compile your own, because you have no way of knowing whether or not it was compiled from the corresponding .po file, or a different one. If it was compiled against a different one, then it could contain spam and other malicious strings without your knowledge.
 -->
しばしば、翻訳者はコンパイルした .mo ファイルをプレーンテキストの .po ファイルと一緒に送って来るが、その .mo ファイルが対応する .po ファイルからコンパイルされたものなのか、それとも別のものなのかを知る術がないから、その .mo ファイルは捨てて、自分でコンパイルすべきです。それが別のものに対してコンパイルされたものであれば、あなたの知らないうちにスパムやその他の悪意ある文字列が含まれている可能性があります。

<!-- 
Using PoEdit to generate the binary will override the headers in the .po file, so instead it's better to compile it from the command line:
 -->
PoEdit を使ってバイナリーを生成すると、.po ファイルのヘッダが上書きされてしまうので、コマンドラインからコンパイルする方が良いです :

```
msgfmt -cv -o /path/to/output.mo /path/to/input.po
```