<!-- 
# Release Confirmation Emails
 -->
# リリース確認の e メール

<!-- 
In order to better protect plugins from inadvertent releases, we’ve added a new **opt-in** feature for plugins: Release Confirmation.
 -->
不用意なリリースからプラグインを守るため、プラグインに対して新しい **オプトイン** 機能を追加しました: リリース確認です。

<!-- 
When enabled on a plugin, to release a new version of a plugin you’ll need to tag a new release in SVN as normal, and then confirm on the [Release Management](https://wordpress.org/plugins/developers/releases/) dashboard.
 -->
プラグインで有効になっている場合、プラグインの新しいバージョンをリリースするには、通常通り SVN で新しいリリースにタグを付け、[リリース管理](https://wordpress.org/plugins/developers/releases/)ダッシュボードで確認する必要があります。

<!-- 
Access to the Release Management dashboard is limited to plugin committers, and all actions require confirmation via a tokenised link which is emailed to you as needed.
 -->
リリース管理ダッシュボードへのアクセスはプラグインのコミッターに限定されており、すべてのアクションにはトークン化されたリンク経由での確認が必要です。

<!-- 
When WordPress.org detects a new version has been tagged in SVN, all committers are automatically sent an email notifying them that a new release is pending, who made it, and a link to the dashboard to confirm the release.
Plugin committers will also see a banner on the top of your WordPress.org plugins page directing you to the Release Management dashboard.
 -->
WordPress.org が、新しいバージョンが SVN にタグ付けされたことを検知すると、すべてのコミッターに対して、新しいリリースが保留中であることと、誰がリリースしたのか、リリースを確認するためのダッシュボードへのリンクを記載した、通知メールが自動的に送信されます。プラグインコミッターには、WordPress.org のプラグインページの上部にリリース管理ダッシュボードへのバナーも表示されます。

<!-- 
Once confirmed, the release will proceed as usual and should update within a few minutes.
 -->
リリースが確認されれば、通常通り作業が進められ、数分以内に更新されることでしょう。

<!-- 
## Requirements
 -->
## 必要条件

<!-- 
-   Plugins are required to use tags for new versions, you cannot release your plugin from trunk.
-   You must still update the `Stable Tag:` header in your trunk/readme.txt file.
-   Once released, alterations cannot be made to the tagged version. This includes changing the readme (for tested up to).
-   Committers must be able to receive emails directly, and not have it go to a shared inbox or support ticket system.
 -->
-   プラグインは、新しいバージョン用のタグを使用する必要があり、trunk からプラグインをリリースできません。
-   それでも、trunk/readme.txt 内の `Stable Tag:` ヘッダーを更新する必要があります。
-   いったんリリースされると、タグ付けされたバージョンに変更を加えることはできません。これには readme の変更も (テスト済みまで) 含まれます。
-   コミッターは、共有の受信箱やサポートチケットシステムにメールを送らず、直接メールを受け取れるようにしてください。

<!-- 
## Requiring double approval
 -->
## 二重承認の必要性

<!-- 
Release Confirmations are opt-in, but only requires a singular committer to confirm the release.
If a group would like to require multiple committers to approve a release, please contact the Plugins team with your request.
 -->
リリース確認はオプトインですが、リリースの確認は一人のコミッターにのみ要求されます。複数のコミッターにリリースを承認してもらいたい場合は、リクエストをプラグインチームまでご連絡ください。