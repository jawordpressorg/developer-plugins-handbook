<!-- 
# Localization
 -->
# ローカライゼーション

<!-- 
## What is localization?
 -->
## ローカライゼーションとは何か ?

<!-- 
Localization describes the subsequent process of translating an internationalized plugin. Localization is often abbreviated as `l10n` (because there are 10 letters between the l and the n).
 -->
ローカライゼーションとは、国際化されたプラグインを翻訳する後続プロセスのことです。ローカライゼーションはしばしば `l10n` と略されます (l と n の間に 10 文字あるから)。

<!-- 
## Localization files
 -->
## ローカライゼーション・ファイル

<!-- 
### POT (Portable Object Template) files
 -->
### POT (ポータブル・オブジェクト・テンプレート) ファイル

<!-- 
This file contains the original strings (in English) in your plugin.
 -->
このファイルには、プラグインの原文の文字列 (英語) が含まれています。

<!-- 
### PO (Portable Object) files
 -->
### PO (ポータブル・オブジェクト) ファイル

<!-- 
Every translator will take the `POT` file and translate the `msgstr` sections into their own language. The result is a `PO` file with the same format as a `POT`, but with translations and some specific headers. There is one `PO` file per language.
 -->
各翻訳者は `POT` ファイルを受け取って `msgstr` セクションを自分の言語に翻訳します。その結果、`POT` と同じフォーマットで、翻訳といくつかの特定のヘッダーを持つ `PO` ファイルができます。1 つの言語につき 1 つの `PO` ファイルが存在します。

<!-- 
### MO (Machine Object) files
 -->
### MO (マシン・オブジェクト) ファイル

