<!--
# What is a Plugin?
-->

# プラグインとは何ですか ?

<!--
Plugins are packages of code that extend the core functionality of WordPress. WordPress plugins are made up of PHP code and can include other assets such as images, CSS, and JavaScript.
-->

プラグインは、WordPress のコア機能を拡張するコードのパッケージです。WordPress のプラグインは PHP コードで構成されており、画像、CSS、JavaScript などの他のアセットを含めることができます。

<!--
By making your own plugin you are _extending_ WordPress, for example, building additional functionality on top of what WordPress already offers, or you could write a plugin that displays links to the ten most recent posts on your site.
-->

プラグインを作成することは、WordPress を「拡張」することです。たとえば、WordPress がすでに提供している機能の上にさらに機能を追加したり、サイトの最新の10記事へのリンクを表示するプラグインを作成できます。


<!--
Or, using WordPress' custom post types, you could write a plugin that creates a full-featured support ticketing system with email notifications, custom ticket statuses, and a client-facing portal. The possibilities are _endless_!_
-->

あるいは、WordPress のカスタム投稿タイプを使用して、電子メール通知、カスタムチケットステータス、および顧客向けポータルを備えたフル機能のサポートチケットシステムを作成するプラグインを作成することも可能です。可能性は無限大です !

<!--
Most WordPress plugins are composed of many files, but a plugin really only _needs_ one main file with a specifically formatted [DocBlock](https://en.wikipedia.org/wiki/PHPDoc) in the header.
-->

WordPress のプラグインは多くのファイルで構成されていますが、プラグインとして認識されるために本当に必要なのは、ヘッダーに特別な書式の [DocBlock](https://en.wikipedia.org/wiki/PHPDoc) を持つ1つのメインファイルだけです。

[Hello Dolly](https://wordpress.org/plugins/hello-dolly/ "Hello Dolly"), one of the first plugins, is only [100 lines](https://plugins.trac.wordpress.org/browser/hello-dolly/trunk/hello.php) long. Hello Dolly shows lyrics from [the famous song](https://en.wikipedia.org/wiki/Hello,_Dolly!_(song)) in the WordPress admin. Some CSS is used in the PHP file to control how the lyric is styled.

最初のプラグインの一つである [Hello Dolly](https://wordpress.org/plugins/hello-dolly/ "Hello Dolly") は、わずか[100行](https://plugins.trac.wordpress.org/browser/hello-dolly/trunk/hello.php)の長さです。Hello Dolly は、WordPress の 管理画面に[有名な曲](https://en.wikipedia.org/wiki/Hello,_Dolly!_(song))の歌詞を表示します。その PHP ファイルには、歌詞のスタイルを制御するためにいくつかの CSS が使用されています。

<!--
As a WordPress.org plugin author, you have an amazing opportunity to create a plugin that will be installed, tinkered with, and loved by millions of WordPress users. All **you** need to do is turn your great idea into code. The Plugin Handbook is here to help you with that.
-->

WordPress.org のプラグイン作者として、何百万人もの WordPress ユーザーにインストールされ、いじられ、愛されるプラグインを作成するすばらしい機会があります。**あなた**がすべきことは、あなたのすばらしいアイデアをコードにすることです。プラグインハンドブックは、そのお手伝いをするためにあります。
