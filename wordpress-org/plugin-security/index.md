<!--
# Managing Your Plugin's Security
-->

# プラグインのセキュリティ管理

<!--
The security of code in WordPress plugins is taken [very seriously](https://wordpress.org/about/security/).
-->

WordPress プラグインのコードのセキュリティは、[非常に慎重に](https://wordpress.org/about/security/)考慮されています。

<!--
[warning]If you have found a plugin with a security issue, please read [Reporting Plugin Security Issues](https://developer.wordpress.org/plugins/wordpress-org/plugin-security/reporting-plugin-security-issues/).[/warning]
-->

[warning]セキュリティの課題があるプラグインを見つけた場合は、[プラグインのセキュリティ課題を報告する](https://ja.wordpress.org/team/handbook/plugin-development/wordpress-org/plugin-security/reporting-plugin-security-issues/)をお読みください。[/warning]

<!--
When a plugin vulnerability is verified by the WordPress Security Team, they contact the plugin author and direct them as to how to fix and release a secure version of the plugin. If there is a lack of response from the plugin author or if the vulnerability is severe, the plugin/theme is pulled from the public directory, and in some cases, fixed and updated directly by the Security Team.
-->

WordPress セキュリティチームによってプラグインの脆弱性が確認されると、プラグイン作者に連絡し、修正方法と安全なバージョンのプラグインのリリースを指示します。プラグイン作者からの応答がない場合、または脆弱性が深刻な場合は、プラグイン/テーマは公開ディレクトリから引き抜かれ、場合によってはセキュリティチームによって直接修正・更新されます。

<!--
## Fixing Security Issues
-->

## セキュリティ課題の修正

<!--
When you receive a report of security issues in your plugins, it can be terrifying. First, don't panic. Everyone makes mistakes. What matters most is fixing it safely and promptly.
-->

プラグインにセキュリティの課題があるという報告を受けると、恐ろしくなります。まず、慌てないでください。誰にでもミスはあります。最も重要なのは、安全かつ迅速に修正することです。

<!--
1. Make sure you understand the report. If you're not sure what it means, ask for details. Even third-party reporters are usually willing to take the time to explain what's wrong and direct you where to research a proper fix.
2. Keep your changes as small as possible. This will make it much easier for you to review later on.
3. Test your plugin. Make sure the security fix doesn't break anything else. Make sure upgrading doesn't cause weird errors. Keep `WP_DEBUG` on and log any errors.
4. Document the issue in your change log. You don't need to include details on exactly what happened, but do document that a security issue was resolved.
5. Credit the reporter in your readme. This is just nice, and makes people more inclined to help you for free later on.
6. Bump your version number. We recommend [SemVer](https://semver.org/), so a security release for version 3.9 of your plugin would change the version to 3.9.1 and so on.
-->

1. 報告の内容をよく理解してください。意味がわからない場合は、詳細を尋ねてください。第三者の報告者であっても、通常は時間を割いて何が問題なのかを説明し、適切な修正方法を調べる場所を指示してくれます。
2. 変更はできるだけ最小限にとどめましょう。そうすることで、後で見直すのがずっと簡単になります。
3. プラグインをテストしましょう。セキュリティ修正が他の何かを壊していないことを確認してください。アップグレードによって変なエラーが発生しないことを確認してください。`WP_DEBUG` をオンにしておき、エラーがあればログに記録してください。
4. 変更ログに課題を記録しましょう。何が起きたかについて詳細を書く必要はありませんが、セキュリティの課題が解決されたことを記録してください。
5. readme に報告者についてクレジットしてください。これは単なる善意であり、のちのち、人々が無償であなたを助けようという気にさせるものです。
6. バージョン番号を上げましょう。私たちは [SemVer (semantic software versioning、意味論的ソフトウェア・バージョニング)](https://semver.org/) を推奨しているので、プラグインのバージョン3.9のセキュリティリリースはバージョンを3.9.1などに変更します。

<!--
## Automatic Plugin Security Updates
-->

## プラグインの自動セキュリティ・アップデート

<!--
Since WordPress 3.7, we have had the ability to push automatic security updates for plugins to fix critical vulnerabilities in plugins. Many sites have made use of the plugin automatic updates functionality, either by opting in directly through filters, or by using one of the many remote management services for WordPress that are available.
-->

WordPress 3.7以降、プラグインの重要な脆弱性を修正するために、プラグインの自動セキュリティアップデートをプッシュする機能が追加されました。多くのサイトが、フィルターを通して直接オプトインするか、利用可能な WordPress のリモート管理サービスのいずれかを使用して、プラグインの自動アップデート機能を利用しています。

<!--
In extreme situations, the Plugin Review Team and the WordPress Security Team may determine a plugin issue is great enough that it must be updated for all users. This is exceptionally rare, as the potential for conflicts is high.
-->

極端な状況では、プラグインレビューチームと WordPress セキュリティチームが、プラグインの課題が全ユーザーのためにアップデートしなければならないほど大きいと判断することがあります。これは競合の可能性が高いため、非常にまれなケースです。

<!--
The process of approving a plugin for an automatic update, and rolling it out to WordPress users, is highly manual. The security team reviews all code changes in the release, verifies the issue and the fix, and confirms the plugin is safe to trigger an update. Rolling out an automatic update requires modification and deployment of the API code. This is the same standard and process for a core security release.
-->

プラグインを自動アップデートの対象として承認し、WordPress ユーザーに展開するプロセスは、ほとんど手作業で行われます。セキュリティチームは、リリースのすべてのコード変更をレビューし、課題と修正を確認し、プラグインがアップデートを起動しても安全であることを確認します。自動アップデートの展開には、API コードの修正と配置が必要です。これは、コア・セキュリティリリースの標準およびプロセスと同じです。

<!--
### Criteria
-->

### 評価基準

<!--
The current criteria we take into consideration for a security push is a simple list:
-->

セキュリティ・プッシュのために考慮する、現在の評価基準は単純なリストです:

<!--
1. Has the security team been made aware of the issue?
2. How severe is the issue? What impact would it have on the security of a WordPress install, and the greater internet?
3. Is the fix for the issue self-contained or does it add significant extra superfluous code?
4. If multiple branches of the plugin are affected, has a release per branch been prepared?
5. Can the update be _safely_ installed automatically?
-->

1. セキュリティチームは、その課題を認知していますか ?
2. その課題は、どの程度深刻ですか ? WordPress や インターネット全体のセキュリティにどのような影響がありますか ?
3. 課題の修正は自己完結型ですか、それともかなり多くの過剰なコードを追加しますか ?
4. プラグインの複数のブランチが影響を受ける場合、ブランチごとのリリースは準備されていますか ?
5. アップデートは _安全に_ 自動的にインストールできますか ?

<!--
These requirements are defined in a way that anyone should be able to tick each box.
-->

これらの要件は、誰もがそれぞれのボックスにチェックを入れられるように定義されています。

<!--
The first criterion — making the security team aware of the issue — is critical. Since it's a tightly controlled process, the WordPress security team needs to be notified as early as possible. Letting us know is as simple as emailing us at `plugins@wordpress.org` with the details.
-->

最初の評価基準 — セキュリティ・チームに課題を認知させること — は、非常に重要です。厳重に管理されたプロセスであるため、WordPress のセキュリティチームにはできるだけ早く通知する必要があります。WordPress セキュリティチームへの通知は、`plugins@wordpress.org` までメールで詳細をお知らせいただくだけで、簡単に行うことができます。

<!--
The plugin and security teams will work with the plugin author (and the reporter, if different) to study the vulnerability and its exact exposure, verify the proposed fix, and determine what versions will be released and when.
-->

プラグイン・チームとセキュリティ・チームは、プラグイン作者 (異なる場合は報告者) と協力して、脆弱性とその正確な露出度を調査し、提案された修正を検証し、どのバージョンをいつリリースするかを決定します。

<!--
## FAQ
-->

## FAQ

<!--
### How do I request my plugin be automatically updated?
-->

### プラグインの自動アップデートをリクエストするには ?

<!--
If you feel your plugin has a large enough user base or the issue is of great significance, email `plugin@wordpress.org` **before** you push the code. Include a patch of the changes for review in the email, and explain why you feel this should be automated.
-->

あなたのプラグインに十分なユーザーベースがあるか、課題が非常に重要であると感じる場合は、コードをプッシュする **前に** `plugin@wordpress.org` にメールを送ってください。メールにはレビュー用の変更パッチを添付し、なぜ自動化する必要があるのかを説明してください。

<!--
### Can I include changes besides the security related ones for automated updates?
-->

### 自動アップデートの対象に、セキュリティ関連以外の変更を含めることは可能 ?

<!--
With few exceptions, no. A security push should _only_ be security related. We prefer (and many times require) plugin releases which fix **only** the security issue, with minimal code changes and with no unrelated changes.
-->

一部の例外を除いては、そうではありません。セキュリティ・プッシュはセキュリティに _だけ_ 関連すべきです。私たちは、セキュリティの課題 **だけ** を修正し、最小限のコード変更で、関連性のない変更を含まないプラグインのリリースを好みます (そして、多くの場合、それを要求します)。

<!--
This allows everyone to review the changes quickly and to be far more confident in them. Also it means there is a minimal amount of disruption on the part of the users.
-->

こうすることで、誰もが変更点をすばやく確認し、はるかに自信を持つことができます。また、ユーザー側の混乱も最小限に抑えられます。

<!--
### Why did plugin A get a automatic update, but plugin B didn't?
-->

### プラグイン A には自動アップデートが適用され、プラグイン B には適用されないのは、なぜ ?

<!--
It's not bias from WordPress.org, it's just a throwback to the manual process we've been using. If we're alerted to an issue, we'll work to handle it. If we find out several days later, the window of opportunity to get the fix rolled out has usually passed and it won't be as effective.
-->

WordPress.org のバイアスではなく、これまでの手動プロセスに戻っただけです。もし私たちが課題に対して警告を受けたら、それに応えようと努力します。数日後に問題が発覚した場合、通常、修正プログラムを展開する機会は過ぎており、自動アップデートを実施してもそれほど効果的ではありません。

<!--
### How can I disable automatic updates?
-->

### 自動アップデートを無効にするには ?

<!--
There are several options to disable this functionality. The article for [disabling core automatic updates](https://make.wordpress.org/core/2013/10/25/the-definitive-guide-to-disabling-auto-updates-in-wordpress-3-7/) applies here. Anything that disables all automatic update functionality will prevent plugin updates. If you only wish to disable plugin updates, whether for all plugins or a single plugin, you can do so with a single filter call.
-->

この機能を無効にするにはいくつかのオプションがあります。[コアの自動アップデートを無効にする](https://make.wordpress.org/core/2013/10/25/the-definitive-guide-to-disabling-auto-updates-in-wordpress-3-7/)の記事がこれに当てはまります。すべての自動更新機能を無効にすると、プラグインの更新ができなくなります。プラグインの更新だけを無効にしたい場合は、すべてのプラグインであれ、単一のプラグインであれ、1回のフィルター呼び出しで可能です。

<!--
### What if I can't (or don't want to) fix my code?
-->

### 自分のコードを修正できない (あるいは修正したくない) 場合は ?

<!--
You don't have to. Your plugin will remain closed and, after 2 or 3 months, the plugin page will report that it was closed for security issues. If you want to push a fix but keep the plugin closed, we can do that too. Just reply to the email and talk to us.
-->

その必要はありません。あなたのプラグインはクローズされたままとなり、2、3ヵ月後にプラグインのページに、セキュリティの課題でクローズされたことが報告されます。プラグインをクローズしたまま修正をプッシュしたい場合、私たちはそれも可能です。メールに返信して、私たちにご相談ください。

<!--
### Do I only have to fix the reported issue?
-->

### 報告された課題だけを修正すればいい ?

<!--
Yes and no. You _do_ have to fix the issues reported, but when you're done, the _entire_ plugin is re-reviewed, and if more issues are found, you'll be required to fix those as well. The ultimate goal is to make sure the reopened plugin is safe.
-->

Yes でもあり No でもあります。報告された課題は、修正 _しなければなりません_ が、それが終わるとプラグイン _全体_ が再レビューされ、さらに課題が見つかった場合は、それらも修正する必要があります。最終的な目標は、再開されたプラグインが安全であることを確認することです。

<!--
### What if I have guideline issues?
-->

### ガイドラインに課題がある場合は ?

<!--
This comes up when people are breaking other guidelines like including their own copy of jQuery or making undocumented external service calls. It depends on the severity of the other issues. If it's just your own jQuery, we'll likely let it be reopened and allow you to fix that at your own pace. If you're logging all installs of your plugins, you'll be required to correct that before we reopen the plugin.
-->

これは、jQuery の独自のコピーを入れたり、ドキュメント化されていない外部サービスを呼び出したりするなど、他のガイドラインを破っている場合に発生します。他の課題の重大性に拠ります。あなた自身の jQuery だけであれば、私たちはおそらくその課題を再開させ、あなた自身のペースで修正することを許可するでしょう。プラグインのすべてのインストールを記録している場合は、プラグインを再開する前に修正する必要があります。
