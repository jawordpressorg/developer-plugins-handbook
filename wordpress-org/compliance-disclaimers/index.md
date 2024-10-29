<!-- 
# Compliance Disclaimers
 -->
# コンプライアンスに関する免責事項

<!-- 
As of **April 12, 2018**, [Guideline 9](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/#9-developers-and-their-plugins-must-not-do-anything-illegal-dishonest-or-morally-offensive) (Developers and their plugins must not do anything illegal, dishonest, or morally offensive.) has been amended to include the following new prohibition:
 -->
**2018年4月12日** より、[ガイドライン 9](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/#9-developers-and-their-plugins-must-not-do-anything-illegal-dishonest-or-morally-offensive) (開発者とそのプラグインは、違法なこと、不正なこと、道徳に反することをしてはならない) が改正され、新たに以下の禁止事項が盛り込まれました:

<!-- 
- implying that a plugin can create, provide, automate, or guarantee legal compliance
 -->
- プラグインが法令遵守を作成、提供、自動化、保証できると暗示すること

<!-- 
Some plugins offer to assist a site with being ‘compliant’ with laws like the ADA, GDPR, EU Cookie Law, VAT, HIPPA, PCI, and so on.
 -->
プラグインの中には、ADA (Americans with Disabilities of Act。障害を持つアメリカ人法)、GDPR (General Data Protection Regulation。EU 一般データ保護規則)、EU Cookie 法、VAT (Value Added Tax。付加価値税)、HIPAA (Health Insurance Portability and Accountability Act。医療保険の相互運用性と説明責任に関する法律)、PCI などの法律に「準拠」しているサイトを支援するものもあります。

<!-- 
No plugin can offer 100% legal compliance. They can (and do) assist sites with being more compliant. Still, at the end of the day, the responsibility remains with the site administrators to ensure their sites meet the qualifications for any compliance. Even services are not providing full compliance, just compliance when _their_ service is in use.
 -->
どのプラグインも100％の法令遵守を提供できません。プラグインは、サイトがよりコンプライアンスに適合するよう支援できます (そして実際にそうしています)。しかし、結局のところ、サイト管理者は、自分のサイトがどのようなコンプライアンスに対して適合しているかを確認する責任があります。サービスであっても、完全なコンプライアンスを提供しているわけではなく、_その_ サービスが利用されている場合のコンプライアンスにすぎません。

<!-- 
In order to make this more clear to site administrators, we recommend that plugins do **not** claim to be 100% compliant, and instead to explain that the plugin itself will assist in compliance. This has the added benefit of protecting developers in the case where compliance guidelines change and the plugin has not yet been updated.
 -->
サイト管理者にこのことをより明確に伝えるために、プラグインは100%準拠を主張 **しない** ことを推奨し、代わりにプラグイン自体が準拠を支援することを説明することを推奨します。これは、コンプライアンス・ガイドラインが変更され、プラグインがまだ更新されていない場合に、開発者を保護するという追加の利点があります。

<!-- 
## What do I need to do?
 -->
## どうすればいいの ?

<!-- 
tl;dr: Update your readme, documentation, assets (banners, screenshots, etc), and descriptions to clearly state that your plugin is meant to **assist** in compliance.
 -->
要約すると: Readme、ドキュメント、アセット (バナー、スクリーンショット等)、説明を更新し、あなたのプラグインがコンプライアンスを **支援** するものであることを明記しましょう。

<!-- 
For example, if your plugin says it “will make your website ADA compliant.” you should change that to “will help make your website more ADA compliant.” In addition, it would be wise to add in a note that “no plugin can provide 100% compliance” and then enumerate what yours does to get people closer. It’ll help your sales pitches too!
 -->
たとえば、プラグインに「あなたの web サイトを ADA に準拠させます。」と記述している場合、「あなたの web サイトをより ADA に準拠させる支援をします。」と変更してください。加えて、「100％のコンプライアンスを提供できるプラグインはありません」と注釈を加え、プラグインが何をするのかを列挙して、理解を深めてもらうことが賢明です。セールストークにも役立つでしょう !

<!-- 
## Do I need to change my plugin display name?
 -->
## プラグインの表示名を変更する必要がありますか ?

<!-- 
If your plugin name claims or implies compliance, yes.
 -->
プラグイン名がコンプライアンスを主張または暗示しているなら、イエスです。

<!-- 
For example, if your plugin display name is “100% EU Cookie Law Compliance” or “VAT-MOSS Compliance” then you should change the display name to “Improve EU Cookie Law Compliance” or “VAT-MOSS Compliance Assistant”
 -->
たとえば、プラグインの表示名が「100% EU Cookie 法準拠」または「VAT-MOSS 準拠」の場合、表示名を「EU Cookie 法準拠の改善」または「VAT-MOSS 準拠アシスタント」に変更する必要があります。

<!-- 
Keep in mind, a BETTER plugin name would be one that is unique to you. Remember, people can find “Foobar’s EU Cookie Law Tools” easier than “EU Cookie Law Tools” – they’ll remember your name easier.
 -->
覚えておいてほしいのは、「より良い」プラグイン名は、あなた固有の名前であるということです。人々は、「EU Cookie 法ツール」よりも「Foobar の EU Cookie 法ツール」が探し易いのです – あなたの名前を覚えてくれるでしょう。

<!-- 
## My plugin’s a service and is 100% compliant. Do I still need to do this?
 -->
## 私のプラグインはサービスであり、100％準拠しています。これでも変更する必要がありますか ?

<!-- 
Yes, but in a slightly different way.
 -->
イエスだけど、ちょっと違うやり方で。

<!-- 
A service assumes the responsibility for the compliance needed in those cases, and that’s what needs to be clear in the readme: it’s not the plugin code, it’s the service. We strongly recommend you link to your proof of compliance, and that is has a date on it.
 -->
サービスは、そのような場合に必要なコンプライアンスに対する責任を負うものであり、それは readme で明確にする必要があります: それはプラグインコードではなく、サービスです。私たちは、コンプライアンスを証明する書類にリンクすること、そしてその書類に日付が記載されていることを強く推奨します。

<!-- 
For example, instead of saying “Foobar Payment Plugin is PCI compliant.” you could say “The Foobar Payment Gateway Service handles PCI compliance, however this only pertains to purchases made using our gateway. Full details on our compliance can be found in our `[documentation](https://service-name.com/doc/)`.”
 -->
たとえば、「Foobar 支払いプラグインは PCI に準拠しています。」と言う代わりに「Foobar 支払ゲートウェイサービスは PCI に準拠していますが、これは私たちのゲートウェイを利用して行われた購入にのみ関係します。当社のコンプライアンスに関する完全な詳細は、当社の `[documentation](https://service-name.com/doc/)` に記載されています。」と言うこともできます。

<!-- 
## My plugin uses a 3rd party library that claims 100% compliance. Do I need to change that?
 -->
## 私のプラグインは、100％準拠を謳うサードパーティのライブラリを使用しています。変更する必要がありますか ?

<!-- 
Not unless you also claim it in your own readme/documentation. Though you should be a good human and warn them that what they’re doing isn’t really accurate.
 -->
あなた自身の readme やドキュメントで、それを主張しない限りは。しかし、あなたは善良な人間であるべきであり、彼らのしていることが実際には正確ではないことを警告すべきです。

<!-- 
## I only talk about 100% XHTML compliance. Do I have to change things?
 -->
## 私は100％ XHTML に準拠することしか話しません。変更する必要がありますか ?

<!-- 
Technically no, but … can you **really** promise 100% compliance forever and ever? Probably best to change that and just say “Updated for further XHTML compliance.” Check out how WordPress.org handles [Accessibility compliance](https://wordpress.org/about/accessibility/) for a good place to start.
 -->
技術的にはノーだが … **本当に** 100％のコンプライアンスを、未来永劫に約束できますか ? おそらく、それを変更して「さらなる XHTML 準拠の為に更新しました」と言うのがベストでしょう。手始めに WordPress.org の[アクセシビリティ・コンプライアンス](https://wordpress.org/about/accessibility/)の扱い方をチェックしてみてください。

<!-- 
## What happens if I don’t do this?
 -->
## これをしないと、どうなるんですか ?

<!-- 
If we find you’re making inaccurate claims, we will warn you. Then if it’s not fixed in a reasonable amount of time (60 days) your plugin may be closed. Worst than that, however, you open yourself up for legal disputes. This is not actually our responsibility to protect you from, however we feel that being good stewards of open source includes educating you as to these things. Essential, this is something that could seriously hurt you (or your company), and we’d rather that not happen.
 -->
あなたが不正確な主張をしていることが判明した場合、私たちはあなたに警告します。その後、妥当な期間 (60日) 内に修正されなければ、あなたのプラグインはクローズされるかもしれません。しかし、それよりも最悪なのは、法的な争いに巻き込まれる可能性があるということです。このようなことからあなたを守ることは、実は私たちの責任ではありませんが、オープンソースの良き世話人であるためには、こういったことについてあなた方を教育することも含まれると考えています。本質的に、これはあなた (またはあなたの会社) を深刻に傷つける可能性があることであり、私たちはそうならないことを望んでいます。

<!-- 
In addition, from this point forward, if your plugin is closed for other issues (guideline or security related), we will require you to update the readme before we will reopen the plugin.
 -->
加えて、この時点から、もしあなたのプラグインが他の課題 (ガイドラインやセキュリティ関連) によってクローズされた場合、プラグインを再開する前に readme を更新していただく必要があります。

<!-- 
## How do I report other plugins for this violation?
 -->
## この違反に関して、他のプラグインを報告するには ?

<!-- 
Same way you would anything. Email `plugins@wordpress.org` with a link to their plugin and an explanation as to why you feel they’re in violation. Keep in mind, closing a plugin is a last resort, so we may already be talking to them about it. Also remember pointing out other people making this mistake doesn’t give you a free pass. You have to fix your own stuff too.
 -->
何でも同じです。`plugins@wordpress.org` 宛てに、そのプラグインへのリンクと、なぜ違反していると感じるのかの説明を e メールで送ってください。プラグインをクローズするのは最終手段だということを覚えておいてください。ですから、私たちはすでに彼らにそのことを話しているかもしれません。また、他の人がこのような間違いを犯していることを指摘しても、あなたにフリーパスを与えるわけではないことも覚えておいてください。もちろん、自分のものは自分で修正しなければなりません。