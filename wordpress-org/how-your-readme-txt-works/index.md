<!--
# Plugin Readmes
-->

# プラグイン Readme

<!--
This page will explain some aspects of the plugin directory, and explain of the more obvious aspects which a lot of people miss.
-->

このページでは、プラグイン・ディレクトリのいくつかの側面を説明し、多くの人々が見逃している、より明白な側面について説明します。

<!--
To make your entry in the plugin browser most useful, each plugin should have a readme file named `readme.txt` that adheres to the [WordPress plugin readme file standard](https://wordpress.org/plugins/readme.txt). This file controls the output on the front-facing part of the directory. Writing a description in the readme determines exactly what will be displayed on `wordpress.org/plugins/Your-Plugin`
-->

プラグイン・ブラウザのエントリーを最も有用なものにするために、各プラグインは、[WordPress プラグイン readme ファイル標準](https://ja.wordpress.org/plugins/readme.txt)に準拠した `readme.txt` という名称の readme ファイルを持つ必要があります。このファイルは、ディレクトリのフロントページの出力を制御します。readme に詳細を記述することで、`wordpress.org/plugins/Your-Plugin` に何が表示されるかが決まります。

<!--
You can use the [plugin readme generator](https://generatewp.com/plugin-readme/) and put your completed result through the [official readme validator](https://wordpress.org/plugins/developers/readme-validator/) to check it. If you need more visual assistance you can use the tool [wpreadme.com](https://wpreadme.com/)
-->

[プラグイン readme ジェネレーター](https://generatewp.com/plugin-readme/)を使い完成した結果を、[公式 readme バリデーター](https://ja.wordpress.org/plugins/developers/readme-validator/)を通してチェックできます。より視覚的な支援が必要な場合は、[wpreadme.com](https://wpreadme.com/)というツールを使うことができます。

<!--
Since WordPress 5.8 plugin [readme files are not parsed for requirements](https://core.trac.wordpress.org/ticket/48520). This means that headers `Requires PHP` and `Requires at least` are going to be parsed from plugin’s main PHP file.
-->

WordPress 5.8以降、プラグインの [readme ファイルは、要件としてパースされることはありません](https://core.trac.wordpress.org/ticket/48520)。これは、ヘッダー `Requires PHP` と `Requires at least` が、プラグインのメイン PHP ファイルからパースされることを意味します。

<!--
## Section Details
-->

## セクション詳細

<!--
All plugins contain a main PHP file, and almost all plugins have a `readme.txt` file as well. The `readme.txt` file is intended to be written using a subset of markdown.
-->

すべてのプラグインにはメインの PHP ファイルがあり、ほぼすべてのプラグインにはファイル `readme.txt` もあります。ファイル `readme.txt` は、Markdown のサブセットを使って記述することを想定しています。

<!--
### Readme Header Information
-->

### Readme ヘッダー情報

<!--
The Plugin readme header consists of this information:
-->

プラグインの readme ヘッダーは、この情報で構成されています:

```
=== Plugin Name ===
Contributors: (this should be a list of wordpress.org userid's)
Donate link: https://example.com/
Tags: tag1, tag2
Requires at least: 4.7
Tested up to: 5.4
Stable tag: 4.3
Requires PHP: 7.0
License: GPLv2 or later
License URI: https://www.gnu.org/licenses/gpl-2.0.html
Here is a short description of the plugin.  This should be no more than 150 characters.  No markup here.
```

<!--
- **Contributors** – a case sensitive, comma separated list of all WordPress.org usernames who have contributed to the code. It is generally considered respectful to include the names of people who worked on forked projects. Some developers will ask to be removed from the list, as they don’t want other plugins showing up on their profile page. It’s best to honor those requests. Remember to _only_ use the WordPress.org username – anything else will show up sans profile link and gravatar. To change someone’s display name (which shows on the front facing pages for the plugin), edit the profile `https://wordpress.org/support/users/YOURID/edit/` and change the display name.
- **Donate link** – (OPTIONAL) Makes a “Donate to this plugin” link in the sidebar. If there is no link, nothing shows up.
- **Tags** – 1 to 5 comma separated terms that describe the plugin. Plugins must refrain from using competitors plugin names as tags. Plugins should not use tags which are unique to that plugin, as these will not be shown.
- **Tested up to** – The version of WordPress that the plugin has been tested against. This field _ignores_ minor versions, as plugins shouldn’t break with a minor update. This means a plugin only need to define the major version it is tested against and the WordPress.org plugin directory will automatically add the minor version. This should be numbers _only_, so ‘4.9’ and not ‘WP 4.9’
- **Requires PHP** – (OPTIONAL) The required _minimum_ version of PHP needed for use with this plugin. This should be numbers _only_, so ‘7.0’ and not ‘PHP 7.0’
- **Stable Tag** – The stable version of the plugin. This is _not_ the version of WordPress, but the version of the plugin itself. Only use numbers and periods, and [SemVer formatting](https://semver.org/) is recommended.
- **License** – The GPLV2 (or later) compatible license used for the plugin.
- **License URI** – (OPTIONAL) A link to the license. This is optional, but if a plugin uses a more rare license, strongly recommended.
-->

- **Contributors** – 大文字と小文字を区別し、カンマで区切られた、コードに貢献した WordPress.org のすべてのユーザー名のリスト。フォークされたプロジェクトで働いた人の名前を含めることは、一般的に敬意を表していると考えられています。開発者の中には、他のプラグインが自分のプロフィールページに表示されるのを望まないので、リストから削除してほしいと頼む人もいます。そのような要請には従うのが一番です。WordPress.org の **ユーザー名だけ** を使うことを忘れないでください – それ以外だとプロフィールリンクや gravatar が表示されません。(プラグインのフロントページに表示される) 誰かの表示名を変更するには、プロフィール `https://wordpress.org/support/users/YOURID/edit/` を編集し、表示名を変更します。
- **Donate link** – (任意) サイドバーに「このプラグインに寄付する」リンクを作成します。リンクがない場合は、何も表示されません。
- **Tags** – プラグインを説明する、カンマで区切られた、1～5個の語句。プラグインは、競合他社のプラグイン名をタグとして使用することを差し控える必要があります。プラグイン独自のタグは、表示されないので、使用しないでください。
- **Tested up to** – プラグインがテストされた WordPress のバージョン。プラグインはマイナーアップデートで壊れることはないので、このフィールドはマイナーバージョンを **無視します**。つまり、プラグインはテスト対象のメジャーバージョンを定義するだけでよく、WordPress.org のプラグイン・ディレクトリは、自動的にマイナーバージョンを追加することを意味します。これは数字 _だけ_ であるべきですので、「4.9」であって「WP 4.9」ではありません。
- **Requires PHP** – (任意) このプラグインを使用するために必要な PHP の **最低** バージョン。これは **数字だけ** であるべきですので、「7.0」であって「PHP 7.0」ではありません。
- **Stable Tag** – プラグインの安定バージョン。これは、WordPress のバージョン **ではなく**、プラグイン自体のバージョンです。数字とピリオドのみを使用し、[SemVer フォーマット](https://semver.org/)を推奨します。
- **License** – プラグインに使用されている GPLV2 (またはそれ以降) と互換性のあるライセンス。
- **License URI** – (任意) ライセンスへのリンク。これは任意ですが、プラグインがよりまれなライセンスを使用している場合は、強く推奨します。

<!--
At the end of the header section is a place for a _short_ description of a plugin. The example recommends no more than 150 characters and to not use markup. That line of text is the single line description of the plugin which shows up right under the plugin name. If it’s longer than 150 characters, it gets cut off, so keep it short.
-->

ヘッダー・セクションの最後には、プラグインの **短い** 説明のための場所があります。この例では、150文字以内で、マークアップを使わないことを推奨しています。そのテキスト行は、プラグイン名のすぐ下に表示される、プラグインの1行説明です。150文字より長いとカットされてしまうので、短く書きましょう。

<!--
### Installation
-->

### 導入方法

<!--
If your plugin has no custom install settings, it’s okay to omit this section. If your plugin has custom configuration notes post install, this is a great place to put that information.
-->

プラグインにカスタム・インストール設定がない場合、このセクションは省略してもかまいません。もしあなたのプラグインにインストール後のカスタム設定メモがある場合、ここはその情報を書くのに最適な場所です。

<!--
### Custom Sections
-->

### カスタム・セクション

<!--
While custom sections are permitted and supported, please use them in moderation. People get used to seeing how every other plugin looks, and when yours is weird, they’ll miss important information.
-->

カスタム・セクションは許可され、サポートされていますが、節度を持って使用してください。他のプラグインの見た目に慣れてしまうと、あなたのプラグインが変わっていると、重要な情報を見逃してしまいます。

<!--
## Technical Details
-->

## 技術的な詳細

<!--
While most of the readme details are self evident, there are a few sections that trip people up.
-->

Readme の詳細のほとんどは自明ですが、人々を引っ掛ける箇所がいくつかあります。

<!--
### How The Readme Is Parsed
-->

### Readme のパース方法

<!--
[warning]While using the stable tag of trunk currently works in the Plugin Directory, it’s not a supported or recommended method to indicate new versions and has been known to cause issues with automatic updates. At this time, we are actively discouraging and (in the case of new plugins) prohibiting it’s use[/warning]
-->

[warning]現在のところ、trunk の Stable Tag は、プラグイン・ディレクトリで使用できますが、新しいバージョンを示す方法としてはサポートされていませんし、推奨されていませんし、自動アップデートで問題を引き起こすことが知られています。現時点では、積極的に推奨していませんし、(新しいプラグインの場合) その使用を禁止しています。[/warning]

<!--
WordPress.org’s Plugin Directory works based on the information found in the field **Stable Tag** in the readme. When WordPress.org parses the `readme.txt`, the very first thing it does is to look at the `readme.txt` in the `/trunk` directory, where it reads the “Stable Tag” line.
-->

WordPress.org のプラグイン・ディレクトリは、readme の **Stable Tag** フィールドにある情報にもとづいて動作します。WordPress.org が `readme.txt` をパースする際、最初に行うのはディレクトリ `/trunk` の `readme.txt` を見ることで、そこで「Stable Tag」行を読み取ります。

<!--
When the Stable Tag is properly set, WordPress.org will go and look in `/tags/` for the referenced version. So a Stable Tag of “1.2.3” will make it look for `/tags/1.2.3/`.
-->

Stable Tag が適切に設定されると、WordPress.org は `/tags/` で参照されているバージョンを検索します。つまり、「1.2.3」の Stable Tag は `/tags/1.2.3/` を検索することになります。

<!--
[tip]The readme.txt in the tag folder must also be properly updated to have the correct “Stable Tag” — failing to do so may cause your plugin to not be updatable.[/tip]
-->

[tip]tag フォルダー内の readme.txt も正しく更新し、正しい「Stable Tag」にする必要があります — それを怠ると、プラグインを更新できなくなる可能性があります。[/tip]

<!--
If the Stable Tag is 1.2.3 and `/tags/1.2.3/` exists, then nothing in trunk will be read any further for parsing by any part of the system. If you try to change the description of the plugin in `/trunk/readme.txt` then your changes won’t do anything on your plugin page. Everything comes from the `readme.txt` in the file being pointed to by the Stable Tag.
-->

もし Stable Tag が1.2.3であり、`/tags/1.2.3/` が存在するなら、trunk に含まれるものは、システムのどの部分からもパースされるために、それ以上読み込まれることはありません。`/trunk/readme.txt` でプラグインの説明を変更しようとする場合、その変更はプラグインページでは何も意味を持ちません。すべては、Stable Tag が指し示しているファイルの `readme.txt` から由来します。

<!--
The WordPress.org Plugin Directory reads the main plugin PHP file to get things like the Name of the plugin, the Plugin URI, and most importantly, the version number. On the plugin page, you’ll see the download button which reads “Download Version 1.2.3” or similar. That version number comes from the plugin’s main PHP file, _not_ the readme!
-->

WordPress.org のプラグイン・ディレクトリは、プラグインの PHP ファイルを読み込み、プラグインの名前、プラグイン URI、そして最も重要なバージョン番号などを取得します。プラグインページには、「バージョン1.2.3をダウンロード」などと書かれたダウンロードボタンがあります。そのバージョン番号は、プラグインのメイン PHP ファイルから取得したもので、readme から取得したもの _ではありません_ !

<!--
The Stable Tag points to a subdirectory in the `/tags` directory. But the version of the plugin is not actually set by that folder name. Instead, it’s the version that is listed in the plugin’s PHP file itself which determines the name. If you have changed Stable Tag to 1.4 and the plugin still says 1.3 in the PHP file, then the version listed will be 1.3.
-->

Stable Tag は、ディレクトリ `/tags` のサブディレクトリを指し示します。しかし、プラグインのバージョンは、実際にはそのフォルダー名では設定されません。その代わりに、プラグインの PHP ファイル自体に記載されているバージョンによって、名前が決まります。Stable Tag を1.4に変更しても、プラグインの PHP ファイルに1.3と記載されている場合、バージョンは1.3となります。

<!--
### Videos
-->

### 動画

<!--
You can embed videos from YouTube, Vimeo, and anywhere else [WordPress supports by default](https://wordpress.org/support/article/embeds/). All you have to do is paste the video URL onto it’s own line in your readme.
-->

YouTube、Vimeo、その他[WordPress がデフォルトでサポートしている](https://wordpress.org/support/article/embeds/)どこからでも、動画を埋め込むことができます。動画の URL を、readme の専用行に貼り付けるだけです。

<!--
We recommend you NOT have the video as the final line in a FAQ section, as sometimes formatting gets weird.
-->

フォーマットが変になることがあるので、動画を FAQ セクションの最終行に「しない」ことをおすすめします。

<!--
### Markdown
-->

### Markdown

<!--
The readmes use a customized version of [Markdown](https://daringfireball.net/projects/markdown/). Most Markdown calls work as expected.
-->

readme は、[Markdown](https://daringfireball.net/projects/markdown/) のカスタマイズ版を使用しています。ほとんどの Markdown 呼び出しは、期待通りに動作します。

<!--
Markdown allows for easy linking in your readme.txt as well. Just write like this to link a word to a URL:
-->

Markdown を使えば、readme.txt にも簡単にリンクを張ることができます。単語を URL にリンクさせるには、このように書くだけです:

\[WordPress\](http://wordpress.org)

<!--
Videos can be put into your readme.txt too. A YouTube or Vimeo link on a line by itself will be auto-embedded. It’s also possible to embed videos hosted on VideoPress using the wpvideo shortcode.
-->

動画も readme.txt に入れることができます。YouTube や Vimeo のリンクを1行に記述すると、自動的に埋め込まれます。wpvideo ショートコードを使用して、VideoPress でホストされている動画を埋め込むことも可能です。

<!--
### Field Details
-->

### フィールド詳細

<!--
For those who want to know exactly what gets parsed into what:
-->

何が何にパースされるのかを、正確に知りたい人のために:

<!--
- **Authors**
  Author field from the plugin header and Contributors field from the readme file.
- **Version**
  Version field from the plugin header.
- **Tags** (as in categories)
  Tags field from the readme file.
- **Plugin Name**
  The Plugin Name from the readme file falling back on the Plugin Name specified in the plugin header.
- **Author and Plugin Homepages**
  The Author URI and Plugin URI fields of the plugin header. The Plugin URI should be _unique_ to each plugin. Do **not** use the same URI for your free and pro plugin. It ends badly.
- **Last updated time**
  Time of last check in to the appropriate directory after a version number change.
- **Creation time**
  Time of _first_ check in.
-->

- **Authors**
 プラグイン・ヘッダーの Author フィールドと readme ファイルの Contributors フィールド。
- **Version**
 プラグイン・ヘッダーの Version フィールド。
- **Tags** (カテゴリーと同じ)
 readme ファイルの Tags フィールド。
- **Plugin Name**
 readme ファイルの Plugin Name は、プラグイン・ヘッダーで指定された Plugin Name にフォールバックする。
- **Author and Plugin Homepages**
 プラグイン・ヘッダーの Author URI と Plugin URI フィールド。プラグイン URI は、各プラグインに対して **一意** でなければなりません。無償プラグインとプロプラグインに同じ URI を使用 **しないでください**。酷い結果になります。
- **Last updated time**
 バージョン番号変更後、該当ディレクトリにチェックインした最後の時刻。
- **Creation time**
 **初回** チェックインの時刻。

<!--
### File Size
-->

### ファイル・サイズ

<!--
While readmes are simple text files, having a file larger than 10k may result in errors. Your readme should be brief and to the point. The description should not be a sales pitch as much as a description of the plugin, what it does, and how to use it. Your install directions should be direct. Your FAQ should actually address issues.
-->

readme は、シンプルなテキストファイルですが、10k を超えるファイルはエラーになる可能性があります。readme は、簡潔で要点を押さえたものでなければなりません。説明文は、売り込みではなく、プラグインの説明、プラグインが何をするのか、プラグインの使い方を説明してください。インストール手順は、直接的であるべきです。FAQ は、実際に課題に対処したものであるべきです。

<!--
As for your changelog, we recommend keeping the current release in the readme and splitting the rest out out into it’s own file — `changelog.txt` for example. By storing all the older changelog data there, you keep your readme small and allow the people who get really into long changelogs to read things on their own.
-->

変更履歴については、現在のリリースを readme に残し、残りを独自のファイル — たとえば、`changelog.txt` — に分割することをおすすめします。古い変更履歴のデータをすべてそこに保存することで、readme を小さく保つことができ、長い変更履歴を読みたがる人は、自分で読めます。

<!--
Similarly, if you need in-depth documentation with inline images and so on, direct people to your own website.
-->

同様に、インライン画像などを含む詳細な文書が必要な場合は、人々を独自の web サイトに誘導しましょう。

<!--
## See Also
-->

## 関連記事

<!--
- [Plugin Headers](https://developer.wordpress.org/plugins/plugin-basics/header-requirements/) (found in the main file of the plugin)
-->

- [プラグイン・ヘッダー](https://ja.wordpress.org/team/handbook/plugin-development/plugin-basics/header-requirements/) (プラグインのメイン・ファイルにあります)
