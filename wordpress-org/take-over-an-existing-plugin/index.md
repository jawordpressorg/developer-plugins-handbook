<!-- 
# Take Over an Existing Plugin
 -->
# 既存プラグインを引き継ぐ

<!-- 
People cease development on their plugins for a variety of reasons. Instead of letting those plugins stagnate, we encourage people to instead list them for adoption by another, more active, developer.
 -->
さまざまな理由で、プラグインの開発を断念する人がいます。そのようなプラグインを停滞させるのではなく、より積極的な他の開発者に引き継いでもらえるよう、プラグインをリストに載せることをおすすめします。

<!-- 
In adopting a plugin, you are promising to be responsible for all future development, and to ensure the plugin (and you) comply with all [plugin guidelines](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/).
 -->
プラグインを引き継ぐことで、あなたは将来のすべての開発に責任を持ち、プラグイン (そして、あなた) がすべての[プラグイン・ガイドライン](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/)遵守を約束することになります。

<!-- 
[alert]Not all requests will be approved, even following a successful review.[/alert]
 -->
[alert]レビューに合格しても、すべてのリクエストが承認されるわけではありません。[/alert]

<!-- 
## The Adoption Process
 -->
## 引き継ぎプロセス

<!-- 
There are two ways a plugin can be adopted.
 -->
プラグインを引き継ぐには、2つの方法があります。

<!-- 
1. You ask the developer directly, they say yes and add you
2. You ask the Plugin Review team to assist you
 -->
1. 開発者に直接尋ねて、開発者が「はい」と言って、あなたを追加する
2. プラグイン・レビューチームに、支援を依頼する

<!-- 
Since you’re reading this, you likely are working on the second method, so keep reading. You will be expected to have followed **all** the steps herein.
 -->
これを読んでいるあなたは、おそらく2つ目の方法に取り組んでいるはずですので、このまま読み進めてください。ここに書かれている **すべて** のステップを踏んでいることが期待されます。

<!-- 
### 1. Check the Plugin Status
 -->
### 1. プラグイン・ステータスの確認

<!-- 
If the plugin is open and active, give it a full review on your own before you go any further. Make sure you feel comfortable and capable of maintaining the code long term.
 -->
もしそのプラグインがオープンで、アクティブであれば、先に進む前にあなた自身で完全なレビューをしてください。長期にわたるコード維持が、快適かつ可能であることを確認してください。

<!-- 
If a plugin is closed because it was **unused**, you can skip the rest of this and email `plugins@wordpress.org` right away and attach your version of the proposed plugin.
 -->
プラグインが **不使用** という理由でクローズされた場合は、この続きを省略して、提案プラグインのあなたのバージョンを添付して、すぐに `plugins@wordpress.org` にメールしてください。

<!-- 
If the plugin was closed for security issues, we require **all** those issues to be resolved, so put your best foot forward and demonstrate you have the impetus to find and fix those issues.
 -->
もしプラグインがセキュリティ上の課題でクローズされたのであれば、私たちはそれらの課題を **すべて** 解決することを求めるので、最善を尽くし、それらの課題を見つけ、修正する意欲があることを証明してください。

<!-- 
Closed plugins are _less_ likely to be able to be adopted, as the nature of their closures may be more complex and intricate. If a plugin was closed for license issues, for example, we may not be permitted to reopen it for anyone except the license holders.
 -->
クローズされたプラグインは、そのクローズの性質がより複雑で入り組んでいる可能性があるため、引き継がれる可能性が _低い_ です。たとえば、ライセンス課題でクローズされたプラグインは、ライセンス保持者以外には再オープンが許可されないかもしれません。

<!-- 
Larger plugins (100k users or more) are also less likely to be adopted, as that is a not-insignificant userbase, and we need to be sure you really are capable of managing a plugin of that size.
 -->
大規模なプラグイン (100k ユーザー以上) は引き継がれる可能性も低くなります。というのも、その規模のユーザーベースは決して小さくないため、その規模のプラグインを管理する能力が本当にあるかどうかを確認する必要があるからです。

