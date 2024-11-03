<!-- 
# Block Specific Plugin Guidelines
 -->
# ブロック固有のプラグイン・ガイドライン

<!-- 
[info]All Block Specific plugins must also comply with the [overall plugin guidelines](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/). These additional guidelines are unique to block specific plugins.[/info]
 -->
[info]すべてのブロック固有のプラグインは、[プラグイン全般のガイドライン](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/)にも従わなければなりません。これらの追加ガイドラインは、ブロック固有のプラグインに特有のものです。[/info]

<!-- 
## Guide to submitting plugins to the Block Directory
 -->
## ブロック・ディレクトリへのプラグイン申請ガイド

<!-- 
The goal of the [Block Directory](https://wordpress.org/plugins/browse/block/) is to provide a safe place for WordPress users to find and install new blocks.
 -->
[ブロック・ディレクトリ](https://wordpress.org/plugins/browse/block/)の目指すところは、WordPress ユーザーが新しいブロックを見つけてインストールするための安全な場所を提供することです。

<!-- 
### User Expectations
 -->
### ユーザーへの期待

<!-- 
- Users will have a place they can go, both within their WordPress admin and on WordPress.org, where they can download and install blocks that have been pre-vetted for major security issues.
- Users will be able to one-click install blocks from their admin, one at a time.
- Blocks will appear in their block library after installation and activation.
- Blocks will work seamlessly and immediately without intrusive advertisements or upselling.
 -->
- ユーザーは、WordPress の管理画面と WordPress.org の両方で、セキュリティ上の課題がないか事前に審査されたブロックをダウンロードしてインストールできる場所を持つことができます。
- ユーザーは、管理画面からワンクリックでブロックを1つずつインストールできます。
- ブロックは、インストールと有効化後にブロック・ライブラリに表示されます。
- ブロックは、押し付けがましい広告やアップセリングなしに、シームレスかつ即座に機能します。

<!-- 
### Developer Expectations
 -->
### 開発者への期待

<!-- 
- Developers will have a concrete set of requirements and guidelines to follow when writing blocks for the Block Directory.
- Following these guidelines will help ensure that the blocks they develop can be seamlessly installed in the editor.
- Blocks submitted to the Block Directory are held to stricter technical and policy rules than WordPress plugins in general.
- Plugins with blocks that do not meet the Block Directory Guidelines may still be submitted to the Plugin Directory.
 -->
- 開発者は、ブロック・ディレクトリ用のブロックを作成する際に従うべき、具体的な要件とガイドラインを持つことになります。
- これらのガイドラインに従うことで、開発したブロックをエディターにシームレスにインストールできます。
- ブロック・ディレクトリに提出されたブロックは、一般的な WordPress プラグインよりも厳しい技術的ルールおよびポリシールールに従います。
- ブロック・ディレクトリ・ガイドラインを満たしていないブロックを含むプラグインも、プラグイン・ディレクトリに登録できます。

<!-- 
### Definitions
 -->
### 定義

<!-- 
For the purposes of the Block Directory, we distinguish between two types of plugins:
 -->
ブロック・ディレクトリでは、2種類のプラグインを区別しています:

<!-- 
1. Plugins that exist solely to distribute a block.
2. All other plugins, including those that bundle many independent blocks, plugins that contain blocks in addition to other functionality, and plugins with no blocks at all.
 -->
1. ブロックを配布するためだけに存在するプラグイン。
2. 多くの独立したブロックをバンドルするプラグイン、他の機能に加えてブロックを含むプラグイン、ブロックをまったく含まないプラグイン、これらを含む、その他のすべてのプラグイン。

<!-- 
These guidelines apply specifically to the first type of plugin, which is called a Block Plugin. If a plugin is of the second type, then the further guidelines and restrictions do not apply. All plugins, be they block-only or not, are required to comply with the [Detailed Plugin Guidelines](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/).
 -->
これらのガイドラインは、特にブロック・プラグインと呼ばれる、最初のタイプのプラグインに適用されます。プラグインが2番目のタイプであれば、さらなるガイドラインと制限は適用されません。すべてのプラグインは、ブロック・プラグインであろうとなかろうと、[プラグイン詳細ガイドライン](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/)に従うことが要求されます。

<!-- 
### Block Plugins and the Block Directory
 -->
### ブロック・プラグインとブロック・ディレクトリ

<!-- 
The Block Directory contains only Block Plugins, that is to say plugins that contain only a single, independent, top-level block and a minimum of supporting code. Block plugins have the following characteristics:
 -->
ブロック・ディレクトリには、ブロック・プラグインだけが含まれています。すなわち、単一の独立したトップレベルブロックと、最小限のサポートコードのみを含むプラグインです。ブロック・プラグインには、以下の特徴があります:

<!-- 
1. A specific type of WordPress plugin, with the same structure including a `readme.txt` file.
2. Containing only blocks (typically a single top-level block).
3. Contain a minimum of server-side (i.e. PHP) code.
4. Self-contained with no UI outside of the post editor.
 -->
1. WordPress プラグインの特定の種類のことで、`readme.txt` ファイルを含む同じ構造を持つ。
2. ブロックのみを含む (一般的には単一のトップレベルブロック)。
3. 最小限のサーバーサイド (つまり PHP) コードを含む。
4. 投稿エディター以外の UI を持たない、自己完結型。

<!-- 
In addition to the guidelines that apply to all WordPress plugins, Block Plugins that are submitted to the Block Directory must adhere to these guidelines:
 -->
ブロック・ディレクトリに提出されるブロック・プラグインは、すべての WordPress プラグインに適用されるガイドラインに加え、これらのガイドラインに従わなければなりません:

<!-- 
### Guidelines
 -->
### ガイドライン

<!-- 
#### 1. Block Plugins are for the Block Editor.
 -->
#### 1. ブロック・プラグインは、ブロック・エディター用。

<!-- 
A Block Plugin must contain a block, and a minimum of other supporting code. It may not contain any UX outside of the editor, such as WordPress options or `wp-admin` menus. Server-side code should be kept to a minimum.
 -->
ブロック・プラグインは、ブロックと、その他の最小限のサポートコードを含んでいなければなりません。WordPress のオプションや `wp-admin` メニューなど、エディター以外の UX を含むことはできません。サーバーサイドのコードは、最小限に抑える必要があります。

<!-- 
Plugins that only extend or provide styles for other, pre-existing blocks are currently not eligible for inclusion in the Block Directory. At this time, they are not supported by the Block Editor’s seamless install process. Only Block Plugins that register a new block are currently supported.
 -->
他の既存のブロックを拡張したり、他の既存のブロックにスタイルを提供するだけのプラグインは、現在のところ、ブロック・ディレクトリに含めることはできません。現時点では、ブロック・エディターのシームレスなインストールプロセスには未対応です。現在のところ、新規ブロックを登録するブロック・プラグインにのみ対応しています。

<!-- 
#### 2. Block Plugins are separate blocks.
 -->
#### 2. ブロック・プラグインは、独立したブロック。

<!-- 
Block plugins are intended to be single purpose, separate, independent blocks, not bundles or compendiums of many blocks. In most cases, a Block Plugin should contain only one single top-level block. The Block Directory will not include collections of blocks that could be reasonably split up into separate, independent, blocks.
 -->
ブロック・プラグインは、多くのブロックのバンドルや作品集ではなく、単一の目的の、別個の、独立したブロックであることを意図しています。たいていの場合、ブロック・プラグインは、単一のトップレベル・ブロックのみを含むべきです。ブロック・ディレクトリには、ブロックのコレクションは含まれません。個別の独立したブロックに分割するのが合理的です。

<!-- 
Block plugins may contain more than one block where a clearly necessary parent/child or container/content dependency exists; for example a list block that contains list item blocks.
 -->
ブロック・プラグインは、明らかに必要な親/子関係、あるいはコンテナ/コンテンツの依存関係が存在する場合には、複数のブロックを含むことができます; たとえば、リスト・アイテム・ブロックを含むリスト・ブロックなどです。

<!-- 
#### 3. Plugin and block names should reflect the block’s purpose.
 -->
#### 3. プラグイン名とブロック名は、ブロックの目的を反映したものであるべき。

<!-- 
Plugin titles and block titles should describe what the block does in a way that helps users easily understand its purpose. In most cases the plugin title and the block title should be identical or very similar. Some examples of good plugin and block names include:
 -->
プラグインタイトルとブロックタイトルは、ユーザーがそのブロックの目的を簡単に理解できるように、そのブロックが何をするのかを説明する必要があります。ほとんどの場合、プラグインタイトルとブロックタイトルは同じか、非常に似ているべきです。プラグイン名とブロック名の好例を、いくつか挙げます:

<!-- 
`Rainbow Block`
`Sepia Image Grid`
`Business Hours Block`
 -->
`Rainbow Block`
`Sepia Image Grid`
`Business Hours Block`

<!-- 
Please avoid plugin and block titles unrelated to the block itself, or that cannot be easily distinguished from core blocks. Some examples of unhelpful plugin and block names are things such as:
 -->
ブロック自体に関係のないプラグインやブロックのタイトル、またはコアブロックと簡単に区別できないようなタイトルは、どうか避けてください。プラグイン名やブロック名の悪例としては、以下のようなものがあります:

<!-- 
`PluginCo Inc Block`
`Widget`
`Image Block`
 -->
`PluginCo Inc Block`
`Widget`
`Image Block`

<!-- 
The same trademark restrictions for plugin titles exist for block titles and names. This means that a block may not be named “Facerange Block” unless developed by a legal representative of Facerange.
 -->
プラグインタイトルに関する商標の制限は、ブロックのタイトルや名称にも適用されます。つまり、Facerange の法定代理人によって開発されたものでない限り、ブロックの名称を「Facerange Block」にはできません。

<!-- 
#### 3a. Block names should be unique and properly namespaced.
 -->
#### 3a. ブロック名は一意であるべきで、適切に名前空間を設定すべき。

<!-- 
The block name (meaning the [`name` parameter to `registerBlockType()`](https://developer.wordpress.org/block-editor/developers/block-api/block-registration/#block-name) and [`name` in `block.json`](https://github.com/WordPress/gutenberg/blob/master/docs/rfc/block-registration.md#name)) must be unique to the block. As with titles, please respect trademarks and other projects’ commonly used names, so as not to conflict with them.
 -->
([`registerBlockType()` のパラメータ `name`](https://developer.wordpress.org/block-editor/developers/block-api/block-registration/#block-name) と [`block.json` の `name`](https://github.com/WordPress/gutenberg/blob/master/docs/rfc/block-registration.md#name)を意味する) ブロック名は、ブロックに固有でなければなりません。タイトルと同様に、商標や他のプロジェクトで一般的に使われている名前を尊重して、それらと衝突しないようにしてください。

<!-- 
The namespace prefix to the block name should reflect either the plugin author, or the plugin slug. For example:
 -->
ブロック名の名前空間の接頭辞は、プラグインの作者かプラグインのスラッグのどちらかを反映する必要があります。たとえば:

<!-- 
`name: "my-rainbow-block-plugin/rainbow"`, or
`name: "john-doe/rainbow"`, or
`name: "pluginco/rainbow"`.
 -->
`name: "my-rainbow-block-plugin/rainbow"`、あるいは
`name: "john-doe/rainbow"`、あるいは
`name: "pluginco/rainbow"`。

<!-- 
The namespace may not be a reserved one such as `core` or `wordpress`.
 -->
名前空間は、`core` や `wordpress` のような予約されたものであっては、なりません。

<!-- 
#### 4. Block Plugins must include a `block.json` file.
 -->
#### 4. ブロック・プラグインは、`block.json` ファイルを含める必要がある。

<!-- 
The Block Registration RFC outlines the format of a `block.json` file: [https://github.com/WordPress/gutenberg/blob/master/docs/designers-developers/developers/block-api/block-metadata.md](https://github.com/WordPress/gutenberg/blob/master/docs/designers-developers/developers/block-api/block-metadata.md)
 -->
ブロック登録 RFC は、`block.json` ファイルのフォーマットを概説しています: [https://github.com/WordPress/gutenberg/blob/master/docs/designers-developers/developers/block-api/block-metadata.md](https://github.com/WordPress/gutenberg/blob/master/docs/designers-developers/developers/block-api/block-metadata.md)

<!-- 
Block Plugins must include a valid `block.json` file. In addition to the requirements specified in the RFC, the `block.json` must include the following attributes:
 -->
ブロック・プラグインには、有効な `block.json` ファイルを含める必要があります。`block.json` には、RFC で指定されている要件に加えて、以下の属性が含まれていなければなりません:

<!-- 
- `name`
- `title`
- At least one of: `script`, `editorScript`
- At least one of: `style`, `editorStyle`
 -->
- `name`
- `title`
- 右記の少なくとも1つ: `script`、`editorScript`
- 右記の少なくとも1つ: `style`、`editorStyle`

<!-- 
#### 5. Block Plugins must work independently.
 -->
#### 5. ブロック・プラグインは、独立して動作すべき。

<!-- 
Block Plugins must function by themselves without requiring any external dependencies such as another WordPress plugin or theme.
 -->
ブロック・プラグインは、他の WordPress プラグインやテーマなどの外部依存を必要とせず、それ自体で機能しなければなりません。

<!-- 
A Block Plugin may make use of code or hooks in another WordPress plugin or theme, provided the Block Plugin is still usable without that plugin or theme installed. For example, a Recipe Block Plugin is permitted to apply a filter implemented in a slider plugin to improve its image display, as long as the Recipe Block Plugin is still usable without the slider plugin.
 -->
ブロック・プラグインは、他の WordPress プラグインやテーマのコードやフックを利用できますが、それらのプラグインやテーマがインストールされていなくても、ブロック・プラグインが使用可能であることが条件となります。たとえば、レシピ・ブロック・プラグインは、スライダー・プラグインに実装されたフィルターを適用して、画像表示を改善できますが、レシピ・ブロック・プラグインが、スライダープラグインなしで使用可能である場合に限ります。

<!-- 
#### 6. Block Plugins should work seamlessly.
 -->
#### 6. ブロック・プラグインは、シームレスに動作すること。

<!-- 
Block Plugins are intended to work seamlessly and instantly when installed from the editor. That means they should not encumber the user with additional steps or prerequisites such as installing another plugin or theme, signing up for an account, or logging in or manually connecting to an external service.
 -->
ブロック・プラグインは、エディターからインストールした際、シームレスかつ即座に動作することを目的としています。つまり、他のプラグインやテーマのインストール、アカウントのサインアップ、あるいは、外部サービスへのログインや外部サービスとの手動接続、によってユーザーを煩わせるべきではないということです。

<!-- 
No form of payment is permitted for the use of a Block Plugin. While it is allowed to use the donation link feature in the plugin’s readme, or to link from the full plugin listing, the Block Plugin itself must be free to use. Block plugins that do require a paid service or include upselling and premium features are still permitted in the main WordPress Plugin Directory, subject to its guidelines.
 -->
ブロック・プラグインの使用に対して対価を求めることは許されません。プラグインの Readme にある寄付リンク機能を使ったり、フルプラグイン一覧からリンクしたりすることは許されていますが、ブロック・プラグイン自体は無料で使えるものでなければなりません。有償サービスを必要とするブロック・プラグインや、アップセルやプレミアム機能を含むブロック・プラグインは、ガイドラインに従って、メインの WordPress プラグイン・ディレクトリで許可されています。

<!-- 
Block Plugins may use an external/cloud API where necessary, provided it can be done seamlessly without requiring a login or activation key.
 -->
ブロック・プラグインは、ログインやアクティベーションキーを必要とせずにシームレスに実行できる場合に限り、必要に応じて外部/クラウド API を使用できます。

<!-- 
They should not rely on an external API or cloud service for functions that could be performed locally.
 -->
ローカルで実行可能な機能を、外部の API やクラウドサービスに依存すべきではありません。

<!-- 
#### 7. Server-side code should be kept to a minimum.
 -->
#### 7. サーバーサイドのコードは、最小限にとどめるべき。

<!-- 
Since Block Plugins are WordPress plugins, they necessarily contain PHP code for metadata and initialization. As much as possible, they should avoid including additional PHP code or server-side libraries. The WordPress REST API should be the preferred interface to WordPress, rather than custom server-side code.
 -->
ブロック・プラグインは、WordPress のプラグインですから、必然的にメタデータや初期化のための PHP コードを含みます。可能な限り、追加の PHP コードやサーバーサイド・ライブラリを含めることは避けるべきです。WordPress REST API は、サーバーサイドのカスタムコードではなく、WordPress へのインターフェイスとして優先されるべきです。

<!-- 
There are limits to the REST API, and situations where server-side PHP is the only performant way to implement a feature. In those situations, PHP code may be included, provided it is clearly written, used as little as possible, and well documented.
 -->
REST API には限界があり、ある機能を実装するためにはサーバーサイドで PHP を使うのが唯一の方法であるという状況もあり、そのような状況では、PHP コードを含めることができます。ただし、PHP コードを明確に記述し、できるだけ使用しないようにし、ドキュメントをきちんと作成する必要があります。

<!-- 
#### 8. Must not include advertisements or promotional notices.
 -->
#### 8. 広告や販売促進に関する告知を、含まないこと。

<!-- 
Block Plugins must not include code that displays alerts, dashboard notifications, or similar obtrusive messages unrelated to the purpose of the block.
 -->
ブロック・プラグインは、アラート、ダッシュボード通知、またはブロックの目的とは無関係な同様の邪魔なメッセージを表示するコードを含んではなりません。