<!-- 
From every translated `PO` file a `MO` file is built. These are machine-readable, binary files that the gettext functions actually use (they don't care about `.POT` or `.PO` files), and are a "compiled" version of the `PO` file. The conversion is done using the `msgfmt` command line tool. In general, an application may use more than one large logical translatable module and a different `MO` file accordingly. A text domain is a handle of each module, which has a different `MO` file.
 -->
翻訳された `PO` ファイルから `MO` ファイルがビルドされます。これは機械語のバイナリーファイルで、gettext 関数が実際に使用する (`.POT` や `.PO` ファイルは気にしない) ファイルであり、`PO` ファイルの "コンパイル済み" バージョンです。変換は、`msgfmt` コマンドラインツールを使って行われます。一般的に、アプリケーションは、複数の大きな論理翻訳モジュールを使用することがあり、それに応じて `MO` ファイルも使い分けることがあります。テキストドメインは、各モジュールのハンドルであり、異なる `MO` ファイルを持ちます。

<!-- 
## Generating the POT file
 -->
## POT ファイルの生成

<!-- 
The `POT` file is the one you need to hand to translators, so that they can do their work. The `POT` and `PO` files can easily be interchangeably renamed to change file types without issues.
 -->
`POT` ファイルは、翻訳者に渡す必要があるファイルで、そうすることで翻訳者は仕事をすることができます。`POT` 及び `PO` ファイルは、ファイル名を簡単に入れ替えることができ、問題なくファイルの種類を変更することができます。

<!-- 
[info]It is a good idea to offer the POT file along with your plugin, so that translators won't have to ask you specifically about it.[/info]
 -->
[info]POT ファイルをプラグインと一緒に提供するのは良いアイデアで、そうすることで翻訳者から特に尋ねられる必要がなくなります。[/info]

<!-- 
There are a couple of ways to generate a `POT` file for your plugin:
 -->
プラグイン用の `POT` ファイルを生成するには、いくつかの方法があります :

### WP-CLI

<!-- 
Install [WP-CLI](https://make.wordpress.org/cli/handbook/guides/installing/) and use the `wp i18n make-pot` command according to the [documentation](https://developer.wordpress.org/cli/commands/i18n/make-pot/).
 -->
[WP-CLI](https://make.wordpress.org/cli/handbook/guides/installing/) をインストールし、[ドキュメント](https://developer.wordpress.org/cli/commands/i18n/make-pot/)に従って、`wp i18n make-pot` コマンドを使用します。

### Poedit

<!-- 
You can also use [Poedit](https://poedit.net/) locally when translating. This is an open source tool for all major OSs. The free Poedit default version supports manual scanning of all source code with Gettext functions. A pro version of it also features one-click scanning for WordPress plugins. After generating the `PO` file you can rename the file to `POT`. If a `MO` was generated then you can delete that file as it is not needed. If you don't have the pro version you can easily get the [Blank POT](https://github.com/fxbenard/Blank-WordPress-Pot) and use that as the base of your `POT file`. Once you have placed the blank `POT` in the languages folder you can click "Update" in Poedit to update the `POT` file with your strings.
 -->
[Poedit](https://poedit.net/) は、翻訳時にローカルで使用することもできます。これはすべての主要 OS に対応したオープンソースのツールです。無料の Poedit デフォルト版は、Gettext 関数を使ったすべてのソースコードの手動スキャンをサポートしています。プロ版では、WordPress プラグインをワンクリックでスキャンする機能もあります。`PO` ファイルを生成した後、ファイル名を `POT` に変更することができます。`MO` が生成された場合は、そのファイルは不要なので削除することができます。プロ版を持っていない場合は、[Blank POT](https://github.com/fxbenard/Blank-WordPress-Pot) を入手し、それを `POT ファイル` のベースとして使うことができます。空の `POT` を languages フォルダに置いたら、Poedit の "Update" をクリックして、`POT` ファイルをあなたの文字列で更新することができます。

<!-- 
### Grunt Tasks
 -->
### Grunt タスク

<!-- 
There are even some grunt tasks that you can use to create the POTs. [grunt-wp-i18n](https://github.com/cedaro/grunt-wp-i18n) and [grunt-pot](https://www.npmjs.com/package/grunt-pot). Steps on setting up grunt are beyond the scope of this documentation, but just be aware that it is possible. Here is an [example Grunt.js and package.json](https://gist.github.com/grappler/10187003) that you can place in the root of your plugin.
 -->
POT の作成に使える grunt タスクもあります。[grunt-wp-i18n](https://github.com/cedaro/grunt-wp-i18n) と [grunt-pot](https://www.npmjs.com/package/grunt-pot) です。grunt をセットアップする手順は、このドキュメントの範囲外ですが、可能であることだけは認識しておいてください。プラグインのルートに置くことができる [Grunt.js と package.json の例](https://gist.github.com/grappler/10187003) です。

<!-- 
## Translate the PO file
 -->
## PO ファイルの翻訳

<!-- 
Save the translated file as `my-plugin-{locale}.mo`. The locale is the language code and/or country code. For example, the locale for German is `de_DE`. From the code example above the text domain is 'my-plugin' therefore the German MO and PO files should be named `my-plugin-de_DE.mo` and `my-plugin-de_DE.po`. For more information about language and country codes, see [Installing WordPress in Your Language](https://developer.wordpress.org/advanced-administration/before-install/in-your-language/).
 -->
翻訳したファイルを `my-plugin-{ロケール}.mo` という名前で保存します。ロケールとは、言語コードや国コードのことです。例えば、ドイツ語のロケールは `de_DE` です。上記のコード例では、テキストドメインは 'my-plugin' なので、ドイツ語の MO 及び PO ファイルの名前は `my-plugin-de_DE.mo` と `my-plugin-de_DE.po` になります。言語コードと国コードの詳細情報については、[あなたの言語で WordPress のインストール](https://developer.wordpress.org/advanced-administration/before-install/in-your-language/)を参照してください。

<!-- 
There are multiple ways to translate a `PO` file.
 -->
`PO` ファイルを翻訳するには、複数の方法があります。

<!-- 
### Manually
 -->
### 手動

<!-- 
You can use a text editor to enter the translation. In a text editor it will look like this.
 -->
テキストエディタを使って翻訳を入力することができます。テキストエディタでは、次の様になります。

```
#: plugin-name.php:123
msgid "Page Title"
msgstr ""
```

<!-- 
You enter the translation between the quotation marks. For the German translation it would look like this.
 -->
引用符の間に訳語を入力します。ドイツ語の場合、次の様になります。

```
#: plugin-name.php:123
msgid "Page Title"
msgstr "Seitentitel"
```

### Poedit

<!-- 
You can also use [Poedit](https://poedit.net/) when translating. The free Poedit default version supports manual scanning of all source code with Gettext functions. A pro version of it also features one-click scanning for WordPress plugins and themes.
 -->
翻訳の際、[Poedit](https://poedit.net/) を使用することもできます。無料の Poedit デフォルト版は、Gettext 関数によるすべてのソースコードの手動スキャンをサポートしています。プロ版では、WordPress のプラグインとテーマをワンクリックでスキャンする機能もあります。

<!-- 
### Online Services
 -->
### オンライン・サービス

<!-- 
A third option is to use an online translation service. The general idea is that you upload the `POT` file and then you can give permission to users or translators to translate your plugin. This allows you to track the changes, always have the latest translation and reduce the translation being done twice.
 -->
第 3 の方法は、オンライン翻訳サービスを利用することです。一般的なアイデアは、`POT` ファイルをアップロードして、ユーザーや翻訳者にプラグインの翻訳を許可するというものです。これにより、変更を追跡することができ、常に最新の翻訳を持つことができ、翻訳が二度行なわれるのを減らすことができます。

<!-- 
Here are a few tools that can be used to translate PO files online:
 -->
PO ファイルをオンラインで翻訳するために使用できるツールをいくつかご紹介します :

- [Transifex](https://www.transifex.com/)
- [WebTranslateIt](https://webtranslateit.com/)
- [Poeditor](https://poeditor.com/)
- [GlotPress](https://wordpress.org/plugins/glotpress/)

<!-- 
## Generate MO file
 -->
## MO ファイルの生成

<!-- 
### Command line
 -->
### コマンドライン


<!-- 
`msgfmt` is used to create the MO file. `msgfmt` is part of Gettext package. Otherwise command line can be used. A typical `msgfmt` command looks like this:
 -->
`msgfmt` は、MO ファイルの作成に使用されます。`msgfmt` は、Gettext パッケージの一部です。そうでない場合は、コマンドラインを使うことができます。典型的な `msgfmt` コマンドは、以下の様なものです :

<!-- 
#### Unix Operating Systems
 -->
#### Unix オペレーティング・システム

```
msgfmt -o filename.mo filename.po
```

<!-- 
#### Windows Operating Systems
 -->
#### Windows オペレーティング・システム

```
msgfmt -o filename.mo filename.po
```

<!-- 
If you have a lot of `PO` files to convert at once, you can run it as a batch. For example, using a `bash` command:
 -->
一度にたくさんの `PO` ファイルを変換する場合は、バッチとして実行することができます。例えば、`bash` コマンドを使用します :

<!-- 
#### Unix Operating Systems (multiple files)
 -->
#### Unix オペレーティング・システム (複数ファイル)

```
# Find PO files, process each with msgfmt and rename the result to MO
for file in `find . -name "*.po"` ; do msgfmt -o ${file/.po/.mo} $file ; done
```

<!-- 
#### Windows Operating Systems (multiple files)
 -->
#### Windows オペレーティング・システム (複数ファイル)

<!-- 
For Windows you need to install [Cygwin](https://www.cygwin.com/) first.
 -->
Windows の場合は、まず [Cygwin](https://www.cygwin.com/) をインストールする必要があります。

<!-- 
Create a file called `potomo.sh` and put the following into it:
 -->
`potomo.sh` というファイルを作成し、以下の様に記述します :

```
#! /bin/sh
# Find PO files, process each with msgfmt and rename the result to MO
for file in `/usr/bin/find . -name '*.po'` ; do /usr/bin/msgfmt -o ${file/.po/.mo} $file ; done
```

<!-- 
You can run this command in the command line.
 -->
このコマンドは、コマンドラインで実行できます。

```
cd C:/path/to/language/folder/my-plugin/languages & C:/cygwin/bin/bash -c /cygdrive/c/path/to/script/directory/potomo.sh
```

### Poedit

<!-- 
`msgfmt` is also integrated in [Poedit](https://poedit.net/) allowing you to use it to generate the MO file. There is a setting in the preferences where you can enable or disable it.
 -->
`msgfmt` も [Poedit](https://poedit.net/) に統合されていて、MO ファイルの生成に使用できます。環境設定に有効/無効の設定があります。

<!-- 
![Internationalization Localization](https://i3.wp.com/developer.wordpress.org/files/2014/10/internationalization-localization-04.jpg)
 -->
![国際化ローカライゼーション](https://i3.wp.com/developer.wordpress.org/files/2014/10/internationalization-localization-04.jpg)

<!-- 
### Grunt task
 -->
### Grunt タスク

<!-- 
There is [grunt-po2mo](https://www.npmjs.com/package/grunt-po2mo) that will convert all of the files.
 -->
すべてのファイルを変換する [grunt-po2mo](https://www.npmjs.com/package/grunt-po2mo) があります。

<!-- 
## Tips for Good Translations
 -->
## 良い翻訳のためのヒント

<!-- 
### Don't translate literally, translate organically
 -->
### 機械的に翻訳するな、有機的に翻訳しろ

<!-- 
Being multi-lingual, you undoubtedly know that the languages you speak have different structures, rhythms, tones, and inflections. Translated messages don't need to be structured the same way as the English ones: take the ideas that are presented and come up with a message that expresses the same thing in a natural way for the target language. It's the difference between creating an equal message and an equivalent message: don't replicate, replace. Even with more structural items in messages, you have creative license to adapt and change if you feel it will be more logical for, or better adapted to, your target audience.
 -->
マルチリンガルであるあなたは、自分が話す言語には異なる構造、リズム、トーン、抑揚があることを知っている筈です。翻訳されたメッセージは、英語のものと同じ様に構成する必要はない : 提示されたアイデアをもとに、ターゲット言語にとって自然な方法で同じことを表現するメッセージを考え出すのです。同じメッセージを作るか、同等のメッセージを作るかの違い : 複製するのではなく、置き換えるということです。より論理的で、ターゲットとする読者によりよく適応していると感じられるなら、メッセージに構造的な項目が多くても、あなたには適応したり変更したりするクリエイティブ・ライセンスがあります。

<!-- 
### Try to keep the same level of formality (or informality)
 -->
### フォーマルさ (またはインフォーマルさ) のレベルを保つ様に

<!-- 
Each message has a different level of formality or informality. Exactly what level of formality or informality to use for each message in your target language is something you'll have to figure out on your own (or with your team), but WordPress messages (informational messages in particular) tend to have a politely informal tone in English. Try to accomplish the equivalent in the target language, within your cultural context.
 -->
各メッセージは、フォーマルさ、またはインフォーマルさのレベルが異なります。ターゲット言語での各メッセージにどのレベルのフォーマルさまたはインフォーマルさを使うかは、あなた自身 (またはあなたのチーム) で考えなければならないことだが、WordPress のメッセージ (特に情報メッセージ) は、英語ではかなりインフォーマルなトーンになる傾向があります。あなたの文化的背景の範囲内で、ターゲット言語でも同等のことを達成する様にしましょう。

<!-- 
### Don't use slang or audience-specific terms
 -->
### スラングや特定対象者特有の用語を使うな

<!-- 
Some amount of terminology is to be expected in a blog, but refrain from using colloquialisms that only the "in" crowd will get. If the uninitiated blogger were to install WordPress in your language, would they know what the term means? Words like pingback, trackback, and feed are exceptions to this rule; they're terminology that are typically difficult to translate, and many translators choose to leave in English.
 -->
ブログにはある程度の専門用語がつきものだが、 "内輪" にしか通じない様な口語表現は控えましょう。不慣れなブロガーがあなたの言語で WordPress をインストールしたとして、その用語の意味がわかるでしょうか ? ピンバック、トラックバック、フィードの様な単語は例外 ; これらは一般的に翻訳が難しい専門用語であり、多くの翻訳者は英語のままにしています。

<!-- 
### Read other software's localizations in your language
 -->
### 他のソフトウェアのローカライゼーションを、あなたの言語で読む

<!-- 
If you get stuck or need direction, try reading through the translations of other popular software tools to get a feel for what terms are commonly used, how formality is addressed, etc. Of course, WordPress has its own tone and feel, so keep that in mind when you're reading other localizations, but feel free to dig up UI terms and the like to maintain consistency with other software in your language.
 -->
行き詰まったり、指示が必要な場合は、他の一般的なソフトウェアツールの翻訳を読んでみて、どの様な用語が一般的に使用されているか、どの様にフォーマルな表現が使われているか、などの感覚をつかんでください。勿論、WordPress には独自のトーンやフィールがあるので、他のローカライゼーションを読むときは、それを念頭に置くが、あなたの言語の他のソフトウェアとの一貫性を保つために、UI 用語などを自由に掘り起こしてください。

<!-- 
## Using Localizations
 -->
## ローカライゼーションの使用

<!-- 
Place the localization files in the language folder, either in the plugin `languages` folder or as of WordPress 3.7 in the plugin `languages` folder normally under `wp-content`. The full path would be `wp-content/languages/plugins/my-plugin-fr_FR.mo`.
 -->
language フォルダ内のローカライゼーションファイルを、プラグインの `languages` フォルダ内か、WordPress 3.7 以降では通常 `wp-content` 配下のプラグイン `languages` フォルダ内に置きます。フルパスは `wp-content/languages/plugins/my-plugin-fr_FR.mo`になります。

<!-- 
You can change the language in the "General Settings". If you do not see this option, or the language into which you want to switch i snot listed, do it manually:
 -->
言語は "一般設定" で変更できます。このオプションが表示されない場合、または切り替えたい言語がリストにない場合は、手動で行なってください :

<!-- 
- Define `WPLANG` inside of `wp-config.php` to your chosen language. For example, if you wanted to use French, you would have: `define ('WPLANG', 'fr_FR');`
- Go to `wp-admin/options-general.php` or "Settings" -> "General"
- Select your language in "Site Language" dropdown
- Go to `wp-admin/update-core.php`
- Click "Update translations", when available
- Core translations files are downloaded, when available
 -->
- `wp-config.php` の中で、`WPLANG` を選択した言語に定義します。例えば、フランス語を使いたい場合は、次のようになります : `define ('WPLANG', 'fr_FR');`
- `wp-admin/options-general.php` に移動するか、"設定" -> "一般" を選択します。
- "サイトの言語" ドロップダウンで言語を選択します。
- `wp-admin/update-core.php` に移動します。
- 利用可能な場合は、"翻訳の更新" をクリックします。
- 利用可能な場合は、コアの翻訳ファイルがダウンロードされます。

<!-- 
## Resources
 -->
## リソース

<!-- 
- [Creating .pot file for your theme or plugin](https://foxland.fi/creating-pot-file-for-your-theme-or-plugin/)
- [How To Internationalize WordPress Plugins](https://tommcfarlin.com/internationalize-wordpress-plugins/)
- [Translating Your Theme](https://code.tutsplus.com/translating-your-theme--wp-25014t)
- [Blank WordPress POT](https://github.com/fxbenard/Blank-WordPress-Pot)
- [Improved i18n WordPress tools](https://github.com/grappler/i18n)
- [How to update translations quickly](https://ulrich.pogson.ch/update-translations-quickly)
- [Gist: Complete Localization Grunt task](https://gist.github.com/grappler/10187003)
- WordPress.tv
  - [i18n](https://wordpress.tv/tag/i18n/)
  - [internationalization](https://wordpress.tv/tag/internationalization/)
  - [translation](https://wordpress.tv/tag/translation/)
 -->
- [テーマやプラグインの .pot ファイルを作成する](https://foxland.fi/creating-pot-file-for-your-theme-or-plugin/)
- [WordPress プラグインを国際化する方法](https://tommcfarlin.com/internationalize-wordpress-plugins/)
- [テーマの翻訳](https://code.tutsplus.com/translating-your-theme--wp-25014t)
- [空の WordPress POT](https://github.com/fxbenard/Blank-WordPress-Pot)
- [改善された i18n WordPress ツール](https://github.com/grappler/i18n)
- [翻訳を素早く更新する方法](https://ulrich.pogson.ch/update-translations-quickly)
- [Gist: 完全なローカライゼーション Grunt タスク](https://gist.github.com/grappler/10187003)
- WordPress.tv
  - [i18n](https://wordpress.tv/tag/i18n/)
  - [国際化](https://wordpress.tv/tag/internationalization/)
  - [翻訳](https://wordpress.tv/tag/translation/)