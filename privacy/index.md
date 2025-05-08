<!--
# Privacy
-->

# プライバシー

<!--
Are you writing a plugin that handles personal data – things like names, addresses, and other things that can be used to identify a person? You'll want to take care with that data and protect the privacy of your users and visitors.
-->

個人データ - 名前や住所など、個人を特定できるようなもの - を扱うプラグインを書いていますか ? そのようなデータには注意を払い、ユーザーや訪問者のプライバシーを保護したいと思うでしょう。

<!--
## What is Privacy?
-->

## プライバシーとは ?

<!--
WordPress.org made several enhancements ahead of Europe's General Data Protection Regulation. Following the launch of this work, we have made Privacy a permanent focus in core trac development, which will allow us to continue making enhancements on privacy and data protection outside specific legislation.
-->

WordPress.org は、ヨーロッパの一般データ保護規則 (General Data Protection Regulation、略して GDPR) に先立ち、いくつかの機能強化を行いました。この作業の開始後、私たちはプライバシーを trac のコア開発における恒久的な焦点とし、特定の法律以外でもプライバシーとデータ保護に関する機能強化を継続できるようにしました。

<!--
But what kind of issues might fall under the definition of "privacy", and how do we define it? Although privacy requirements vary widely across countries, cultures, and legal systems, there are several general principles applicable across any situation:
-->

しかし、どのような問題が「プライバシー」の定義の対象となり、そして、どのように定義すればよいのでしょうか ? プライバシーの要件は国や文化、法制度によって大きく異なりますが、どのような状況でも適用できる一般原則がいくつかあります:

<!--
- **Consent and choice:** giving users (and site visitors) choices and options over the uses of their data, and requiring clear, specific, and informed opt-in;
- **Purpose legitimacy and specification:** only collect and use the personal data for the purpose it was intended for, and for which the user was clearly informed of in advance;
- **Collection limitation:** only collect the user data which is needed; don't make extra copies of data or combine your data with data from other plugins if you can avoid it;
- **Data minimization:** restrict the processing of data, as well as the number of people who have access to it, to the minimum uses and people necessary;
- **Use, retention and disclosure limitation:** delete data which is no longer needed, both in active use and in archives, by both the recipient and any third parties;
- **Accuracy and quality:** ensure that the data collected and used is correct, relevant, and up-to-date, especially if inaccurate or poor data could adversely impact the user;
- **Openness, transparency and notice:** inform users how their data is being collected, used, and shared, as well as any rights they have over those uses;
- **Individual participation and access:** give users a means to access or download their data;
- **Accountability:** documenting the uses of data, protecting it in transit and in use by third parties, and preventing misuse and breaches as much as is possible;
- **Information security:** protecting data through appropriate technical and security measures;
- **Privacy compliance:** ensuring that the work meets the privacy regulations of the location where it will be used to collect and process people's data.
-->

- **同意と選択:** ユーザー (およびサイト訪問者) にデータの使用に関する選択肢とオプションを与え、明確で具体的、かつ十分な情報にもとづいたオプトインを要求すること;
- **目的の正当性とその範囲:** 個人データを収集し利用するのは、それが意図され、利用者に事前に明確に通知された目的のためだけです。
- **収集の制限:** 必要なユーザーデータのみを収集します; 避けられる場合、データの余分なコピーを作成したり、他のプラグインからのデータとあなたのデータを組み合わせたりしません。
- **データの最小化:** データの処理とそれにアクセスできる人の数を、必要最小限の用途と人に制限します。
- **使用、保持および開示の制限:** 現行使用およびアーカイブの両方において、受信者と第三者の両方によって、不要となったデータは削除されます。
- **正確性と品質:** 特に、不正確または不十分なデータが利用者に悪影響を及ぼす可能性がある場合は、収集され使用されるデータが正しく、適切で、最新のものであることを保証すること。
- **公開性、透明性および通知:** 自分のデータがどのように収集、使用、共有されているか、また、それらの使用に関してユーザーが有する権利をユーザーに通知します。
- **個人の参加とアクセス:** ユーザーが自分のデータにアクセスしたり、ダウンロードしたりする手段を提供します。
- **説明責任:** データの使用をドキュメント化し、転送中および第三者による使用中のデータを保護し、誤用や違反を可能な限り防止します。
- **情報セキュリティ:** 適切な技術的およびセキュリティ対策によって、データを保護すること。
- **プライバシー遵守:** 個人情報の収集および処理に使用される場所の、プライバシー規定に適合していることを確認します。

