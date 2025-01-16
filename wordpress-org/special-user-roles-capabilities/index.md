<!-- 
# Special User Roles and Capabilities
 -->
# 特別な権限グループと権限

<!-- 
Every person who pushes code for, or aids in support for, a plugin is required to have their **OWN** individual account. These accounts do not have to be personally identifying (that is, you can name them PluginNameSupport1 if you wanted), however all accounts must be used by a single human for your own protection.
 -->
プラグインのコードをプッシュする人、またはプラグインのサポートを支援する人は、**各自** 個別のアカウントを持つ必要があります。これらのアカウントは、個人を特定できるものである必要はありません (つまり、お望みであれば、PluginNameSupport1という名前にもできる) が、あなた自身を保護するために、すべてのアカウントはそれぞれ一人の人間によって使用されなければなりません。

<!-- 
There are four roles a user can have with regards to plugins. All can be managed from the **advanced view** section of a plugin page:
 -->
プラグインに関して、ユーザーが持てる4つの権限グループがあります。すべてプラグインページの **詳細表示** セクションから管理できます:

<!-- 
![Interface of the plugin page, the link ''Advanced View'' is highlighted.](https://i0.wp.com/developer.wordpress.org/files/2020/08/advanced-view.jpg?resize=300%2C260&ssl=1)
 -->
![「Advanced View」というリンクがハイライトされている、プラグインページのインターフェース](https://i0.wp.com/developer.wordpress.org/files/2020/08/advanced-view.jpg?resize=300%2C260&ssl=1)

<!-- 
There are fields to add Support Reps and Committers as needed.
 -->
必要に応じて、サポート担当やコミッターを追加する欄があります。

<!-- 
## Owner
 -->
## 所有者

<!-- 
A plugin owner is automatically set by the person who submits the plugin. On plugin approval, they are added as a Committer (see below) and flagged as the owner. Should this need to be changed, scroll down to the **Danger Zone** section and select the new owner from the dropdown:
 -->
プラグインの所有者は、プラグインを投稿した人が自動的に設定されます。プラグインが承認されると、コミッターとして追加され (下記参照)、所有者としてフラグが立てられます。これを変更する必要がある場合は、**Danger Zone** セクションまでスクロールダウンし、ドロップダウンから新しい所有者を選択してください:

<!-- 
![Transfer this plugin interface with a selector for the new owner and a "Please transfer -Plugin Name-" button](https://i0.wp.com/developer.wordpress.org/files/2020/08/can-transger.jpg?resize=1024%2C548&ssl=1)
 -->
![セレクタと「-プラグイン名-を譲渡します」ボタンインターフェースで、新しいオーナーにこのプラグインを譲渡する](https://i0.wp.com/developer.wordpress.org/files/2020/08/can-transger.jpg?resize=1024%2C548&ssl=1)

<!-- 
If there are no other users with commit access, you will need to grant them access before you can transfer the plugin. Remember, plugin owners should **always** have commit access to the plugins they own.
 -->
コミット権限を持つユーザーが他に居ない場合、プラグインを譲渡する前にそのユーザーに権限を与える必要があります。プラグインの所有者は、自分が所有するプラグインへのコミットアクセス権を **常に** 持つべきであることを覚えておいてください。

<!-- 
If you see this message, then you are not the current owner, and need to contact them to have ownership transferred:
 -->
このメッセージが表示された場合、あなたは現在の所有者ではないので、所有権を譲渡するために連絡する必要があります:

<!-- 
![Message: This plugin is currently owned by -user- the can choose to transfer ownership rights of the plugin to you](https://i0.wp.com/developer.wordpress.org/files/2020/08/Owner.jpg?resize=1024%2C249&ssl=1)
 -->
![メッセージ: このプラグインは現在のところ -user- によって所有されており、プラグインの所有権をあなたに譲渡できます](https://i0.wp.com/developer.wordpress.org/files/2020/08/Owner.jpg?resize=1024%2C249&ssl=1)

<!-- 
If the original owner is no longer available, you may contact the plugins team for assistance.
 -->
元の所有者がもはや見つからない場合は、プラグイン・チームに連絡して支援を求めることができます。

<!-- 
## Committer
 -->
## コミッター

<!-- 
Someone with commit access has the ability to push code via SVN and make official requests concerning a plugin to the Plugin Directory Team.
 -->
コミット権限を持っている人は、SVN 経由でコードをプッシュしたり、プラグイン・ディレクトリチームに対して、プラグインに関する公式な申請を提出したりできます。

<!-- 
Anyone with commit access has the right to request a plugin be closed, and has the ability to add and remove anyone from commit access. This is done from the **Advanced Page** on the sidebar:
 -->
コミットアクセス権を持つ人は誰でもプラグインのクローズを申請する権利があり、コミットアクセス権を持つ人を追加したり削除したりする権利があります。これはサイドバーの **詳細ページ** から行います:

<!-- 
![Interface to add a committer, an input with an "Add" button next to it](https://i0.wp.com/developer.wordpress.org/files/2021/02/Commit.jpg?resize=302%2C133&ssl=1)
 -->
![「Add」ボタン横の入力欄で、コミッターを追加するインターフェイス](https://i0.wp.com/developer.wordpress.org/files/2021/02/Commit.jpg?resize=302%2C133&ssl=1)

<!-- 
In the forums, these people are labeled as a “Plugin Author” and have the ability to mark posts regarding their plugin as resolved.
 -->
フォーラムでは、これらの人々は「Plugin Author」として表示され、自分のプラグインに関する投稿を解決済みとしてマークする権限を持っています。

<!-- 
Other than the “Plugin Author” label in the forum for replies to plugin support topics, having commit access is not outwardly displayed. In order to be listed in the plugin’s “Contributors & Developers” section, and to have the plugin included in a WordPress.org profile, the user must be listed as a contributor (see the subsequent section).
 -->
フォーラムでプラグインのサポートトピックに返信する際、「Plugin Author」ラベルが表示される以外、コミット権限を持っていることは表には表示されません。プラグインの「貢献者と開発者」セクションに表示され、WordPress.org のプロフィールにプラグインが表示されるようにするには、ユーザーはコントリビューターとしてリストされている必要があります (後続のセクションを参照)。

<!-- 
Adding and removing commit access can only be done by an existing committer.
 -->
コミットアクセス権の追加と削除は、既存のコミッターのみが実行できます。

<!-- 
## Support Rep
 -->
## サポート担当

<!-- 
A support rep has **no** extra ability to directly manage the plugin itself. They cannot request changes be made to a plugin’s status in the directory. However, they will be labeled in the forums as being official support and this can help people understand who is helping them.
 -->
サポート担当は、プラグイン自体を直接管理する特別な権限は **ありません**。彼らは、ディレクトリ内のプラグインのステータスの変更をリクエストできません。しかし、公式サポートであることがフォーラムで表示され、誰がサポートしているのかを理解する助けになります。

<!-- 
![Interface to add a support rep, an input with an "Add" button next to it](https://i0.wp.com/developer.wordpress.org/files/2021/02/Support.jpg?resize=317%2C140&ssl=1)
 -->
![「Add」ボタン横の入力欄で、サポート担当を追加するインターフェイス](https://i0.wp.com/developer.wordpress.org/files/2021/02/Support.jpg?resize=317%2C140&ssl=1)

<!-- 
In the forums, they are labeled as a “Plugin Support” and have the ability to mark posts regarding their plugin as resolved.
 -->
フォーラムでは、彼らは「Plugin Support」として表示され、自分のプラグインに関する投稿を解決済みとしてマークする権限を持っています。

<!-- 
They are displayed on the plugin page, and the plugin appears on their profile page as a Support Representative.
 -->
彼らはプラグインのページに表示され、プロフィールページでは、そのプラグインは、サポート担当として表示されます。

<!-- 
Adding and removing this status can only be done by an existing committer.
 -->
このステータスを追加したり削除したりできるのは、既存のコミッターだけです。

<!-- 
## Contributor
 -->
## 貢献者

<!-- 
A contributor has no extra ability to directly manage the plugin itself. They _cannot_ request changes be made to a plugin’s status in the directory.
 -->
貢献者は、プラグイン自体を直接管理する特別な権限を持ちません。彼らは、ディレクトリ内のプラグインのステータスに変更を加えるようリクエストすることは _できません_。

<!-- 
In the forums, they are labeled as a “Plugin Contributor” and have the ability to mark posts regarding their plugin as resolved.
 -->
フォーラムでは、彼らは「Plugin Contributor」として表示され、自分のプラグインに関する投稿を解決済みとしてマークする権限を持っています。

<!-- 
A contributor is publicly listed in the plugin’s “Contributors & Developers” section and the plugin is listed as one of the user’s plugins in their WordPress.org profile.
 -->
貢献者は、プラグインの「貢献者と開発者」セクションに公的にリストされ、また、WordPress.org のプロフィールでは、そのプラグインは、ユーザーのプラグインの一つとしてリストされます。

<!-- 
To be added as a contributor, a user must be listed within _Contributors_ in the plugin’s `readme.txt`.
 -->
貢献者として追加されるには、ユーザーがプラグインの `readme.txt` 内の _Contributors_ にリストされている必要があります。

<!-- 
While it is common to add people who helped with a plugin’s conceptualization or was an original contributor, you do not need to add anyone to your plugin with more access than you’re comfortable with.
 -->
プラグインのコンセプト作りを手伝った人や 当初の貢献者を追加するのはよくあることですが、あなたが納得できる以上のアクセス権を持つ人を、プラグインに追加する必要はありません。
