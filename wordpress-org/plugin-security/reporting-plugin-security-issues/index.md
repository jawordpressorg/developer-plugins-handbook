<!-- 
# Reporting Plugin Security Issues
 -->
# プラグインのセキュリティ課題を報告する

<!-- 
[warning]Please do not report security issues with WordPress Core to the plugin team. To report an issue with WordPress itself, [follow the directions for reporting security vulnerabilities.](https://make.wordpress.org/core/handbook/testing/reporting-security-vulnerabilities/)[/warning]
 -->
[warning]WordPress Core のセキュリティ課題をプラグインチームに報告しないでください。WordPress 自体の課題を報告するには、[セキュリティー脆弱性の報告に関する手順に従ってください](https://make.wordpress.org/core/handbook/testing/reporting-security-vulnerabilities/)。[/warning]

<!-- 
If you find a plugin with a security issue, please **do not** post about it publicly anywhere. Even if there’s a report filed on one of the official security tracking sites, bringing more awareness to the security issue tends to increase people being hacked, and rarely speeds up the fixing.
 -->
セキュリティ上の課題があるプラグインを見つけた場合、それについて公に投稿 **しないでください**。たとえ公式のセキュリティ追跡サイトに報告があったとしても、セキュリティの課題を広く認識させることは、ハッキングされる人を増加させる傾向があるだけであり、修正が早まることはほとんどありません。

<!-- 
To report a plugin, please email `plugins@wordpress.org` with the following:
 -->
プラグインを報告するには、`plugins@wordpress.org` に以下の内容を e メールで連絡してください:

<!-- 
- a clear and concise description of the issue
- a link to the specific plugin
- whether or not you have validated the security issue yourself
- **optional** – links to any public disclosures on 3rd party sites
 -->
- 課題についての、明確で簡潔な説明
- 当該プラグインへのリンク
- あなた自身が、セキュリティ課題を検証したか否か
- **任意** – 第三者サイトで公に開示されている情報へのリンク

<!-- 
In the case of serious exploits, please keep in mind responsible and reasonable disclosure. Every attempt to contact the developer directly should be made _before_ you reported the plugin to us (though we understand this can be difficult – check in the source code of the plugin first, many developers list their emails). If you cannot contact them privately, please contact us directly and we’ll help out.
 -->
深刻な脆弱性の場合は、責任ある合理的な情報開示を心掛けてください。プラグインを私たちに報告する _前に_、開発者に直接連絡するあらゆる試みを行う必要があります (難しいとは理解していますけれども – 多くの開発者が e メールアドレスを掲載しているので、まずはプラグインのソースコードを確認してください)。個人的に連絡できない場合は、私たちに直接ご連絡くだされば、お手伝いします。

<!-- 
Most plugins are closed to prevent new downloads until the issue is resolved. As such, you may _not_ be alerted of a fix until the plugin is updated. We also **do not** provide assistance with filing CVEs at this time, due to a lack of resources. You’re welcome to do so on your own, but we cannot help you.
 -->
ほとんどのプラグインは、課題が解決されるまで新しいダウンロードができないようにクローズされます。その為、プラグインが更新されるまで、修正されたことが通知 _されない_ 可能性があります。また、リソースが不足しているため、現時点では CVE (Common Vulnerabilities and Exposures、共通脆弱性識別子データベース) のファイリングに関する支援も提供 **していません**。ご自身で CVE を申請されるのは自由ですが、私たちはお手伝いできません。

<!-- 
If you’ve already posted the vulnerability in public and provided a link to your report, please do not delete it! We will pass it on directly to the developers of the plugin.
 -->
すでに脆弱性を公開で投稿し、報告へのリンクを提供している場合は、削除しないでください ! プラグインの開発者宛に直接転送します。