<!-- 
### 2. Contact the Original Developer
 -->
### 2. オリジナル開発者に連絡を取る

<!-- 
You _must_ attempt to contact the original developer, as they can [give you access to the plugin](https://developer.wordpress.org/plugins/wordpress-org/plugin-developer-faq/#plugin-ownership). We recommend trying:
 -->
[プラグインへのアクセス権を与える](https://developer.wordpress.org/plugins/wordpress-org/plugin-developer-faq/#plugin-ownership)ことができるため、オリジナル開発者に _必ず_ 連絡を取るようにしてください。試してみることをおすすめします:

<!-- 
- email
- leaving a comment on the plugin support page
- opening a GitHub issue
 -->
- メールする
- プラグインのサポートページに、コメントを残す
- GitHub issue を作成する

<!-- 
We expect you to make all reasonable efforts to reach out to them. If the plugin page says the plugin has no active developer, then you’re fine.
 -->
私たちは、あなたが彼らと連絡を取るためにあらゆる合理的な努力をすることを期待しています。プラグインのページに、そのプラグインにはアクティブな開発者がいないと書かれていれば、問題ありません。

<!-- 
If you _do_ get in touch with the developer, ask them to [transfer ownership to you](https://developer.wordpress.org/plugins/wordpress-org/plugin-developer-faq/#plugin-ownership). They can do this on their own and, once it’s done, you may manage the plugin. If they have issues, have them contact the plugin team via email and we will assist them.
 -->
もし開発者と連絡を _取る_ のであれば、[所有権をあなたに移す](https://developer.wordpress.org/plugins/wordpress-org/plugin-developer-faq/#plugin-ownership)ように頼んでください。彼らは自分でこれを行うことができ、それが完了したら、あなたはプラグインを管理できます。もし彼らに問題があれば、メールでプラグイン・チームに連絡してください。私たちが支援します。

<!-- 
If there’s no way to get in touch, or they don’t reply, move to step 3.
 -->
連絡を取る方法がない、あるいは返信がない場合は、ステップ3に進みます。

<!-- 
### 3. Update The Code
 -->
### 3. コードの更新

<!-- 
Even if the plugin has been given to you by the developer, you must review the code from the top down to make sure it’s safe, secure, and meets our current [guidelines](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/).
 -->
プラグインを開発者から譲り受けたとしても、安全でセキュアであり、現在の[ガイドライン](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/)に適合していることを確認するために、コード全体を上からレビューする必要があります。

<!-- 
Your update must include editing the readme to ensure it documents the new ownership (and preferably when it takes place), removing all links to their site/support resources, as well as updating the copyright information to include you. Remember, copyright is additive. You keep the old and add yours on.
 -->
あなたの更新には、「新しい所有権を確実に文書化する (できれば、所有権の移動がいつ行われるのかも)、readme の編集」、「彼らのサイト/サポートリソースへの、すべてのリンクの削除」、そして「あなたを含む著作権情報の更新」が含まれていなければなりません。著作権は、付加的なものであることを忘れないでください。古いものを残し、あなたのものを加えるのです。

<!-- 
If your plugin is a major upgrade, you _must_ provide an upgrade path. Just wanting a name-slug is not sufficient reason to take over a plugin. We care deeply about our users, and violating their trust in us by breaking their existing sites with your upgrades is to be avoided at all costs.
 -->
もしあなたのプラグインがメジャーアップグレードであれば、アップグレードパスを提供 _しなければなりません_。単にネームスラッグが欲しいだけでは、プラグインを引き継ぐ十分な理由にはなりません。私たちはユーザーをとても大切にしています。あなたのアップグレードによって既存のサイトを壊してしまうことで、私たちに対するユーザーの信頼を侵害することは絶対に避けなければなりません。

<!-- 
Remember you need to _increase_ the version number so people are prompted to upgrade to your new version.
 -->
新しいバージョンへのアップグレードを促すために、バージョン番号を _上げる_ 必要があることを忘れないでください。

<!-- 
### 4. Submit Your Code for Review
 -->
### 4. レビューのために、コードを提出する

<!-- 
If you still can’t get in touch with the original developer, you’ll need to ask the Plugin Review Team for help.
 -->
それでもオリジナル開発者と連絡が取れない場合は、プラグイン・レビューチームに助けを求める必要があります。

<!-- 
Once you’ve finished updating the code, email `plugins@wordpress.org` explaining how you tried to contact the original developer and with your code attached as a zip. If you can’t email zips, then upload it to some file service (Google Drive, Dropbox, etc) or provide a link to your code repository (Github, Bitbucket, etc). Make sure the link is public!
 -->
コードの更新が完了したら、オリジナル開発者とどのように連絡を取ろうとしたかを説明し、コードを zip 形式で添付して `plugins@wordpress.org` にメールしてください。zip ファイルをメールできない場合は、ファイルサービス (Google Drive、Dropbox、など) にアップロードするか、コードリポジトリ (GitHub、Bitbucket、など) へのリンクを提供してください。リンクが公開されていることを確認してください !

<!-- 
After we receive your version of the code as a zip, we will review it and test it. At this point, you will go through a _normal_ review process. That is, we will treat you like any new plugin and we will check the whole plugin for security and guidelines. Even if those issues are found in the original plugin, you will be required to fix them.
 -->
あなたのバージョンのコードを zip で受け取った後、私たちはそれをレビューし、テストします。この時点で、あなたは _通常の_ レビュープロセスを経ることになります。つまり、新しいプラグインと同じように扱い、プラグイン全体のセキュリティとガイドラインをチェックします。たとえオリジナルプラグインにそのような課題が見つかったとしても、修正する必要があります。

<!-- 
At this stage, some plugins are determined to have existing security flaws. We may close those plugins, depending on the nature of the issues, and you will be trusted to not publicly disclose those issues.
 -->
この段階で、セキュリティ上の欠陥があると判断されるプラグインもあります。課題の内容によっては、それらのプラグインをクローズすることもありますし、あなたにはそれらの課題を公表しないという約束をしていただきます。

<!-- 
### 5. We Contact the Original Developer
 -->
### 5. 我々が、オリジナル開発者に連絡を取る

<!-- 
Once we feel the code is acceptable, and that you are capable of sustaining that specific plugin in a secure manner that adheres to our guidelines, we will contact the original developer on your behalf and give them your information, explaining that you want to take over development.
 -->
私たちがそのコードを受け入れ、あなたが私たちのガイドラインに従った安全な方法で特定のプラグインを維持する能力があると感じたら、あなたの代わりにオリジナル開発者に連絡し、あなたの情報を伝え、あなたが開発を引き継ぎたいことを説明します。

<!-- 
We’ll do everything we can to ensure the original plugin author has been notified, but sometimes that’s just not possible.
 -->
できる限りオリジナルプラグインの作者に通知するよう努めますが、不可能な場合もあります。

<!-- 
### 6. Wait Patiently
 -->
### 6. 気長に待つ

<!-- 
We give the original developer 30 days (1 month) to reply to our inquiry. Should they reply and deny the request, we will honour their decision and ask you to convert the plugin into a forked version. We do our best to respect them as much as we respect you as a developer, and honor their wishes with their work.
 -->
私たちは、30日 (1ヵ月) 以内に私たちの問い合わせに返答するよう、オリジナル開発者に伝えます。もし彼らが返答し、リクエストを拒否した場合、私たちは彼らの決定を尊重し、あなたにプラグインをフォークしたバージョンにコンバートするよう依頼します。私たちは、開発者であるあなたと同じように彼らを尊重し、彼らの仕事に対する彼らの意思を尊重するよう最善を尽くします。

<!-- 
If they approve it, we will assist in transitioning the plugin to your account.
 -->
承認されれば、プラグインをあなたのアカウントに移管する支援をします。

<!-- 
If they don’t reply, and you’ve made it this far, we will likely transfer the plugin to you.
 -->
もし返信がなく、ここまで来たのであれば、プラグインをあなたに譲渡することになるでしょう。

<!-- 
### 7. Update the Plugin
 -->
### 7. プラグインの更新

<!-- 
In order to _safely_ update the plugin, we will close it before we add you. You will then be required to update via SVN. Once that’s done, we’ll double check everything is correct and reopen it. The plugin will now be yours.
 -->
プラグインを _安全に_ 更新するために、あなたを追加する前にプラグインをクローズします。その後、SVN 経由でアップデートしてください。それが完了したら、すべてが正しいことを再確認し、プラグインを再オープンします。これでプラグインは、あなたのものになります。

<!-- 
## Frequently Asked Questions
 -->
## よくある質問

<!-- 
### Will old reviews/support posts be removed?
 -->
### 古いレビューやサポートの投稿は、削除されるの ?

<!-- 
No. You inherit the good and the bad.
 -->
いいえ。良いことも悪いことも継承します。

<!-- 
### Do I have to keep the original developer on?
 -->
### オリジナル開発者は、継続雇用する必要があるの ?

<!-- 
No. You can (and in fact should) remove commit access from anyone who is not actively maintaining the plugin. However. Per copyright restrictions, you must retain their credit in the code. We recommend you also leave them listed as a contributor.
 -->
いいえ。プラグインを積極的に保守していない人からのコミットアクセスを削除できます (実際そうすべき)。しかしながら。著作権の規定により、あなたはその人のクレジットをコードに残さなければなりません。また、彼らをコントリビューターとしてリストアップしておくことをおすすめします。

<!-- 
### The original developer is dead. Does that change anything?
 -->
### オリジナル開発者は亡くなっている。それで何か変わるの ?

<!-- 
Yes, but not how you’re thinking. You (obviously) can skip asking them for permissions first, but we actually reach out to the developers’ coworkers and teams to see if they want to continue maintaining the plugin. In some cases, a developer will ask us to permanently close their plugins in the event of their death. We respect their wishes.
 -->
はい。でも、あなたが考えているのとは違います。あなたは (もちろん) 最初に彼らに許可を求めることを省略できますが、私たちは実際に開発者の同僚やチームに連絡を取り、彼らがプラグインの保守を続けたいかどうかを確認します。開発者が亡くなった場合、そのプラグインを永久にクローズするよう私たちに依頼する場合もあります。私たちは、彼らの意思を尊重します。

<!-- 
### Why was my request denied?
 -->
### なぜ、リクエストが却下されたの ?

<!-- 
In cases where we deny an adoption, it’s usually for the following reasons.
 -->
私たちが引き継ぎを拒否する場合、たいていは次のような理由です。

<!-- 
- The requesting developer does not have the experience we feel the plugin requires
- The requested plugin is deemed high-risk
- The existing developer is a company or legal entity who owns the trademark
- The plugin has legal issues preventing us from from any transfers
- The requesting developer has had multiple guideline infractions
- The original developer asked us not to
 -->
- リクエストしている開発者が、そのプラグインに必要と思われる経験を持っていない
- リクエストされたプラグインは、リスクが高いと判断される
- 既存の開発者が、商標を所有している会社または法人である
- このプラグインには法的な課題があり、譲渡はできない
- リクエストしている開発者は、複数のガイドライン違反をしている
- オリジナル開発者が、私たちに譲渡しないよう要請した

<!-- 
If we don’t feel comfortable handing over a plugin, we will inform you as soon as possible.
 -->
プラグインをお渡しすることに納得がいかない場合は、できるだけ早くお知らせします。

<!-- 
There are rare cases where the plugin has already been given to new owners, but they have not yet deployed code. In general, if you’re told that a specific plugin is not available, there is a long history concerning the plugin preventing us from permitting takeover. In those cases, we recommend you submit your plugin as a fork.
 -->
まれに、プラグインがすでに新しい所有者に譲渡されているが、まだコードをデプロイしていない場合があります。一般的に、特定のプラグインが利用できないと言われた場合、そのプラグインに関する長い歴史があり、私たちが引き継ぎを許可できないことがあります。そのような場合は、プラグインをフォークして申請することをおすすめします。