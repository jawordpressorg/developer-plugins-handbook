<!--
# Detailed Plugin Guidelines
-->

# 詳細なプラグイン・ガイドライン

<!--
[info]Adding a Block Only plugin? Please read the [Block Specific Guidelines](https://developer.wordpress.org/plugins/wordpress-org/block-specific-plugin-guidelines/).[/info]
-->

[info]ブロック専用プラグインを追加しますか ? [ブロック固有のガイドライン](https://developer.wordpress.org/plugins/wordpress-org/block-specific-plugin-guidelines/)をお読みください。[/info]

<!--
## The Plugin Directory
-->

## プラグイン・ディレクトリ

<!--
The goal of the WordPress Plugin Directory is to provide a safe place for all WordPress users – from the non-technical to the developer – to download plugins that are consistent with the goals of the WordPress project.
-->

WordPress プラグイン・ディレクトリの目的は、すべての WordPress ユーザー - 非技術者から開発者まで - が、WordPress プロジェクトの目標に沿ったプラグインをダウンロードできる安全な場所を提供することです。

<!--
To that end, we want to ensure a simple and transparent process for developers to submit plugins for the directory. As part of our ongoing efforts to make the plugin directory inclusion process more transparent, we have created a list of developer guidelines. We strive to create a level playing field for all developers.
-->

そのために、私たちは開発者がディレクトリにプラグインを申請するためのシンプルで透明なプロセスを確保したいと考えています。プラグインディレクトリの掲載プロセスをより透明なものにするための継続的な努力の一環として、開発者ガイドラインのリストを作成しました。私たちはすべての開発者が公平に利用できるように努力しています。

<!--
If you have suggestions to improve the guidelines, or questions about them, please email `plugins@wordpress.org` and let us know.
-->

ガイドラインを改善するための提案や、ガイドラインに関する質問がありましたら、`plugins@wordpress.org` までメールでお知らせください。

<!--
## Developer Expectations
-->

## 開発者への期待

<!--
Developers, all users with commit access, and all users who officially support a plugin are expected to abide by the following guidelines:
-->

開発者、コミットアクセス権を持つすべてのユーザー、そしてプラグインを公式にサポートするすべてのユーザーは、以下のガイドラインに従うことが期待されています:

<!--
- Plugin Directory Guidelines (this document)
- [Community Guidelines](https://make.wordpress.org/handbook/community-code-of-conduct/)
- [Forums Guidelines](https://wordpress.org/support/guidelines/) (should they use the forums/reviews)
-->

- プラグイン・ディレクトリ ガイドライン (本ドキュメント)
- [コミュニティ ガイドライン](https://make.wordpress.org/handbook/community-code-of-conduct/)
- [フォーラム ガイドライン](https://wordpress.org/support/guidelines/) (フォーラム/レビューを利用するべきか)

<!--
Violations may result in plugins or plugin data (for previously approved plugins) being removed from the directory until the issues are resolved. Plugin data, such as user reviews and code, may not be restored depending on the nature of the violation and the results of a peer-review of the situation. Repeat violations may result in all the author's plugins being removed and the developer being banned from hosting plugins on WordPress.org.
-->

違反があった場合、問題が解決されるまでプラグインまたはプラグインデータ (以前に承認されたプラグインの場合) がディレクトリから削除されることがあります。ユーザーレビューやコードなどのプラグインデータは、違反の内容や状況に対するピアレビューの結果によっては、復元されないことがあります。違反が繰り返されると、作者のすべてのプラグインが削除され、開発者は WordPress.org でのプラグインのホスティングが禁止される可能性があります。

<!--
It is the responsibility of the plugin developer to ensure their contact information on WordPress.org is up to date and accurate, in order that they receive all notifications from the plugins team. Auto-replies and emails that route to a support system are not permitted as they historically prevent humans from addressing emails in a timely fashion.
-->

プラグイン開発者の責任において、WordPress.org の連絡先情報が最新かつ正確であることを確認し、プラグインチームからのすべての通知を受け取れるようにしてください。サポートシステムへの自動返信やメールは、歴史的に人間がタイムリーにメールに対応することを妨げているため、許可されていません。

<!--
All code in the directory should be made as secure as possible. Security is the ultimate responsibility of the plugin developer, and the Plugin Directory enforces this to the best of our ability. Should a plugin be found to have security issues, it will be closed until the situation is resolved. In extreme cases the plugin may be updated by the WordPress Security team and propagated for the safety of the general public.
-->

ディレクトリ内のすべてのコードは、可能な限り、安全でなければなりません。セキュリティは、プラグイン開発者の最終的な責任であり、プラグイン・ディレクトリは、可能な限りこれを実施します。プラグインにセキュリティの問題があることが判明した場合、そのプラグインは、問題が解決するまでクローズされます。極端な場合、プラグインは WordPress セキュリティチームによって更新され、一般の人々の安全のために周知されるかもしれません。

<!--
While we attempt to account for as many relevant interpretations of the guidelines as possible, it is unreasonable to expect that every circumstance will be explicitly covered. If you are uncertain whether a plugin might violate the guidelines, please contact `plugins@wordpress.org` and ask.
-->

可能な限りガイドラインに関連する解釈を考慮しようとしていますが、すべての状況を明確にカバーすることを期待するのは不合理です。プラグインがガイドラインに違反するかどうか不明な場合は、`plugins@wordpress.org` までお問い合わせください。

<!--
## The Guidelines
-->

## ガイドライン

<!--
### 1. Plugins must be compatible with the GNU General Public License
-->

### 1. プラグインは、GNU GPL (General Public License。一般公衆利用許諾契約書) と互換性がなければならない。

<!--
Although any GPL-compatible license is acceptable, using the same license as WordPress — "GPLv2 or later" — is strongly recommended. All code, data, and images — anything stored in the plugin directory hosted on WordPress.org — must comply with the GPL or a GPL-Compatible license. Included third-party libraries, code, images, or otherwise, must be compatible. For a specific list of compatible licenses, please read the [GPL-Compatible license list](https://www.gnu.org/licenses/license-list.html#GPLCompatibleLicenses) on gnu.org.
-->

GPL 互換ライセンスであれば何でもかまいませんが、WordPress と同じライセンス —「GPLv2以降」— を使用することを強く推奨します。すべてのコード、データ、画像 (WordPress.org でホストされているプラグイン・ディレクトリに保存されているもの) は、GPL または GPL 互換ライセンスに準拠していなければなりません。含まれるサードパーティのライブラリ、コード、画像、その他は互換性がなければなりません。互換性のあるライセンスの具体的なリストについては、gnu.org の [GPL互換ライセンス・リスト](https://www.gnu.org/licenses/license-list.html#GPLCompatibleLicenses)をお読みください。

<!--
### 2. Developers are responsible for the contents and actions of their plugins
-->

### 2. 開発者は、そのプラグインの内容や動作に責任を負う。

<!--
It is the sole responsibility of plugin developers to ensure all files within their plugins comply with the guidelines. Intentionally writing code to circumvent guidelines, or restoring code they were asked to remove, is prohibited (see #9 illegal/dishonest actions).
-->

プラグイン内のすべてのファイルがガイドラインに準拠していることを確認するのは、プラグイン開発者自身の責任です。意図的にガイドラインを回避するコードを書いたり、削除を求められたコードを復元したりすることは禁止されています (ガイドライン「9: 違法/不正な行為」参照)。

<!--
Developers are expected to confirm, before uploading to SVN, the licensing of all included files, from original source code to images and libraries. In addition, they must comply to the terms of use for all third party services and APIs utilized by their plugins. If there is no way to validate the licensing of a library or the terms of an API, then they cannot be used.
-->

開発者は、SVN にアップロードする前に、オリジナルのソースコードから画像やライブラリに至るまで、含まれるすべてのファイルのライセンスを確認することが期待されています。さらに、プラグインが利用するすべてのサードパーティのサービスや API の利用規約を遵守しなければなりません。ライブラリのライセンスや API の利用規約を確認する方法がない場合、それらを使用できません。

<!--
### 3. A stable version of a plugin must be available from its WordPress Plugin Directory page
-->

### 3. プラグインの安定バージョンは、WordPress プラグイン・ディレクトリのページから入手可能でなければならない。

<!--
The only version of the plugin that WordPress.org distributes is the one in the directory. Though people may develop their code somewhere else, users will be downloading from the directory, not the development environment.
-->

WordPress.org が配布するプラグインのバージョンは、ディレクトリ内のものだけです。他の場所でコードを開発する人もいるかもしれませんが、ユーザーは、開発環境ではなく、ディレクトリからダウンロードすることになります。

<!--
Distributing code via alternate methods, while not keeping the code hosted here up to date, may result in a plugin being removed.
-->

ここでホストされているコードを最新の状態に保たないまま、別の方法でコードを配布すると、プラグインが削除される可能性があります。

<!--
### 4. Code must be (mostly) human readable
-->

### 4. コードは、(ほぼ) 人間が読めるものでなければならない。

<!--
Obscuring code by hiding it with techniques or systems similar to `p,a,c,k,e,r`'s obfuscate feature, uglify's mangle, or unclear naming conventions such as `$z12sdf813d`, is not permitted in the directory. Making code non-human readable forces future developers to face an unnecessary hurdle, as well as being a common vector for hidden, malicious code.
-->

`p,a,c,k,e,r` の難読化 (obfuscate) 機能や、uglify のマングル (mangle) 機能、あるいは `$z12sdf813d` のような意味不明な命名規則に類似した技術やシステムを使ってコードを隠蔽することは、このディレクトリでは許可されていません。コードを人間が読めないようにすることは、将来の開発者に不必要なハードルを強いるだけでなく、隠された悪意のあるコードの一般的な媒介になります。

<!--
We require developers to provide public, maintained access to their source code and any build tools in one of the following ways:
-->

私たちは開発者に、以下のいずれかの方法で、ソースコードとビルドツールへのメンテナンスされた公開アクセスの提供を求めます:

<!--
- Include the source code in the deployed plugin.
- A link in the readme to the development location.
-->

- 配布プラグインにソースコードを含める。
- 開発場所へのリンクを readme に記載する。

<!--
We strongly recommend you document how any development tools are to be used.
-->

開発ツールの使用方法をドキュメント化することを強く推奨します。

<!--
### 5. Trialware is not permitted
-->

### 5. トライアルウェア (試用版) は、許可されていない。

<!--
Plugins may not contain functionality that is restricted or locked, only to be made available by payment or upgrade. Functionality may not be disabled after a trial period or quota is met. In addition, plugins that provide sandbox only access to APIs and services are also trial, or test, plugins and not permitted.
-->

プラグインには、支払いまたはアップグレードによってのみ利用可能になる、制限またはロックされた機能を含めることはできません。試用期間またはクォータを満たした後に機能を無効にできません。さらに、API やサービスへのサンドボックスのみのアクセスを提供するプラグインも、トライアル、またはテスト用のプラグインであり、許可されません。

<!--
Paid functionality in services _is_ permitted (see guideline 6: serviceware), provided all the code inside a plugin is fully available. We recommend the use of add-on plugins, hosted outside of WordPress.org, in order to exclude the premium code. Situations where a plugin is intended as a developer tool only will be reviewed on a case by case basis.
-->

サービスにおける有料機能 _は_ 許可されています (ガイドライン「6: サービスウェア」参照) が、プラグイン内のすべてのコードが完全に利用可能であることが条件です。プレミアムコードを除外するために、WordPress.org の外部でホストされるアドオン・プラグインの使用を推奨します。プラグインが開発者用ツールとしてのみ意図されている状況では、ケースバイケースでレビューされます。

<!--
Attempting to upsell the user on ad-hoc products and features _is_ acceptable, provided it falls within bounds of guideline 11 (hijacking the admin experience).
-->

暫定的な商品や機能をユーザーに売り込もうとすること _は_、ガイドラインの範囲内であれば容認されます (「11: 管理者体験のハイジャック」参照)。

<!--
### 6. Software as a Service is permitted
-->

### 6. SaaS (Software as a Service。サービスとしてのソフトウェア) は、許可されている。

<!--
Plugins that act as an interface to some external third party service (e.g. a video hosting site) are allowed, even for paid services. The service itself must provide functionality of substance and be clearly documented in the readme file submitted with the plugin, preferably with a link to the service's Terms of Use.
-->

外部のサードパーティサービス (例: 動画ホスティングサイト) へのインターフェースとして動作するプラグインは、有料サービスであっても許可されます。そのサービス自体が実質的な機能を提供し、プラグインと一緒に提出される readme ファイルに明確にドキュメント化されていなければなりません。できれば、そのサービスの利用規約へのリンクがあることが望ましいです。

<!--
Services and functionality _not_ allowed include:
-->

許可され _ない_ サービスや機能は、以下の通りです:

<!--
- A service that exists for the sole purpose of validating licenses or keys while all functional aspects of the plugin are included locally is not permitted.
- Creation of a service by moving arbitrary code out of the plugin so that the service may falsely appear to provide supplemented functionality is prohibited.
- Storefronts that are not services. A plugin that acts only as a front-end for products to be purchased from external systems will not be accepted.
-->

- プラグインのすべての機能がローカルに含まれているにもかかわらず、ライセンスまたはキーの検証のみを目的として存在するサービスは、許可されません。
- プラグインから任意のコードを移動してサービスを作成し、サービスが補足機能を提供しているように見せかけることは、禁止されています。
- サービスではないストアフロント。外部システムから商品を購入するためのフロントエンドとしてのみ機能するプラグインは、認められません。

<!--
### 7. Plugins may not track users without their consent
-->

### 7. プラグインは、ユーザーの同意なしに追跡してはならない。

<!--
In the interest of protecting user privacy, plugins may not contact external servers without _explicit_ and authorized consent. This is commonly done via an 'opt in' method, requiring registration with a service or a checkbox within the plugin settings. Documentation on how any user data is collected, and used, should be included in the plugin's readme, preferably with a clearly stated privacy policy.
-->

ユーザーのプライバシーを保護するため、プラグインは _明示的_ で許可された同意なしに、外部サーバーに接続できません。これは一般的に「オプトイン」方式で行われ、サービスへの登録やプラグイン設定内のチェックボックスを必要とします。ユーザーデータがどのように収集され、どのように使用されるかについてのドキュメントは、プラグインの readme に含まれるべきです。できれば、プライバシーポリシーが明記されていることが望ましいです。

<!--
Some examples of prohibited tracking include:
-->

禁止されているトラッキングの例を、いくつか挙げます:

<!--
- Automated collection of user data without explicit confirmation from the user.
- Intentionally misleading users into submitting information as a requirement for use of the plugin itself.
- Offloading assets (including images and scripts) that are unrelated to a service.
- Undocumented (or poorly documented) use of external data (such as blocklists).
- Third-party advertisement mechanisms which track usage and/or views.
-->

- ユーザーの明示的な確認なしに、ユーザーデータを自動的に収集すること。
- プラグイン自体の使用要件として、意図的にユーザーを誤解させて情報を提出させること。
- サービスに関係のない (画像やスクリプトを含む) アセットをオフロードすること。
- ドキュメント化されていない (またはドキュメント化が不十分な) 外部データ (ブロックリストなど) の使用。
- 利用状況や閲覧数を追跡する、サードパーティの広告メカニズム。

<!--
An exception to this policy is Software as a Service, such as Twitter, an Amazon CDN plugin, or Akismet. By installing, activating, registering, and configuring plugins that utilize those services, consent is granted for those systems.
-->

このポリシーの例外は、Twitter、Amazon CDN プラグイン、Akismet などの SaaS (Software as a Service) です。これらのサービスを利用するプラグインをインストール、有効化、登録、設定することにより、これらのシステムに対する同意が付与されます。

<!--
### 8. Plugins may not send executable code via third-party systems
-->

### 8. プラグインは、サードパーティのシステムを介して、実行可能コードを送信することはできない。

<!--
Externally loading code from documented services is permitted, however all communication must be made as securely as possible. Executing outside code within a plugin when not acting as a service is not allowed, for example:
-->

ドキュメント化されたサービスからコードを読み込むことは許可されていますが、すべての通信は可能な限り安全に行われなければなりません。たとえば、サービスとして動作していないときに、プラグイン内で外部のコードを実行することは許可されていません:

<!--
- Serving updates or otherwise installing plugins, themes, or add-ons from servers other than WordPress.org's.
- Installing premium versions of the same plugin.
- Calling third party CDNs for reasons other than font inclusions; all non-service related JavaScript and CSS must be included locally.
- Using third party services to manage regularly updated lists of data, when not explicitly permitted in the service's terms of use.
- Using iframes to connect admin pages; APIs should be used to minimize security risks.
-->

- WordPress.org 以外のサーバーからプラグイン、テーマ、アドオンをインストールしたり、アップデート、その他を提供すること。
- 同じプラグインの、プレミアムバージョンのインストール。
- フォントのインクルード以外の理由でサードパーティの CDN を呼び出すこと。サービスに関連しない JavaScript と CSS は、すべてローカルに含める必要があります。
- サービスの利用規約で明示的に許可されていない場合に、定期的に更新されるデータのリストを管理するためにサードパーティのサービスを使用すること。
- 管理ページへの接続に iframe を使用すること。セキュリティリスクを最小限にするために、API を使用すること。

<!--
Management services that interact with and push software down to a site _are_ permitted, provided the service handles the interaction on it's own domain and not within the WordPress dashboard.
-->

そのサービスが WordPress ダッシュボード内ではなく独自のドメイン上でインタラクションを処理する場合に限り、サイトと相互作用し、ソフトウェアをプッシュダウンする管理サービス _は_ 許可されています。

<!--
### 9. Developers and their plugins must not do anything illegal, dishonest, or morally offensive
-->

### 9. 開発者とそのプラグインは、違法なこと、不正なこと、道徳に反することを行ってはならない。

<!--
While this is subjective and rather broad, the intent is to prevent plugins, developers, and companies from abusing the freedoms and rights of end users as well as other plugin developers.
-->

これは主観的でかなり広範なものですが、プラグインや開発者、企業がエンドユーザーや他のプラグイン開発者の自由や権利を乱用することを防ぐ意図があります。

<!--
This includes (but is not restricted to) the following examples:
-->

これには以下の例が含まれます (ただし、これに限定されるものではありません):

<!--
- Artificially manipulating search results via keyword stuffing, black hat SEO, or otherwise.
- Offering to drive more traffic to sites that use the plugin.
- Compensating, misleading, pressuring, extorting, or blackmailing others for reviews or support.
- Implying users must pay to unlock included features.
- Creating accounts to generate fake reviews or support tickets (i.e. sockpuppeting).
- Taking other developers' plugins and presenting them as original work.
- implying that a plugin can create, provide, automate, or guarantee legal compliance.
- Utilizing the user's server or resources without permission, such as part of a botnet or crypto-mining.
- Violations of the [WordPress.org Community Code of Conduct](https://make.wordpress.org/handbook/community-code-of-conduct/).
- Violations of the [WordCamp Code of Conduct](https://make.wordpress.org/community/handbook/wordcamp-organizer/planning-details/code-of-conduct/)
- Violations of the [Forum Guidelines](https://wordpress.org/support/guidelines/).
- Harassment, threats, or abuse directed at any other member of the WordPress community.
- Falsifying personal information to intentionally disguise identities and avoid sanctions for previous infractions.
- Intentionally attempting to exploit loopholes in the guidelines.
-->

- キーワードの詰め込み、ブラックハット SEO、その他によって検索結果を人為的に操作すること。
- プラグインを使用しているサイトにより、多くのトラフィック誘導を提案すること。
- レビューやサポートのために他者に報酬を与えたり、誤解を与えたり、圧力をかけたり、恐喝したり、脅迫したりすること。
- 含まれている機能をアンロックするために、ユーザーが課金しなければならないと示唆すること。
- 偽のレビューやサポートチケットを作成するためにアカウントを作成すること (すなわち、ソックパペット)。
- 他の開発者のプラグインを盗用して、オリジナルの作品であるかのように見せること。
- プラグインが法令遵守を作成、提供、自動化、保証できると示唆すること。
- ボットネットやクリプトマイニングの一部など、許可なくユーザーのサーバーやリソースを利用すること。
- [WordPress.org コミュニティ行動規範](https://make.wordpress.org/handbook/community-code-of-conduct/)への違反。
- [WordCamp 行動規範](https://make.wordpress.org/community/handbook/wordcamp-organizer/planning-details/code-of-conduct/)への違反。
- [フォーラム・ガイドライン](https://wordpress.org/support/guidelines/)への違反。
- WordPress コミュニティの他のメンバーに対する嫌がらせ、脅迫、虐待。
- 意図的に身元を偽り、過去の違反に対する制裁を避けるために、個人情報を改竄すること。
- ガイドラインの抜け穴を、意図的に利用しようとすること。

<!--
### 10. Plugins may not embed external links or credits on the public site without explicitly asking the user's permission
-->

### 10. プラグインは、ユーザーの許可を明示的に得ることなく、公開サイトに外部リンクやクレジットを埋め込むことはできない。

<!--
All "Powered By" or credit displays and links included in the plugin code must be optional and default to _not_ show on users' front-facing websites. Users must opt-in to displaying any and all credits and links via clearly stated and understandable choices, not buried in the terms of use or documentation. Plugins may not require credit or links be displayed in order to function. Services _are_ permitted to brand their output as they see fit, provided the code is handled in the service and not the plugin.
-->

プラグインコードに含まれるすべての「Powered By」あるいはクレジット表示とリンクは、オプショナルでなければならず、デフォルトではユーザーのフロント・フェイスの Web サイトには表示 _しない_ ようになっていなければなりません。ユーザーは、利用規約やドキュメントに埋もれることなく、明示されたわかりやすい選択肢によって、クレジットやリンクを表示することに同意しなければなりません。プラグインは、機能するためにクレジットやリンクの表示を要求できません。サービスは、コードをプラグインではなくサービス内で処理することを条件に、適切と思われるようにその出力をブランド化すること _が_ 認められます。

<!--
### 11. Plugins should not hijack the admin dashboard
-->

### 11. プラグインは、管理画面のダッシュボードを乗っ取らないこと。

<!--
Users prefer and expect plugins to feel like part of WordPress. Constant nags and overwhelming the admin dashboard with unnecessary alerts detract from this experience.
-->

ユーザーは、プラグインが WordPress の一部のように感じられることを好み、期待しています。常に煩わしく、不必要なアラートで管理ダッシュボードを圧迫することは、この体験を台なしにしてしまうでしょう。

<!--
Upgrade prompts, notices, alerts, and the like must be limited in scope and used sparingly, be that contextually or only on the plugin's setting page. Site wide notices or embedded dashboard widgets _must_ be dismissible or self-dismiss when resolved. Error messages and alerts must include information on how to resolve the situation, and remove themselves when completed.
-->

アップグレードのプロンプト、通知、アラートなどは範囲を限定し、文脈上であれ、プラグインの設定ページのみであれ、控えめに使用しなければなりません。サイト全体の通知やダッシュボードに埋め込まれたウィジェットは、解決されたときに解除または自己解除が可能でなければ _なりません_。エラーメッセージやアラートには、その状況を解決するための情報が含まれていなければなりませんし、完了したら自動的に削除されなければなりません。

<!--
Advertising within the WordPress dashboard should be avoided, as it is generally ineffective. Users normally only visit settings pages when they're trying to solve a problem. Making it harder to use a plugin does not generally encourage a good review, and we recommend limiting any ads placed therein. Remember: tracking referrals via those ads is not permitted (see guideline 7) and most third-party systems do not permit back-end advertisements. Abusing the guidelines of an advertising system will result in developers being reported upstream.
-->

WordPress ダッシュボード内の広告は、一般的に効果がないため避けるべきです。ユーザーは通常、問題を解決しようとしているときにしか設定ページを訪れません。プラグインを使いにくくすることは、一般的に良いレビューを促すことにはならないので、そこに掲載される広告は制限することをおすすめします。覚えておいてください: 広告を経由した紹介を追跡することは、許可されていません (ガイドライン「7」参照) し、ほとんどのサードパーティ・システムは、バックエンド広告を許可していません。広告システムのガイドラインを逸脱すると、開発者は上流に報告されることになります。

<!--
Developers are welcome and encouraged to include links to their own sites or social networks, as well as locally (within the plugin) including images to enhance that experience.
-->

開発者は、自分のサイトやソーシャルネットワークへのリンクを含めてもかまいませんし、むしろ奨励されます。また同様に、体験を向上するためにローカルに (プラグイン内に) 画像を含めることも奨励されます。

<!--
### 12. Public facing pages on WordPress.org (readmes) must not spam
-->

### 12. WordPress.org の公開ページ (readmes) は、スパムであってはならない。

<!--
Public facing pages, including readmes and translation files, may not be used to spam. Spammy behavior includes (but is not limited to) unnecessary affiliate links, tags to competitors plugins, use of over 12 tags total, blackhat SEO, and keyword stuffing.
-->

readme や翻訳ファイルを含む公開ページは、スパム目的に使用できません。スパム行為には、不必要なアフィリエイトリンク、競合プラグインへのタグ付け、合計12以上のタグの使用、ブラックハット SEO、キーワードの詰め込みなどが含まれますが、これらに限定されません。

<!--
Links to directly required products, such as themes or other plugins required for the plugin's use, are permitted within moderation. Similarly, related products may be used in tags but not competitors. If a plugin is a WooCommerce extension, it may use the tag 'woocommerce.' However if the plugin is an alternative to Akismet, it may not use that term as a tag. Repetitive use of a tag or specific term is considered to be keyword stuffing, and is not permitted.
-->

プラグインの使用に必要なテーマや他のプラグインなど、直接必要な製品へのリンクは、節度ある範囲で許可されます。同様に、関連製品はタグで使用できますが、競合製品は使用できません。プラグインが WooCommerce の拡張機能である場合、「woocommerce」というタグを使うことができます。ただし、プラグインが Akismet の代替である場合は、タグとして Akismet というタームを使用できません。タグや特定の用語を繰り返し使用することは、キーワードの詰め込みとみなされ、許可されません。

<!--
Readmes are to be written for people, not bots.
-->

Readme は、bot ではなく、人間のために書かれるべきものです。

<!--
In all cases, affiliate links must be disclosed and must directly link to the affiliate service, not a redirect or cloaked URL.
-->

すべての場合において、アフィリエイトリンクは開示されなければならず、リダイレクトや偽装された URL ではなく、アフィリエイトサービスに直接リンクされていなければなりません。

<!--
### 13. Plugins must use WordPress' default libraries
-->

### 13. プラグインは、WordPress のデフォルトライブラリを使用しなければならない。

<!--
WordPress includes a number of useful libraries, such as jQuery, Atom Lib, SimplePie, PHPMailer, PHPass, and more. For security and stability reasons plugins may not include those libraries in their own code. Instead plugins must use the versions of those libraries packaged with WordPress.
-->

WordPress には、jQuery、Atom Lib、SimplePie、PHPMailer、PHPass などの便利なライブラリが多数含まれています。セキュリティと安定性の理由から、プラグインはこれらのライブラリを独自のコードに含めることはできません。代わりに、プラグインは WordPress に同梱されているバージョンのライブラリを使用しなければなりません。

<!--
For a list of all javascript libraries included in WordPress, please review [Default Scripts Included and Registered by WordPress](https://developer.wordpress.org/reference/functions/wp_enqueue_script/#notes).
-->

WordPress に含まれるすべての JavaScript ライブラリのリストについては、[WordPress に含まれ登録されているデフォルトのスクリプト](https://developer.wordpress.org/reference/functions/wp_enqueue_script/#notes)をご覧ください。

<!--
### 14. Frequent commits to a plugin should be avoided
-->

### 14. プラグインへの頻繁なコミットは、避けるべきである。

<!--
The SVN repository is a release repository, not a development one. All commits, code or readme files, will trigger a regeneration of the zip files associated with the plugin, so only code that is ready for deployment (be that a stable release, beta, or RC) should be pushed to SVN. Including a descriptive and informative message with each commit is strongly recommended. Frequent 'trash' commit messages like 'update' or 'cleanup' makes it hard for others to follow changes. Multiple, rapid-fire commits that only tweak minor aspects of the plugin (including the readme) cause undue strain on the system and can be seen as gaming Recently Updated lists.
-->

SVN リポジトリは、リリースリポジトリであり、開発用ではありません。コードであれ readme ファイルであれ、すべてのコミットはプラグインに関連する zip ファイルを再生成するトリガーとなるので、配布準備が整ったコード (安定版リリース、ベータ版、リリース候補版を問いません) だけを SVN にプッシュしてください。各コミットには、説明的で有益なメッセージを含めることを強く推奨します。「update」や「cleanup」のような「trash」コミットメッセージが頻繁にあると、他の人が変更を追うのが難しくなります。(readme を含む) プラグインの些細な部分を調整しただけの、複数の連発コミットは、システムに過度の負担をかけ、最近更新されたリストがゲーム化しているように見えることがあります。

<!--
An exception to this is when readme files are updated solely to indicate support of the latest release of WordPress.
-->

この例外は、WordPress の最新リリースのサポートを示すためだけに readme ファイルが更新される場合です。

<!--
### 15. Plugin version numbers must be incremented for each new release
-->

### 15. プラグインのバージョン番号は、新規リリースの都度インクリメントしなければならない。

<!--
Users are only alerted to updates when the plugin version is increased. The trunk readme.txt must always reflect the current version of the plugin. For more information on tagging, please read our [SVN directions on tagging](https://developer.wordpress.org/plugins/wordpress-org/how-to-use-subversion/#tags) and [how the readme.txt works](https://developer.wordpress.org/plugins/wordpress-org/how-your-readme-txt-works/).
-->

ユーザーは、プラグインのバージョンが上がったときだけ、アップデートを通知されます。trunk の readme.txt は、常にプラグインの現在のバージョンを反映しなければなりません。tag 付けの詳細については、[tag 付けに関する SVN の指示](https://developer.wordpress.org/plugins/wordpress-org/how-to-use-subversion/#tags)と [readme.txt の仕組み](https://developer.wordpress.org/plugins/wordpress-org/how-your-readme-txt-works/)をお読みください。

<!--
### 16. A complete plugin must be available at the time of submission
-->

### 16. 申請時に、完全なプラグインが利用可能であること。

<!--
All plugins are examined prior to approval, which is why a zip file is required. Names cannot be "reserved" for future use or to protect brands (see #17: respect brands). Directory names for approved plugins that are not used may be given to other developers.
-->

すべてのプラグインは承認前に検査されます。そのため zip ファイルが必要です。将来の使用やブランド保護のために名前を「予約」できません (ガイドライン「17: ブランドを尊重する」参照)。承認されたプラグイン用のディレクトリ名で、使用されていないものは、他の開発者に譲ることができます。

<!--
### 17. Plugins must respect trademarks, copyrights, and project names
-->

### 17. プラグインは、商標、著作権、プロジェクト名を尊重しなければならない。

<!--
The use of trademarks or other projects as the sole or initial term of a plugin slug is prohibited unless proof of legal ownership/representation can be confirmed. For example, the [WordPress Foundation has trademarked the term "WordPress"](https://wordpressfoundation.org/trademark-policy/) and it is a violation to use "wordpress" in a domain name. This policy extends to plugin slugs, and we will not permit a slug to begin with another product's term.
-->

商標やその他のプロジェクトを、プラグインのスラッグの単独または初期タームとして使用することは、法的な所有権/代理権の証明が確認できない限り禁止されています。たとえば、[WordPress Foundation は「WordPress」というタームを商標登録しています](https://wordpressfoundation.org/trademark-policy/)し、ドメイン名に「WordPress」を使用することは違反です。このポリシーはプラグインのスラッグにも適用され、他の製品のタームで始まるスラッグは許可されません。

<!--
For example only employees of Super Sandbox should use the slug "super-sandbox," or their brand in a context such as "Super Sandbox Dancing Sloths." Non-employees should use a format such as "Dancing Sloths for Superbox" instead to avoid potentially misleading users into believing the plugin was developed by Super Sandbox. Similarly, if you don't represent the "MellowYellowSandbox.js" project, it's inappropriate to use that as the name of your plugin.
-->

たとえば、Super Sandbox の従業員のみが、「super-sandbox」というスラッグや、「Super Sandbox Dancing Sloths」のような文脈で、彼らのブランドを使用すべきです。非従業員は、プラグインが Super Sandbox によって開発されたとユーザーに誤解を与える可能性を避けるために、代わりに「Dancing Sloths for Superbox」のようなフォーマットを使うべきです。同様に、もしあなたが「MellowYellowSandbox.js」プロジェクトを代表していないのであれば、それをプラグインの名前として使うのは不適切です。

<!--
Original branding is recommended as it not only helps to avoid confusion, but is more memorable to the user.
-->

オリジナル・ブランディングは、混乱を避けるだけでなく、ユーザーの記憶に残りやすいので推奨されます。

<!--
### 18. We reserve the right to maintain the Plugin Directory to the best of our ability
-->

### 18. 私たちは、可能な限りプラグイン・ディレクトリを維持する権利を保有するものとする。

<!--
Our intent is to enforce these guidelines with as much fairness as humanly possible. We do this to ensure overall plugin quality and the safety of their users. To that end, we reserve the following rights:
-->

私たちの意図は、できるだけ人道的に公平に、これらのガイドラインを実施することです。これは、プラグイン全体の品質とユーザーの安全を確保するためです。そのために、私たちは以下の権利を保持します:

<!--
- ...to update these guidelines at any time.
- ...to disable or remove any plugin from the directory, even for reasons not explicitly covered by the guidelines.
- ...to grant exceptions and allow developers time to address issues, even security related.
- ...to remove developer access to a plugin in lieu of a new, active, developer.
- ...to make changes to a plugin, without developer consent, in the interest of public safety.
-->

- …このガイドラインは、いつでも更新できます。
- …ガイドラインに明示されていない理由であっても、プラグインを無効にしたり、ディレクトリから削除したりができます。
- …たとえセキュリティに関連する問題であっても、例外を認めて、開発者に対処する時間を与えることです。
- …プラグインに対する開発者のアクセス権を削除し、新たに活動する開発者に代えること。
- …公共の安全のために、開発者の同意なしにプラグインに変更を加えること。

<!--
In return, we promise to use those rights sparingly and with as much respect as possible for both end users and developers.
-->

その見返りとして、私たちはこれらの権利を控えめに、そしてエンドユーザーと開発者の双方に可能な限り敬意を払って使用することを約束します。
