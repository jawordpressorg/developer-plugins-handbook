<!--
# Add Your Plugin to the Block Directory
-->

# ブロックディレクトリにプラグインを追加する

<!--
There are two main directory listings of block related plugins.
-->

ブロック関連プラグインの主なディレクトリ・リストは、2つあります。

<!--
- Plugins that are **only** blocks
- Plugins that contain blocks
-->

- ブロック **のみ** を含むプラグイン
- ブロックを含むプラグイン

<!--
A plugin can be listed in both, however there will be no benefit to your plugin SEO or ranking due to either. The only benefit to being a plugin that is only a block is that you gain the ability to be added to the Block Directory in the Block Editor itself, for immediate installation.
-->

プラグインは両方に登録できますが、どちらを選んでもプラグインの SEO やランキングには何のメリットもありません。ブロックだけのプラグインであることの唯一の利点は、ブロックエディター自体でブロックディレクトリに追加され、すぐにインストールできるようになることです。

<!--
## Block Only Plugins
-->

## ブロックのみプラグイン

<!--
Block Only plugins are plugins that **only** contain blocks.
-->

「ブロックのみプラグイン」は、ブロック **のみ** を含むプラグインです。

<!--
Block Plugins are required to be much smaller and more minimalist than a regular WordPress plugin in order to be safely installed with a single click. That means as well as keeping to the regular [plugin guidelines](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/) you’ll also need to follow some additional rules. In particular, you should stick to mostly JavaScript code and keep PHP to the bare minimum; and not add any UI or other code outside of the Gutenberg editor.
-->

ブロック・プラグインは、ワンクリックで安全にインストールするために、通常の WordPress プラグインよりもはるかに小さく、よりミニマルであることが要求されます。つまり、通常の[プラグイン・ガイドライン](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/)を守るだけでなく、いくつかの追加ルールに従う必要があります。特に、主に JavaScript のコードに集中し、PHP は最低限に保つ必要があります; そして、Gutenberg エディター以外の UI やその他のコードを追加しないようにしましょう。

<!--
If you’re a committer of a block plugin that does meet the criteria for adding it to the [Block Directory](https://wordpress.org/plugins/browse/block/) as confirmed by the Checker tool, you can then add it yourself [using the Block Checker tool](https://wordpress.org/plugins/developers/block-plugin-validator/):
-->

あなたがブロック・プラグインのコミッターである場合、チェッカーツールで確認した結果、[ブロックディレクトリ](https://ja.wordpress.org/plugins/browse/block/)に追加する条件を満たしていれば、[ブロックチェッカー・ツールを使って](https://ja.wordpress.org/plugins/developers/block-plugin-validator/)自分で追加できます:

<!--
![Block checker tool interface with a "Add Plugin Name to the Block Directory" button](https://i0.wp.com/developer.wordpress.org/files/2020/08/Screen-Shot-2020-07-10-at-1.29.25-pm.png?resize=1024%2C308&ssl=1)
-->

![ブロックチェッカー・ツールのインターフェース、「ブロックディレクトリに -プラグイン名- を追加」ボタン](https://i0.wp.com/developer.wordpress.org/files/2020/08/Screen-Shot-2020-07-10-at-1.29.25-pm.png?resize=1024%2C308&ssl=1)

<!--
Likewise you can remove it at any time using that same tool if you notice problems or would prefer it wasn’t included.
-->

同様に、問題に気付いたり、含まれていないほうがいいと思ったりした場合は、同じツールを使っていつでも削除できます。

<!--
**Helpful tools:**
-->

**便利なツール:**

<!--
- [Block Creation tutorial](https://github.com/WordPress/gutenberg/pull/22831/files?short_path=c4d2c28#diff-c4d2c286eac33acdc7571032a984e0ca) – how to write a block plugin
- [Block Submission tutorial](https://github.com/WordPress/gutenberg/pull/23545/files?short_path=555f1c3#diff-555f1c31856d86ed5ff0d492b5a127c1) – tips and suggestions for ensuring your block is ready for the Block Directory
- [Block Checker tool](https://make.wordpress.org/plugins/2020/07/11/you-can-now-add-your-own-plugins-to-the-block-directory/) – validate plugin for inclusion
-->

- [ブロック作成チュートリアル](https://github.com/WordPress/gutenberg/pull/22831/files?short_path=c4d2c28#diff-c4d2c286eac33acdc7571032a984e0ca) – ブロック・プラグインの書き方
- [ブロック登録チュートリアル](https://github.com/WordPress/gutenberg/pull/23545/files?short_path=555f1c3#diff-555f1c31856d86ed5ff0d492b5a127c1) – ブロックディレクトリへのブロック登録を確実にするためのヒントと提案
- [ブロックチェッカー・ツール](https://make.wordpress.org/plugins/2020/07/11/you-can-now-add-your-own-plugins-to-the-block-directory/) – プラグインを掲載するために検証する

<!--
## Plugins Containing Blocks
-->

## ブロックが含まれるプラグイン

<!--
Many older plugins, as well as larger and more complex plugins, may contain blocks. They also will contain other features, like widgets. An example of this sort of plugin would be Jetpack or Yoast SEO. While they have a large number of features, they also contain some blocks.
-->

多くの古いプラグインや、より大規模で複雑なプラグインには、ブロックが含まれていることがあります。また、ウィジェットのような他の機能も含まれているでしょう。このようなプラグインの例としては、Jetpack や Yoast SEO が挙げられます。これらのプラグインには多くの機能がありますが、いくつかのブロックも含まれています。

<!--
If you’ve written a plugin that introduces or improves blocks, or know of a plugin that does, **email us at [plugins@wordpress.org](mailto:plugins@wordpress.org)** and request your plugin be added. At that time, your plugin will be reviewed to confirm this request, but also to ensure you meet all current guideline standards.
-->

ブロックを導入または改善するプラグインを作成した場合、またはそのようなプラグインを知っている場合は、**[plugins@wordpress.org](mailto:plugins@wordpress.org) 宛に e メールで** プラグインの追加をリクエストしてください。その際、あなたのプラグインは、このリクエストを確認するためだけでなく、現在のガイドライン基準をすべて満たしているかについてもレビューされます。

<!--
Before you email, please make certain your plugin is compatible with the latest version of WordPress and that it is free from all security issues. If there are security or guideline issues in your plugin, it may be closed pending your corrections.
-->

メールを送る前に、あなたのプラグインが WordPress の最新バージョンと互換性があり、セキュリティ上の課題がないことを確認してください。あなたのプラグインにセキュリティやガイドライン上の課題がある場合、あなたの修正待ちでクローズされることがあります。
