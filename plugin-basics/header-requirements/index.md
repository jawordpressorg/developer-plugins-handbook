<!-- 
# Header Requirements
 -->
# ヘッダーの必要条件

<!-- 
As described in [Getting Started](https://developer.wordpress.org/plugins/plugin-basics/#getting-started), the main PHP file should include header comment what tells WordPress that a file is a plugin and provides information about the plugin.
 -->
[はじめに](https://developer.wordpress.org/plugins/plugin-basics/#getting-started)で説明したように、メインの PHP ファイルには、ファイルがプラグインであることを WordPress に伝え、プラグインに関する情報を提供するヘッダーコメントを含める必要があります。

<!-- 
## Minimum Fields
 -->
## 最低限の項目

<!-- 
At a minimum, a header comment must contain the Plugin Name:
 -->
最低限、ヘッダーコメントには「Plugin Name」を含める必要があります:

```
/*
 * Plugin Name: YOUR PLUGIN NAME
 */
```

<!-- 
## Header Fields
 -->
## ヘッダー項目

<!-- 
Available header fields:
 -->
利用可能なヘッダー項目:

<!-- 
- **Plugin Name:** (_required_) The name of your plugin, which will be displayed in the Plugins list in the WordPress Admin.
- **Plugin URI:** The home page of the plugin, which should be a unique URL, preferably on your own website. This _must be unique_ to your plugin. You cannot use a WordPress.org URL here.
- **Description:** A short description of the plugin, as displayed in the Plugins section in the WordPress Admin. Keep this description to fewer than 140 characters.
- **Version:** The current version number of the plugin, such as 1.0 or 1.0.3.
- **Requires at least:** The lowest WordPress version that the plugin will work on.
- **Requires PHP:** The minimum required PHP version.
- **Author:** The name of the plugin author. Multiple authors may be listed using commas.
- **Author URI:** The author's website or profile on another website, such as WordPress.org.
- **License:** The short name (slug) of the plugin's license (e.g. GPLv2). More information about licensing can be found in the [WordPress.org guidelines](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/#1-plugins-must-be-compatible-with-the-gnu-general-public-license).
- **License URI:** A link to the full text of the license (e.g. [https://www.gnu.org/licenses/old-licenses/gpl-2.0.html](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html)).
- **Text Domain:** The [gettext](https://www.gnu.org/software/gettext/) text domain of the plugin. More information can be found in the [Text Domain](https://developer.wordpress.org/plugins/internationalization/how-to-internationalize-your-plugin/#text-domains) section of the [How to Internationalize your Plugin](https://developer.wordpress.org/plugins/internationalization/how-to-internationalize-your-plugin/) page.
- **Domain Path:** The domain path lets WordPress know where to find the translations. More information can be found in the [Domain Path](https://developer.wordpress.org/plugins/internationalization/how-to-internationalize-your-plugin/#domain-path) section of the [How to Internationalize your Plugin](https://developer.wordpress.org/plugins/internationalization/how-to-internationalize-your-plugin/) page.
- **Network:** Whether the plugin can only be activated network-wide. Can only be set to _true_, and should be left out when not needed.
- **Update URI:** **(_Important: never use for a plugin hosted in the WordPress.org Plugin Directory_)** Allows non WordPress.org plugins to avoid accidentally being overwritten with an update of a plugin of a similar name from the WordPress.org Plugin Directory. For more info read related [dev note](https://make.wordpress.org/core/2021/06/29/introducing-update-uri-plugin-header-in-wordpress-5-8/).
 -->
- **Plugin Name:** (_required_) WordPress 管理画面のプラグインリストに表示される、プラグインの名前です。
- **Plugin URI:** これはプラグインのホームページであり、できればあなた自身の Web サイトにあるユニークな URL でなければなりません。これはあなたのプラグイン _独自のものでなければなりません_。WordPress.org の URL は使用できません。
- **Description:** WordPress 管理画面のプラグインセクションに表示される、プラグインの短い説明です。この説明は140文字以内に収めてください。
- **Version:** 1.0や1.0.3など、プラグインの現在のバージョン番号です。
- **Requires at least:** プラグインが動作する WordPress の最低バージョンです。
- **Requires PHP:** 最低限必要な PHP のバージョンです。
- **Author:** プラグイン作者の名前です。カンマを使って複数の作者を列挙できます。
- **Author URI:** 作者の Web サイト、または WordPress.org のような他の Web サイト上の、プロフィールです。
- **License:** プラグインのライセンスの短い名前 (スラッグ) です (例: GPLv2)。ライセンスの詳細については、[WordPress.orgのガイドライン](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/#1-plugins-must-be-compatible-with-the-gnu-general-public-license)を参照してください。
- **License URI:** ライセンスの全文へのリンクです ([https://www.gnu.org/licenses/old-licenses/gpl-2.0.html](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html) 等)。
- **Text Domain:** プラグインのテキストドメイン [gettext](https://www.gnu.org/software/gettext/) です。詳細は、[プラグインを国際化する方法](https://developer.wordpress.org/plugins/internationalization/how-to-internationalize-your-plugin/)ページの[テキスト・ドメイン](https://developer.wordpress.org/plugins/internationalization/how-to-internationalize-your-plugin/#text-domains)セクションを参照してください。
- **Domain Path:** ドメインパスによって、WordPress に翻訳の場所を知らせることができます。詳細は、[プラグインを国際化する方法](https://developer.wordpress.org/plugins/internationalization/how-to-internationalize-your-plugin/)ページの[ドメイン・パス](https://developer.wordpress.org/plugins/internationalization/how-to-internationalize-your-plugin/#domain-path)セクションを参照してください。
- **Network:** プラグインをネットワーク全体でのみ有効にするか否かを指定します。_true_ にしか設定できないので、必要ない場合は設定しないでください。
- **Update URI:** ** (_重要: WordPress.org Plugin Directory でホストされているプラグインには絶対に使用しないでください。_) **これにより、WordPress.org 以外のプラグインが、WordPress.org Plugin Directory にある似た名前のプラグインのアップデートで誤って上書きされるのを防ぐことができます。詳細は、関連 [dev note](https://make.wordpress.org/core/2021/06/29/introducing-update-uri-plugin-header-in-wordpress-5-8/) を参照してください。

<!-- 
A valid PHP file with a header comment might look like this:
 -->
ヘッダーコメントを持つ有効な PHP ファイルは、以下のようになります:

```
/*
 * Plugin Name:       My Basics Plugin
 * Plugin URI:        https://example.com/plugins/the-basics/
 * Description:       Handle the basics with this plugin.
 * Version:           1.10.3
 * Requires at least: 5.2
 * Requires PHP:      7.2
 * Author:            John Smith
 * Author URI:        https://author.example.com/
 * License:           GPL v2 or later
 * License URI:       https://www.gnu.org/licenses/gpl-2.0.html
 * Text Domain:       my-basics-plugin
 * Domain Path:       /languages
 */
```

<!-- 
Here's another example which allows file-level PHPDoc DocBlock as well as WordPress plugin file headers:
 -->
ファイルレベルの PHPDoc DocBlock と WordPress プラグインのファイルヘッダーを許可する、別の例です:

```
/**
 * Plugin Name
 *
 * @package           PluginPackage
 * @author            Your Name
 * @copyright         2019 Your Name or Company Name
 * @license           GPL-2.0-or-later
 *
 * @wordpress-plugin
 * Plugin Name:       Plugin Name
 * Plugin URI:        https://example.com/plugin-name
 * Description:       Description of the plugin.
 * Version:           1.0.0
 * Requires at least: 5.2
 * Requires PHP:      7.2
 * Author:            Your Name
 * Author URI:        https://example.com
 * Text Domain:       plugin-slug
 * License:           GPL v2 or later
 * License URI:       https://www.gnu.org/licenses/gpl-2.0.txt
 */
```

<!-- 
## Notes
 -->
## 備考

<!-- 
[alert]When assigning a version number to your project, keep in mind that WordPress uses the PHP `version_compare()` function to compare plugin version numbers. Therefore, before you release a new version of your plugin, you should make sure that this PHP function considers the new version to be "greater" than the old one. For example, 1.02 is actually greater than 1.1.[/alert]
 -->
[alert]プロジェクトにバージョン番号を割り当てる際には、WordPress はプラグインのバージョン番号を比較するために PHP の関数 `version_compare()` を使うことを覚えておいてください。よって、プラグインの新バージョンをリリースする前に、この PHP 関数が新バージョンを旧バージョンより「大きい」とみなすかどうかを確認する必要があります。たとえば、1.02は1.1よりも実際には大きいのです。[/alert]