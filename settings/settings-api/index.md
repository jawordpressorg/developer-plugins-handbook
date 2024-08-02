<!-- 
# Settings API
 -->
# 設定 API

<!-- 
The Settings API, added in WordPress 2.7, allows admin pages containing settings forms to be managed semi-automatically. It lets you define settings pages, sections within those pages and fields within the sections.
 -->
WordPress 2.7で追加された設定 API により、半自動的な管理が可能な設定フォームを管理ページに追加でききるようになりました。設定ページ、ページ内のセクション、セクション内のフィールドを定義できます。

<!-- 
New settings pages can be registered along with sections and fields inside them. Existing settings pages can also be added to by registering new settings sections or fields inside of them.
 -->
新しい設定ページを、その中のセクションやフィールドとともに登録できます。既存の設定ページも、その中に新しい設定セクションやフィールドを登録することで追加できます。

<!-- 
Organizing registration and validation of fields still requires some effort from developers, but avoids a lot of complex debugging of underlying options management.
 -->
フィールドの登録と検証を行うには、開発者の労力が必要ですが、オプション管理のための複雑なデバッグの手間を省くことができます。

<!-- 
[alert]When using the Settings API, the form POST to `wp-admin/options.php` which provides fairly strict capabilities checking. Users will need the `manage_options` capability (and in Multisite will have to be a Super Admin) to submit the form.[/alert]
 -->
[alert]設定 API を使用する場合、フォームは、かなり厳密な機能チェックを提供する `wp-admin/options.php` に POST します。ユーザーがフォームを送信するには `manage_options` 権限が必要です (マルチサイト環境では、特権管理者である必要があります)。[/alert]

<!-- 
## Why Use the Setting API?
 -->
## 設定 API を使うのはなぜ ?

<!-- 
A developer _could_ ignore this API and write their own settings page without it. That begs the question, what benefit does this API bring to the table? Following is a quick rundown of some of the benefits.
 -->
開発者はこの API を無視して、API なしで独自の設定ページを書くことは _可能_ です。では、この API はどのような利点をもたらすのでしょう ? 以下は、いくつかの利点の簡単な概要です。

<!-- 
### Visual Consistency
 -->
### 視覚的な一貫性

<!-- 
Using the API to generate your interface elements guarantees that your settings page will look like the rest of the administrative content. Your interface will follow the same styleguide and look like it belongs, and thanks to the talented team of WordPress designers, it'll look awesome!
 -->
API を使ってインターフェース要素を生成すれば、設定ページが他の管理コンテンツと同じように見えることが保証されます。あなたのインターフェースは同じスタイルガイドに従い、WordPress デザイナーの才能あるチームのおかげですばらしいものになるでしょう !

<!-- 
### Robustness (Future-Proofing!)
 -->
### 堅牢性 (将来への備え !)

<!-- 
Since the API is part of WordPress Core, any updates will automatically consider your plugin's settings page. If you make your own interface without using Setting API, WordPress Core updates are more likely to break your customizations. There is also a wider audience testing and maintaining that API code, so it will tend to be more stable.
 -->
API は WordPress Core の一部ですので、アップデートがあればプラグインの設定ページが自動的に考慮されます。設定 API を使わずに独自のインターフェイスを作成した場合、WordPress Core のアップデートによってカスタマイズが壊れる可能性が高くなります。また、その API コードをテストし、保守している多くのユーザーがいるため、より安定している傾向があります。

<!-- 
### Less Work!
 -->
### 仕事が減る !

<!-- 
Of course the most immediate benefit is that the WordPress API does a lot of work for you under the hood. Here are a few examples of things the Settings API does besides applying an awesome-looking, integrated design.
 -->
もちろん、最も直接的な利点は、WordPress API があなたに代わって多くの作業を肩代わりすることです。以下は、設定 API がすばらしい外観と統合されたデザインを適用する以外に行うことのいくつかの例です。

<!-- 
- **Handling Form Submissions**: Let WordPress handle retrieving and storing your `$_POST` submissions.
- **Include Security Measures**: You get extra security measures such as nonces, etc. for free.
- **Sanitizing Data**: You get access to the same methods that the rest of WordPress uses for ensuring strings are safe to use.
 -->
- **フォーム送信の処理** : WordPress に `$_POST` 送信の取得と格納を、任せましょう。
- **セキュリティ対策を含む** : nonce などのセキュリティ対策を、無料で追加できます。
- **データのサニタイズ** : 文字列の安全性を確保するために WordPress の他の部分が使用しているのと同じメソッドに、アクセスできます。

<!-- 
## Function Reference
 -->
## 関数リファレンス

<!-- 
### Setting Register/Unregister
 -->
### 設定の登録/登録解除

<!-- 
- [`register_setting()`](https://developer.wordpress.org/reference/functions/register_setting/)
- [`unregister_setting()`](https://developer.wordpress.org/reference/functions/unregister_setting/)
 -->
- [`register_setting()`](https://developer.wordpress.org/reference/functions/register_setting/)
- [`unregister_setting()`](https://developer.wordpress.org/reference/functions/unregister_setting/)

<!-- 
### Add Field/Section
 -->
### フィールド / セクションの追加

<!-- 
- [`add_settings_section()`](https://developer.wordpress.org/reference/functions/add_settings_section/)
- [`add_settings_field()`](https://developer.wordpress.org/reference/functions/add_settings_field/)
 -->
- [`add_settings_section()`](https://developer.wordpress.org/reference/functions/add_settings_section/)
- [`add_settings_field()`](https://developer.wordpress.org/reference/functions/add_settings_field/)

<!-- 
### Options Form Rendering
 -->
### オプション・フォームのレンダリング

<!-- 
- [`settings_fields()`](https://developer.wordpress.org/reference/functions/settings_fields/)
- [`do_settings_sections()`](https://developer.wordpress.org/reference/functions/do_settings_sections/)
- [`do_settings_fields()`](https://developer.wordpress.org/reference/functions/do_settings_fields/)
 -->
- [`settings_fields()`](https://developer.wordpress.org/reference/functions/settings_fields/)
- [`do_settings_sections()`](https://developer.wordpress.org/reference/functions/do_settings_sections/)
- [`do_settings_fields()`](https://developer.wordpress.org/reference/functions/do_settings_fields/)

<!-- 
### Errors
 -->
### エラー

<!-- 
- [`add_settings_error()`](https://developer.wordpress.org/reference/functions/add_settings_error/)
- [`get_settings_errors()`](https://developer.wordpress.org/reference/functions/get_settings_errors/)
- [`settings_errors()`](https://developer.wordpress.org/reference/functions/settings_errors/)
 -->
- [`add_settings_error()`](https://developer.wordpress.org/reference/functions/add_settings_error/)
- [`get_settings_errors()`](https://developer.wordpress.org/reference/functions/get_settings_errors/)
- [`settings_errors()`](https://developer.wordpress.org/reference/functions/settings_errors/)