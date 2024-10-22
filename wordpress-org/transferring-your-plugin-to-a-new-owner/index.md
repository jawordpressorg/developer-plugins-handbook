<!-- 
# Transferring Your Plugin to a New Owner
 -->
# プラグインを新しいオーナーに譲渡する

<!-- 
While any plugin can have an unlimited number of committers and support reps, there is only one official owner of a plugin at any time. This is akin to how a post on WordPress can only have one official post author.
 -->
どんなプラグインでも、コミッターやサポート担当者の数は無制限ですが、プラグインの公式オーナーは常に一人です。これは、WordPress の投稿に公式の投稿者が一人しかいないのと同じようなものです。

<!-- 
## For Plugins With Under 10,000 Users
 -->
## ユーザー数1万人未満のプラグインの場合

<!-- 
If you’re transferring your plugin to a new owner, there are two steps that must take place.
 -->
プラグインを新しいオーナーに譲渡する場合、2つのステップを踏む必要があります。

<!-- 
First, add the new user as a **committer** to the plugin:
 -->
まず、新しいユーザーを **コミッター** としてプラグインに追加します:

<!-- 
- go to `https://wordpress.org/plugins/YOURPLUGIN/advanced` and add their username in as a committer
- update the `readme.txt` to add their userID as an author
 -->
- `https://wordpress.org/plugins/YOURPLUGIN/advanced` に移動し、その username をコミッターとして追加します
- `readme.txt` を更新し、彼らの userID を作者として追加します

<!-- 
Next, go to the Advanced tab and scroll down to the Danger Zone. There you will see a section for **Transfer Your Plugin**. Pick someone from the dropdown and click the button.
 -->
次に、Advanced タブに行き、Danger Zone までスクロールダウンします。そこに **Transfer Your Plugin** というセクションがあります。ドロップダウンから誰かを選び、ボタンをクリックしてください。

<!-- 
If there are no other committers, the plugin will not be available to be transferred, so you must do that first.
 -->
他のコミッターが居ない場合、プラグインは譲渡されないので、まずそれを行う必要があります。

<!-- 
![](https://i0.wp.com/developer.wordpress.org/files/2020/04/transfer.jpeg?resize=1024%2C558&ssl=1)
 -->
![](https://i0.wp.com/developer.wordpress.org/files/2020/04/transfer.jpeg?resize=1024%2C558&ssl=1)

<!-- 
## For Plugins with OVER 10,000 Users (or are beta/featured)
 -->
## 1万人以上のユーザーを持つプラグイン (またはベータ版 / 機能追加版) の場合

<!-- 
In order to prevent abuse, larger plugins and those officially recognized as featured/beta are restricted from these changes.
 -->
悪用を防止するため、大規模なプラグインや公式に機能追加版 / ベータ版と認められたプラグインは、これらの変更から制限されます。

<!-- 
To transfer a plugin in this case, you will need to email `plugins@wordpress.org` from the **CURRENT** owner’s email the following information:
 -->
この場合、プラグインを譲渡するには、**現在の** 所有者から `plugins@wordpress.org` に、以下の情報をメールする必要があります:

<!-- 
1. A _brief_ explanation of the reason for the transfer
2. The user ID of the new owner
3. If applicable, any changes to the status of being a featured/beta plugin
 -->
1. 譲渡の理由についての _簡単な_ 説明
2. 新しい所有者の userID
3. 該当する場合、機能追加版/ベータ版プラグインのステータスへの変更点

<!-- 
Most requests are processed without issue, however should a plugin be determined to be critical to the WordPress.org project, or should there be reason to believe the request was invalid (i.e. not sent from the current owner’s email, or an email address positively connected back to them), it may be denied or delayed.
 -->
ほとんどのリクエストは問題なく処理されますが、WordPress.org プロジェクトにとって重要なプラグインであると判断された場合、またはリクエストが無効であると考えられる理由がある場合 (例: 現在の所有者のメールアドレスから送信されていないか、または所有者に確実につながっているメールアドレスから送信されていない)、拒否または遅延されることがあります。