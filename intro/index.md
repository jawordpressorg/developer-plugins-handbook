<!--
# Introduction to Plugin Development
-->

# プラグイン開発の紹介

<!--
Welcome to the Plugin Developer Handbook. Whether you're writing your first plugin or your fiftieth, we hope this resource helps you write the best plugin possible.
-->

プラグイン開発者ハンドブックへようこそ。初めてプラグインを書くのであれ、50個目のプラグインを書くのであれ、このリソースが可能な限り最高のプラグインを書く助けになることを願っています。

<!--
The Plugin Developer Handbook covers a variety of topics — everything from what should be in the plugin header, to security best practices, to tools you can use to build your plugin. It's also a work in progress — if you find something missing or incomplete, please notify the documentation team in slack and we'll make it better together.
-->

プラグイン開発者ハンドブックでは、さまざまなトピックを扱います。プラグインのヘッダーに書くべき内容から、セキュリティのベストプラクティス、プラグインを構築するために使用するツールまで、あらゆるトピックを扱います。もし足りないものや不完全なものを見つけたら、slack でドキュメントチームに知らせてください。

<!--
## Why We Make Plugins
-->

## プラグインを作る理由

<!--
If there's one cardinal rule in WordPress development, it's this: **Don't touch WordPress core**. This means that you don't edit core WordPress files to add functionality to your site. This is because WordPress overwrites core files with each update. Any functionality you want to add or modify should be done using plugins.
-->

WordPress の開発で基本的なルールが1つあるとすれば、それは **WordPress のコア部分には触らないこと** です。つまり、WordPress のコアファイルを編集して、サイトに機能を追加してはいけないということです。WordPress はアップデートのたびにコアファイルを上書きしてしまうからです。追加したい機能や修正したい機能は、プラグインを使用して行う必要があります。

<!--
WordPress plugins can be as simple or as complicated as you need them to be, depending on what you want to do. The simplest plugin is a single PHP file. The [Hello Dolly](https://wordpress.org/plugins/hello-dolly/ "Hello Dolly Plugin") plugin is an example of such a plugin. The plugin PHP file just needs a [Plugin Header](https://developer.wordpress.org/plugins/plugin-basics/header-requirements/), a couple of PHP functions, and some [hooks](https://developer.wordpress.org/plugins/hooks/) to attach your functions to.
-->

WordPress のプラグインは、やりたいことに応じて、簡単なものから複雑なものまで作ることができます。最もシンプルなプラグインは、単一の PHP ファイルです。[Hello Dolly](https://wordpress.org/plugins/hello-dolly/ "Hello Dolly Plugin") プラグインはそのようなプラグインの例です。プラグインの PHP ファイルは、[プラグインヘッダー](https://developer.wordpress.org/plugins/plugin-basics/header-requirements/) といくつかの PHP 関数、そして関数をアタッチするための[フック](https://developer.wordpress.org/plugins/hooks/) が必要なだけです。

<!--
Plugins allow you to greatly extend the functionality of WordPress without touching WordPress core itself.
-->

プラグインは、WordPress のコアそのものに触れることなく、WordPress の機能を大幅に拡張できます。