<!--
(Source: [ISO 29100/Privacy Framework standard](https://www.iso.org/standard/45123.html))
-->

(出典: [ISO 29100/プライバシー・フレームワーク標準](https://www.iso.org/standard/45123.html))

<!--
While not all of these principles will be applicable across all situations and uses, using them in the development process can help to ensure user trust.
-->

これらの原則のすべてが、すべての状況や用途に適用できるわけではないが、開発プロセスで使用することで、ユーザーの信頼を確保できます。

<!--
## Privacy By Design
-->

## 設計によるプライバシー

<!--
Many of these principles are espoused in the Privacy by Design framework, which states that:
-->

これらの原則の多くは、「設計によるプライバシー」フレームワークで支持されており、以下のように提唱されています:

<!--
- Privacy should be proactive, not reactive, and must anticipate privacy issues before they reach the user. Privacy must also be preventative, not remedial.
- Privacy should be the default setting. The user should not have to take actions to secure their privacy, and consent for data sharing should not be assumed.
- Privacy should be built into design as a core function, not an add-on.
- Privacy should be positive sum: there should be no trade-off between privacy and security, privacy and safety, or privacy and service provision.
- Privacy should offer end-to-end lifecycle protection through data minimization, minimal data retention, and regular deletion of data which is no longer required.
- The privacy standards used on your plugin (and service, if applicable) should be visible, transparent, open, documented and independently verifiable.
- Privacy should be user-centric. People should be given options such as granular privacy choices, maximized privacy defaults, detailed privacy information notices, user-friendly options, and clear notification of changes.
-->

- プライバシーは、事後的なものではなく、事前的なものであるべきで、プライバシーに関する問題がユーザーに到達する前に、それを予測しなければなりません。また、プライバシーは、改善策ではなく、予防策でなければなりません。
- プライバシーは、デフォルト設定であるべきです。ユーザーは、プライバシーを確保するために行動を起こす必要はなく、データ共有の同意は前提とされるべきではありません。
- プライバシーは、アドオンではなく、コア機能として設計に組み込まれるべきです。
- プライバシーは、非ゼロサム (互いが利益を得る) であるべきです。プライバシーとセキュリティ、プライバシーと安全性、プライバシーとサービス提供の間にトレードオフがあってはなりません。
- プライバシーは、データの最小化、最小限のデータ保持、不要になったデータの定期的な削除を通じて、エンドツーエンドのライフサイクル保護を提供すべきです。
- プラグイン (および該当する場合はサービス) で使用されるプライバシー標準は、可視化され、透明性があり、オープンで、ドキュメント化され、独立して検証可能であるべきです。
- プライバシーは、ユーザー中心であるべきです。きめ細かなプライバシーの選択、最大化されたプライバシーのデフォルト設定、詳細なプライバシー情報の通知、ユーザーフレンドリーなオプション、明確な変更通知などのオプションが、人々に与えられるべきです。

<!--
## Food for Thought for Your Plugin
-->

## プラグインを考えるための糧

<!--
To help your plugin be ready, we recommend going through the following list of questions for every plugin that you make:
-->

プラグインを準備するために、プラグインを作成する都度、以下の質問リストを確認することをおすすめします:

<!--
1. How does your plugin handle personal data? Use [`wp_add_privacy_policy_content()`](https://developer.wordpress.org/reference/functions/wp_add_privacy_policy_content/) to disclose to your users any of the following:
	- Does the plugin share personal data with third parties (e.g. to outside APIs/servers). If so, what data does it share with which third parties and do they have a published privacy policy you can provide a link to?
	- Does the plugin collect personal data? If so, what data and where is it stored? Think about places like user data/meta, options, post meta, custom tables, files, etc.
	- Does the plugin use personal data collected by others? If so, what data? Does the plugin pass personal data to a SDK? What does that SDK do with the data?
	- Does the plugin collect telemetry data, directly or indirectly? Loading an image from a third-party source on every install, for example, could indirectly log and track the usage data of all of your plugin installs.
	- Does the plugin enqueue Javascript, tracking pixels or embed iframes from a third party (third party JS, tracking pixels and iframes can collect visitor's data/actions, leave cookies, etc.)?
	- Does the plugin store things in the browser? If so, where and what? Think about things like cookies, local storage, etc.
2. If your plugin collects personal data…
	- Does it provide a personal data exporter?
	- Does it provide a personal data eraser callback?
	- For what reasons (if any) does the plugin refuse to erase personal data? (e.g. order not yet completed, etc) – those should be disclosed as well.
3. Does the plugin use error logging? Does it avoid logging personal data if possible? Could you use things like [`wp_privacy_anonymize_data()`](https://developer.wordpress.org/reference/functions/wp_privacy_anonymize_data/) to minimize the personal data logged? How long are log entries kept? Who has access to them?
4. In wp-admin, what role/capabilities are required to access/see personal data? Are they sufficient?
5. What personal data is exposed on the front end of the site by the plugin? Does it appear to logged-in and logged-out users? Should it?
6. What personal data is exposed in REST API endpoints by the plugin? Does it appear to logged-in and logged-out users? What roles/capabilities are required to see it? Are those appropriate?
7. Does the plugin properly remove/clean-up data, including especially personal data:
	- During uninstall of the plugin?
	- When a related item is deleted (e.g. from the post meta or any post-referencing rows in another table)?
	- When a user is deleted (e.g. from any user referencing rows in a table)?
8. Does the plugin provide controls to reduce the amount of personal data required?
9. Does the plugin share personal data with SDKs or APIs only when the SDK or API requires it, or is the plugin also sharing personal data that is optional?
10. Does the amount of personal data collected or shared by this plugin change when certain other plugins are also installed?
-->

1. あなたのプラグインは、個人情報をどのように扱いますか ? [`wp_add_privacy_policy_content()`](https://developer.wordpress.org/reference/functions/wp_add_privacy_policy_content/) を使用して、以下のいずれかをユーザーに開示してください:
	- プラグインは、個人情報を第三者 (たとえば、外部の API/サーバーなど) と共有しますか ? もしそうであれば、どのようなデータをどのような第三者と共有し、その第三者には、リンクを提供できるような公開されたプライバシーポリシーがありますか ?
	- ラグインは個人情報を収集しますか ? もしそうなら、どのようなデータをどこに格納していますか ? ユーザーデータ/メタ、オプション、投稿メタ、カスタムテーブル、ファイルなどの場所を考えてください。
	- プラグインは、他者が収集した個人情報を使用しますか ? もしそうなら、どのようなデータですか ? プラグインは、個人情報を SDK に渡しますか ? SDK は、そのデータで何をしますか ?
	- プラグインは、直接または間接的に遠隔測定データを収集しますか ? たとえば、インストールするたびに第三者のソースから画像を読み込むと、間接的にログに記録され、インストールしたすべてのプラグインの利用データが追跡される可能性があります。
	- プラグインは、第三者からの Javascript、トラッキングピクセル、iframe をエンキューしますか (第三者の Javascript、トラッキングピクセル、iframe は、訪問者のデータ/アクションを収集したり、Cookie を残したりできます) ?
	- プラグインは、ブラウザに何かを格納するのですか ? もしそうなら、どこに何を格納しますか ? Cookie やローカルストレージなどについて考えてください。
2. プラグインが、個人情報を収集する場合…
	- 個人データ・エクスポーターを提供していますか ?
	- 個人データ・イレーザー・コールバックを提供していますか ?
	- プラグインは、(もしあれば) どのような理由で個人情報の消去を拒否しますか ? (たとえば、注文が完了していないなど) - これらについても開示する必要があります。
3. プラグインは、エラーログを使用しますか ? 可能であれば、個人情報のログを避けていますか ? [`wp_privacy_anonymize_data()`](https://developer.wordpress.org/reference/functions/wp_privacy_anonymize_data/) のようなものを使って、個人情報のログを最小限にできますか ? ログの保存期間は ? 誰がアクセスできますか ?
4. wp-admin で、個人情報にアクセス/閲覧するために必要な権限グループ/権限は何ですか ? それらは十分ですか ?
5. プラグインによって、サイトのフロントエンドで、どのような個人情報が公開されますか ? ログインしているユーザー、ログアウトしているユーザーに表示されますか ? 表示されるべきですか ?
6. プラグインによって REST API エンドポイントにどのような個人情報が公開されますか ? ログインしているユーザー、ログアウトしているユーザーに表示されますか ? それを見るにはどのような権限グループ/権限が必要ですか ? それらは適切ですか ?
7. プラグインは、特に個人情報を含むデータを適切に削除/後始末していますか:
	- プラグインのアンインストール時 ?
	- 関連項目が削除されたとき (たとえば、投稿メタや他のテーブルの投稿参照行から) ?
	- ユーザーが削除されたとき (たとえば、テーブルのユーザー参照行から) ?
8. プラグインは、必要な個人情報の量を減らすためのコントロールを提供していますか ?
9. プラグインは、SDK または API が要求する場合にのみ個人情報を SDK または API と共有しますか ? または、プラグインは、任意である個人情報も共有しますか ?
10. 他のプラグインもインストールされている場合、このプラグインによって収集または共有される個人情報の量は変化しますか ?

<!--
## External Resources
-->

## 外部リソース

<!--
* [Privacy Blog](https://privacy.blog/)
* [WordPress.org Privacy Policy](https://wordpress.org/about/privacy/)
-->

* [プライバシー・ブログ](https://privacy.blog/)
* [WordPress.org プライバシー・ポリシー](https://wordpress.org/about/privacy/)
