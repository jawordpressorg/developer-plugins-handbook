<!-- 
# Planning, Submitting, and Maintaining Plugins
 -->
# プラグインの計画、申請、メンテナンス

<!-- 
You've written the next [Hello Dolly](https://wordpress.org/plugins/hello-dolly/) and you want the world to use it. What should you do?
 -->
次の [Hello Dolly](https://wordpress.org/plugins/hello-dolly/) を書き上げ、世界中の人に使ってもらいたい。どうすればいい ?

<!-- 
## 1. Test once and test again
 -->
## 1. 一度テスト、もう一度テスト

<!-- 
With any luck, your plugin will be used by lots of people in many different situations and hosting environments. You'll want to make sure you've tested your plugin to make sure it works in any situation and doesn't frustrate your users.
 -->
運が良ければ、あなたのプラグインは、さまざまな状況やホスティング環境で多くの人に使われるでしょう。プラグインがどのような状況でも動作し、ユーザーをイライラさせないことを確認するために、プラグインのテストを行うことをおすすめします。

<!-- 
## 2. Pick a good name
 -->
## 2. 良い名前の選択

<!-- 
A plugin name should reflect the uniqueness of you and your work. When you pick a name, make sure you're not violating trademarks or stomping on someone else's product names. If you're not working for FaceRange (a fake company), you shouldn't name your plugin "FaceRange's Dancing Squirrels" after all. A much better name would be ‘Dancing Squirrels for FaceRange' for example. It can be hard to come up with a good name, so take your time. Your plugin URL cannot be changed after you submit it, but the display name can change a thousand times.
 -->
プラグインの名前は、あなたとあなたの作品の独自性を反映したものでなければなりません。名前を選択する際、商標を侵害したり、他人の製品名を踏みにじったりしていないことを確認してください。もしあなたが FaceRange (架空の会社) の下で働いていないなら、あなたのプラグインに「FaceRange's Dancing Squirrels」という名前を付けるべきではありません。たとえば、「Dancing Squirrels for FaceRange」の方がずっと良い名前でしょう。良い名前を思い付くのは難しいかもしれませんから、時間をかけてください。プラグインの URL は申請後に変更できませんが、表示名は何千回でも変更できます。

<!-- 
Display names are generated from the headers in the main plugin file so mind your Ps and Qs.
 -->
表示名は、メイン・プラグインファイルのヘッダーから生成されるので、書き間違いのない様に、注意してください。

<!-- 
## 3. Write great documentation
 -->
## 3. 適切なドキュメントの作成

<!-- 
A [README.txt](https://wordpress.org/plugins/developers/#readme) file is the best place to start, as it's a standard reference point for all plugins. You'll want to make sure you include:
 -->
ファイル [README.txt](https://wordpress.org/plugins/developers/#readme) は、すべてのプラグインの標準的な参照ポイントであるため、開始するのに最適な場所です。以下を必ず含めてください:

<!-- 
- A concise description of what your plugin actually does. If it does a lot, it might be better as two plugins.
- Installation instructions, especially if there's special configuration to be done. If a user needs to register with your service, make sure you link to it.
- Directions on how to get support, and what you do and do not support.
 -->
- あなたのプラグインが、実際に何をするのかを簡潔に説明しましょう。たくさんのことをするのであれば、プラグインを2つにしたほうがいいかもしれません。
- 特に特別な設定が必要な場合、インストールに関して説明しましょう。ユーザーがあなたのサービスに登録する必要がある場合は、必ずそのリンクを張ってください。
- サポートの受け方と、何をサポートし、何をサポートしないか、の指示を説明しましょう。

<!-- 
## 4. Submit your plugin
 -->
## 4. プラグインの申請

<!-- 
In order to submit a plugin, there are three steps:
 -->
プラグインを申請するには、3つのステップがあります:

<!-- 
1. Register on WordPress.org with a valid, regularly checked email address. If you are submitting a plugin on behalf of a company, use an **official** company email for verification.
2. Whitelist `plugins@wordpress.org` in your email client to ensure you receive email communications.
3. [Submit your plugin](https://wordpress.org/plugins/developers/add/) with a brief overview of what it does and a complete, ready to go, zip of the plugin. The zip must be the complete version of your plugin, just like you would use to manually upload via the plugin installer.
 -->
1. WordPress.org に、有効で定期的にチェックされるメールアドレスで登録します。会社を代表してプラグインを提出する場合は、確認のために **公式な** 会社の電子メールを使用してください。
2. メールクライアントで `plugins@wordpress.org` をホワイトリストに登録し、確実にメールを受信できるようにしましょう。
3. プラグインが何を行うかの簡単な概要と、完全な、すぐに使える、プラグインの zip ファイルを添えて[プラグインを申請](https://wordpress.org/plugins/developers/add/)します。zip は、プラグイン・インストーラから手動でアップロードするのと同じように、プラグインの完全なバージョンでなければなりません。

<!-- 
Once a plugin is queued for review, we will review the code for any issues within 14 business days. Most of the issues can be avoided by following the guidelines. If we do find issues, we will contact the developer(s), and work towards a resolution. Once approved, you'll receive an email with details as to how to access to a [Subversion Repository](https://developer.wordpress.org/plugins/wordpress-org/how-to-use-subversion/) where you'll store your plugin.
 -->
プラグインがレビューのためにキューに入ったら、14営業日以内に問題がないかコードをレビューします。ほとんどの問題はガイドラインに従うことで回避できます。問題が見つかった場合は、開発者に連絡し、解決に向けて努力します。承認されると、プラグインを格納する [Subversion リポジトリ](https://developer.wordpress.org/plugins/wordpress-org/how-to-use-subversion/)へのアクセス方法の詳細が記載されたメールが届きます。

<!-- 
After you upload your plugin (and a [readme file](https://wordpress.org/plugins/developers/#readme)) in that repository via SVN, it will appear on the [plugin directory](https://wordpress.org/plugins/).
 -->
Subversion (SVN) 経由で、そのリポジトリにプラグイン (とファイル [readme](https://wordpress.org/plugins/developers/#readme)) をアップロードすると、[プラグイン・ディレクトリ](https://wordpress.org/plugins/)に表示されます。

<!-- 
## 5. Push out the first version
 -->
## 5. 最初のバージョンの投入

<!-- 
The WordPress.org plugins directory is the easiest way for potential users to download and install your plugin. WordPress' integration with the plugin directory means your plugin can be updated by the user in a couple of clicks.
 -->
WordPress.org のプラグイン・ディレクトリは、潜在的なユーザーがあなたのプラグインをダウンロードしてインストールする最も簡単な方法です。WordPress とプラグイン・ディレクトリの統合は、ユーザーが数回クリックするだけでプラグインを更新できることを意味します。

<!-- 
When you're ready to release your first version, you'll want to [sign up](https://wordpress.org/plugins/developers/add/). After a review process is completed successfully, you'll be granted a Subversion Repository for your code. We have documentation about [using SVN on WordPress.org](https://developer.wordpress.org/plugins/wordpress-org/how-to-use-subversion/), which is a slightly different workflow than you may be familiar with if you use GIT.
 -->
最初のバージョンをリリースする準備ができたら、[サインアップ](https://wordpress.org/plugins/developers/add/)したいと思うでしょう。レビュープロセスが正常に完了すると、コード用の Subversion リポジトリが与えられます。[WordPress.org で SVN の使用](https://developer.wordpress.org/plugins/wordpress-org/how-to-use-subversion/)に関するドキュメントがありますが、Git を使用する場合に慣れているワークフローとは少し異なります。

<!-- 
## 6. Embrace open source
 -->
## 6. オープンソースの採用

<!-- 
Open source is one of the most powerful ideas of our time because it empowers collaboration across borders. By encouraging contributions, you're allowing others to love your code as much as you do. There are several options to open source your code:
 -->
オープンソースは、国境を越えたコラボレーションを可能にする、現代で最もパワフルなアイデアのひとつです。貢献を奨励することで、他の人々があなたと同じように、あなたのコードを愛せます。あなたのコードをオープンソース化するには、いくつかの選択肢があります:

<!-- 
- [Github](https://github.com/) makes it simple to get others involved with your project. Other developers and users can submit bug fixes or reports, feature requests, or brand new contributions easily. Github has a [great documentation portal](https://support.github.com/).
	- [Bitbucket](https://bitbucket.org/) and [Gitlab](https://about.gitlab.com/) are alternatives with similar features.
- The WordPress.org Plugin Directory provides and requires you to use a [Subversion repository](https://developer.wordpress.org/plugins/wordpress-org/how-to-use-subversion/).
 -->
- [Github](https://github.com/) は、あなたのプロジェクトに他の人を参加させることを簡単にします。他の開発者やユーザーは、バグフィックスやレポート、機能リクエスト、あるいは真新しい貢献を簡単に提出できます。GitHub には、[素晴らしいドキュメントポータル](https://support.github.com/)があります。
	- [Bitbucket](https://bitbucket.org/) と [Gitlab](https://about.gitlab.com/) は、似たような機能を持つ代替手段です。
- WordPress.org プラグイン・ディレクトリは、[Subversion リポジトリ](https://developer.wordpress.org/plugins/wordpress-org/how-to-use-subversion/)を提供し、使用することを要求します。

<!-- 
## 7. Listen to your users
 -->
## 7. ユーザーの声に傾聴

<!-- 
You'll often find that your users put your code through many more test cases than you could've imagined. This can be tremendously valuable feedback.
 -->
あなたが想像していた以上に、ユーザーがあなたのコードに多くのテストケースを課していることに気付くでしょう。これは、途轍もなく貴重なフィードバックになります。

<!-- 
Releasing your code through WordPress.org means your plugin automatically has a support forum. Use it! You can subscribe to receive new posts by email and respond to your users in a timely manner. They just want to love your plugin as much as you do.
 -->
WordPress.org を通じてコードを公開するということは、あなたのプラグインが自動的にサポートフォーラムを持つことを意味します。それを使いましょう ! 新しい投稿をメールで受け取り、ユーザーにタイムリーに対応できます。彼らは、あなたと同じように、あなたのプラグインを愛したいと思っています。

<!-- 
Jetpack has a post you can point to about [writing great bug reports](https://jetpack.com/blog/how-to-write-a-great-bug-report/).
 -->
Jetpack には、[優れたバグレポートの書き方](https://jetpack.com/blog/how-to-write-a-great-bug-report/)についての投稿があります。

<!-- 
## 8. Regularly push new versions
 -->
## 8. 定期的な新バージョンの投入

<!-- 
The best plugins are the ones that keep iterating over time, pushing small changes along the way. Don't let your hard work go stale by waiting too long to update. Keep in mind, constant upgrades can cause ‘Update Fatigue' and users will stop upgrading. Keeping a balance between too few updates and too many updates is important.
 -->
最高のプラグインとは、時間をかけて小さな変更を繰り返し続けるものです。アップデートを長く延期しすぎて、苦労して作ったプラグインを時代遅れにさせないでください。一方、絶え間ないアップグレードは「アップデート疲れ」を引き起こし、ユーザーはアップグレードをやめてしまうということも、心にとどめておいてください。少なすぎるアップデートと多すぎるアップデートのバランスを保つことが重要です。

<!-- 
## 9. Rinse and repeat
 -->
## 9. 同じ手順の繰り返し

<!-- 
Like in other parts of life, the best things come from patience and hard work.
 -->
人生の他の部分と同じように、最高のものは忍耐と努力から生み出されるものなのです。