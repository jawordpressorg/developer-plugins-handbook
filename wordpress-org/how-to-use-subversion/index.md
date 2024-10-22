<!-- 
# Using Subversion
 -->
# Subversion の使用

<!-- 
SVN, or Subversion, is a version control system similar to Git. It can be used via command line, or one of numerous GUI applications, such as [Tortoise SVN](https://tortoisesvn.net/), [SmartSVN](https://www.smartsvn.com/), and more. If you're new to SVN, we recommend reviewing a [comparison of SVN clients](https://en.wikipedia.org/wiki/Comparison_of_Subversion_clients) before deciding which is best for you.
 -->
Subversion (SVN) は、Git に似たバージョン管理システムです。コマンドラインでも使えますし、[Tortoise SVN](https://tortoisesvn.net/)などの GUI アプリケーションでも使えます。SVN を初めて使う場合は、[SVN クライアントの比較](https://en.wikipedia.org/wiki/Comparison_of_Subversion_clients)を見てから、どれが最適かを決めることをおすすめします。

<!-- 
This document is _not_ a complete and robust explanation for using SVN, but more a quick primer to get started with plugins on WordPress.org. For more comprehensive documentation, see [The SVN Book](https://svnbook.red-bean.com/).
 -->
このドキュメントは、SVN を使用するための完全で堅牢な説明 _ではなく_、WordPress.org でプラグインを始めるための簡単な入門書です。より包括的なドキュメントは [The SVN Book](https://svnbook.red-bean.com/) を参照してください。

<!-- 
We'll describe here some of the basics about using SVN as it relates to WordPress.org hosting. The basic concepts of SVN, and nearly all code repository services, remain the same.
 -->
ここでは、WordPress.org ホスティングに関連する SVN の使用に関する基本的なことを説明します。SVN、そしてほとんどすべてのコードリポジトリ・サービスの基本的なコンセプトは変わりません。

<!-- 
For additional information, please see these documents:
 -->
追加情報については、以下のドキュメントをご覧ください:

<!-- 
- [How the readme.txt works](https://developer.wordpress.org/plugins/wordpress-org/how-your-readme-txt-works/).
- [How plugin assets (header images and icons) work](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/).
 -->
- [readme.txt の仕組み](https://developer.wordpress.org/plugins/wordpress-org/how-your-readme-txt-works/)
- [プラグイン・アセット (ヘッダー画像やアイコン) の仕組み](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/)

<!-- 
[warning]SVN and the Plugin Directory are a _release_ repository. Unlike Git, you shouldn't commit every small change, as doing so can degrade performance. Please only push **finished** changes to your SVN repository.[/warning]
 -->
[warning]SVN と プラグイン・ディレクトリは、_リリース_ リポジトリです。Git とは異なり、小さな変更をすべてコミットすべきではありません。SVN リポジトリには **完了した** 変更のみをプッシュしてください。[/warning]

<!-- 
## Overview
 -->
## 概要

<!-- 
All your files will be centrally stored in the **svn repository** on our servers. From that repository, anyone can **check out** a copy of your plugin files onto their local machine, but, as a plugin author, only you have the authority to **check in**. That means you can make changes to the files, add new files, and delete files on your local machine and upload those changes back to the central server. It's this process of checking in that updates both the files in the repository and also the information displayed in the WordPress.org Plugin Directory.
 -->
あなたのファイルはすべて、私たちのサーバー上の **svn リポジトリ** に一元的に格納されます。このリポジトリから、誰でもあなたのプラグインファイルのコピーをローカルマシンに **チェックアウト** できますが、プラグイン作者であるあなただけが **チェックイン** する権限を持っています。つまり、あなたはローカルマシンでファイルに変更を加えたり、新しいファイルを追加したり、ファイルを削除したりでき、それらの変更を中央サーバーにアップロードして書き戻すことができます。このチェックイン作業によって、リポジトリ内のファイルや WordPress.org のプラグイン・ディレクトリに表示される情報が更新されます。

<!-- 
Subversion keeps track of all these changes so that you can go back and look at old versions or **revisions** later if you ever need to. In addition to remembering each individual revision, you can tell subversion to **tag** certain revisions of the repository for easy reference. Tags are great for [labeling different releases of your plugin](https://developer.wordpress.org/plugins/wordpress-org/how-to-use-subversion/#tags) and are the only fully supported method of ensuring the correct versions are seen on WordPress.org and updated for users.
 -->
Subversion は、これらの変更点をすべて記録しているため、必要であれば後で古いバージョンや **リビジョン** に戻って見ることができます。個々のリビジョンを記憶するだけでなく、簡単に参照できるように、リポジトリの特定のリビジョンに **tag** を付けるよう、Subversion に指示できます。tag は、[プラグインの異なるリリースのラベル付け](https://developer.wordpress.org/plugins/wordpress-org/how-to-use-subversion/#tags)に最適で、WordPress.org で正しいバージョンが表示され、ユーザーのために更新されることを保証する、完全にサポートされた唯一の方法です。

<!-- 
## Your Account
 -->
## あなたのアカウント

<!-- 
Your account for SVN will be the same username (not the email) of the account you used when you submitted the plugin. This is the user ID you use for the WordPress forums as well.
 -->
SVN 用のアカウントは、プラグインを申請したときに使用したアカウントと同じユーザー名 (メールではありません) になります。これは WordPress のフォーラムでも使用するユーザー ID です。

<!-- 
Remember, _capitalization matters_ — if your username is JaneDoe, then you must use the capital J and D or else SVN will fail. You can see the specific capitalization of your name at [Your Profile](https://profiles.wordpress.org/me/profile/edit/group/1/).
 -->
_大文字と小文字が重要_ であることを忘れないでください。— あなたのユーザー名が JaneDoe なら、大文字の J と D を使わなければ SVN は失敗します。あなたの名前の大文字小文字は、[あなたのプロフィール](https://profiles.wordpress.org/me/profile/edit/group/1/)で確認できます。

<!-- 
If you need to reset your password, go to [login.wordpress.org](https://login.wordpress.org/lostpassword)
 -->
パスワードをリセットする必要がある場合は、[login.wordPress.org](https://login.wordpress.org/lostpassword) にアクセスしてください。

<!-- 
## SVN Folders
 -->
## SVN フォルダー

<!-- 
There are three directories created by default in all SVN repositories.
 -->
すべての SVN リポジトリには、デフォルトで3つのディレクトリが作成されます。

```
/assets/
/tags/
/trunk/
```

<!--
- Use `assets` for [screenshots, plugin headers, and plugin icons](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/).
- Development work belongs in `trunk`.
- Releases go in `tags`.
-->

- [スクリーンショット、プラグイン・ヘッダー、プラグイン・アイコン](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/)には `assets` を使ってください。
- 開発作業は、`trunk` に置きます。
- リリースは、`tags` に入れます。

<!--
_A `/branches/` directory that was used for divergent code is no longer created by default, as it was unused._
-->

`/branches/` ディレクトリは、使用されなかったため、デフォルトでは作成されなくなりました。_

<!-- 
### Trunk
 -->
### Trunk

<!-- 
[warning]Do not put your _main_ plugin file in a subfolder of trunk, like `/trunk/my-plugin/my-plugin.php` as that will break downloads. You may use subfolders for included files.[/warning]
 -->
[warning]ダウンロードができなくなるので、_メイン_ プラグインファイルは、`/trunk/my-plugin/my-plugin.php` のように、trunk のサブフォルダーに置かないでください。インクルードされたファイルにはサブフォルダーを使うことができます。[/warning]

<!-- 
The `/trunk` directory is where your plugin code should live. The trunk can be considered to be the latest and greatest code, however this is not necessarily the latest _stable_ code. Trunk is for the development version. Hopefully, the code in trunk should always be working code, but it may be buggy from time to time because it's not necessarily the "stable" version. For simple plugins, the trunk may be the only version of the code that exists, and that's fine as well.
 -->
`/trunk` ディレクトリは、あなたのプラグインコードを置くべき場所です。trunk は、最新かつ最高のコードと言えますが、必ずしも最新の _安定_ コードとは限りません。trunk は、開発版用のものです。できれば、trunk にあるコードは常に動作するコードであるべきですが、必ずしも「安定版」ではないので、時々バグがあるかもしれません。単純なプラグインの場合、trunk がそのコードの唯一のバージョンかもしれませんし、それはそれでかまいません。

<!-- 
Even if you do your development work elsewhere (like a git repository), we recommend you keep the trunk folder up to date with your code for easy SVN compares.
 -->
開発作業を別の場所 (Git リポジトリなど) で行っている場合でも、SVN と簡単に比較できるように、trunk フォルダーを常に最新のコードにしておくことをおすすめします。

<!-- 
### Tags
 -->
### Tags

<!-- 
The `/tags` directory is where you put versions of the plugin. You will use the same version numbers for the sub-directories here as you do for your plugin versioning. It is important that you always use tag folders and proper versioning to ensure your users get the correct code.
 -->
`/tags` ディレクトリは、プラグインのバージョンを置く場所です。ここのサブディレクトリには、プラグインのバージョン管理と同じバージョン番号を使用します。ユーザーに正しいコードを提供するために、tag フォルダーを使用し、適切なバージョン管理が重要です。

<!-- 
Version 1.0 of the plugin will be in `/tags/1.0`, version 1.1 would be in `/tags/1.1`, and so forth.
 -->
プラグインのバージョン1.0は `/tags/1.0` に、バージョン1.1は `/tags/1.1` に、といった具合です。

<!-- 
We **strongly** encourage the use of [semantic software versioning](https://semver.org/).
 -->
私たちは、[意味論的ソフトウェア・バージョニング](https://semver.org/)の使用を **強く** 推奨します。

<!-- 
### Assets
 -->
### Assets

<!-- 
[info]See also: [How Your Plugin Assets Work](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/)[/info]
 -->
[info]関連記事: [プラグイン・アセットの仕組み](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/)[/info]

<!-- 
Assets is where your screenshots, header images, and plugin icons reside. Some older plugins in the directory may have screenshot files in /trunk instead, however this is not recommended. All new plugins should put their screenshots in /assets. This keeps the filesizes of plugins small, as it is not necessary to send screenshots to WordPress installations along with the plugin itself.
 -->
Assets にはスクリーンショット、ヘッダー画像、プラグイン・アイコンがあります。古いプラグインでは、/trunk ディレクトリにスクリーンショットファイルを置くものもありますが、これは推奨されません。すべての新規プラグインは、/assets にスクリーンショットを置くべきです。プラグイン本体と一緒に WordPress インストールにスクリーンショットを送信する必要がないため、プラグインのファイルサイズを小さく保つことができます。

<!-- 
### Branches
 -->
### Branches

<!-- 
[alert]The `/branches/` directory is no longer created by default, as it was largely unused. This section can be considered deprecated and is available only for informational purposes.[/alert]
 -->
[alert]ほとんど使われていないので、`/branches/` ディレクトリは、デフォルトでは作成されなくなりました。このセクションは非推奨であり、情報提供のみを目的としています。[/alert]

<!-- 
The `/branches` directory is a place that you can use to store branches of the plugin. Perhaps versions that are in development, or test code, etc.
 -->
`/branches` ディレクトリは、プラグインのブランチを保存する場所です。おそらく開発中のバージョンやテストコードなどです。

<!-- 
The WordPress.org system **does not** use the branches directory for anything at all, it's considered to be strictly for developers to use as they need it. As it is no longer created by default, you can ignore it as you do not need it any longer.
 -->
WordPress.org のシステムでは、branches ディレクトリは **一切** 使用されません。branches ディレクトリは、開発者が必要に応じて使用するためのものです。デフォルトでは作成されなくなったので、もう必要ないので無視してかまいません。

<!-- 
## Best Practices
 -->
## ベスト・プラクティス

<!-- 
In order to make your code the most accessible for other developers, the following practices are considered to be optimum.
 -->
あなたのコードを他の開発者が最もアクセスしやすいものにするために、以下のプラクティスが最適と考えられます。

<!-- 
### Don't use SVN for development
 -->
### 開発には SVN を不使用

<!-- 
This is often confusing. Unlike GitHub, SVN is meant to be a _release_ system, not a development system. You don't need to commit and push every small change, and in fact doing so is detrimental to the system. Every time you push code to SVN, it rebuilds _all_ your zip files for all versions in SVN. This is why sometimes your plugin updates don't show for up to 6 hours. Instead, you should push one time, when you're ready to go.
 -->
これは、しばしば混乱を招きます。GitHub とは異なり、SVN は開発システムではなく _リリース_ システムです。小さな変更のたびにコミットしてプッシュする必要はありませんし、実際そうすることはシステムにとって有害です。SVN にコードをプッシュするたびに、SVN にあるすべてのバージョンの zip ファイルを _すべて_ リビルドします。プラグインのアップデートが最大6時間表示されないことがあるのはこのためです。その代わり、準備ができたら一回だけプッシュしてください。

<!-- 
### Use the trunk folder for code
 -->
### コード用に trunk フォルダーの使用

<!-- 
Many people use `trunk` as a placeholder. While it's possible to simply update the `readme.txt` file in trunk and put everything in tag folders, doing so makes it more difficult to compare any changes in your code. Instead, trunk should contain the latest version of your code, even if that version is a beta.
 -->
多くの人は `trunk` をプレースホルダとして使っています。trunk のファイル `readme.txt` を単純に更新して、すべてを tag フォルダーに入れることは可能ですが、そうすると、コードの変更点を比較するのが難しくなります。その代わりに、trunk にはあなたのコードの最新バージョンを、たとえそのバージョンがベータ版であっても、入れておくべきです。

<!-- 
### Always Tag Releases
 -->
### 常にタグ付きリリース

<!-- 
While it's possible to use trunk as a stable tag for plugins, this feature is not actually supported nor recommended. Instead, releases should be properly tagged and iterated. This will ensure full compatibility with any automatic updater, as well as allow for rollbacks should there be an issue with your code.
 -->
プラグインの安定タグとして trunk を使うことは可能ですが、この機能は実際にはサポートされていませんし、推奨もされていません。代わりに、リリースには適切なタグを付けて繰り返しリリースする必要があります。そうすることで、自動アップデータとの完全な互換性が保証され、あなたのコードに問題があった場合にロールバック可能になります。

<!-- 
### Create tags from trunk
 -->
### trunk から tag の作成

<!-- 
Instead of pushing your code directly to a tag folder, you should edit the code in trunk, complete with the stable version in the readme, and _then_ copy the code from trunk to the new tag.
 -->
コードを tag フォルダーに直接プッシュするのではなく、trunk でコードを編集し、readme に安定版と一緒に記載し、trunk から新規 tag にコードを _その後_ コピーしてください。

<!-- 
Not only will this make it easier see any changes, you will be making smaller commits as SVN will only update the changed code. This will save you time and reduce potential errors (such as updating to the wrong stable tag and pushing bad code to users).
 -->
こうすることで、変更を簡単に確認できるだけでなく、SVN は変更されたコードだけを更新するので、より小さなコミットを行うことになります。これは時間の節約になり、潜在的なエラー (間違った安定版タグに更新してしまい、悪いコードをユーザーにプッシュしてしまうなど) を減らすことができます。

<!-- 
Don't worry about the tag folder not existing for a short while. You can use `svn cp` to copy trunk to the tag and then push them up to SVN at the same time.
 -->
tag フォルダーがしばらく存在しなくても心配しないでください。`svn cp` を使って trunk を tag にコピーし、同時に SVN にプッシュできます。

<!-- 
If you are operating locally, then you can update trunk and create tags from it all in one go. Checkout the root of your repository, update the files in /trunk, then `svn copy /trunk /tags/1.2.3` (or whatever the version number is) and then commit the whole thing in one go. SVN is a system based on differences, and as long as you use svn to do the copy operation, then it preserves history and makes everything easy for others to follow along with.
 -->
ローカルで操作しているのであれば、trunk の更新と tag の作成を一度に行うことができます。リポジトリのルートをチェックアウトし、/trunk のファイルを更新し、`svn copy /trunk /tags/1.2.3` (バージョン番号は例) を実行し、一括でコミットします。SVN は差分にもとづくシステムであり、コピー操作に svn を使用する限り、履歴が保存され、他の人がフォローしやすくなります。

<!-- 
### Delete old versions
 -->
### 旧バージョンの削除

<!-- 
Since SVN is a release repository, many developers chose to remove older (non-supported) versions of their plugins. As of 2019, this no longer speeds up releases, as the build process only addresses tags with changed files.
 -->
SVN はリリース・リポジトリですので、多くの開発者は古い (サポートされていない) バージョンのプラグインを削除することを選択しました。2019年現在、ビルドプロセスは変更されたファイルを含む tag にのみ対処するため、これはもはやリリースのスピードアップにはなりません。

<!-- 
## Examples
 -->
## 例

<!-- 
### Starting a New Plugin
 -->
### 新規プラグインの開始

<!-- 
To start your plugin, you need to add the files you already have to your new SVN repository.
 -->
プラグインを開始するには、すでにあるファイルを新規の SVN リポジトリに追加する必要があります。

<!-- 
First create a local directory on your machine to house a copy of the SVN repository:
 -->
まず、あなたのマシン上に SVN リポジトリのコピーを置くローカルディレクトリを作成します:

```
mkdir my-local-dir
```

<!-- 
Next, check out the pre-built repository
 -->
次に、ビルド済みリポジトリをチェックアウトします。

```
svn co https://plugins.svn.wordpress.org/your-plugin-name my-local-dir
> A my-local-dir/trunk
> A my-local-dir/branches
> A my-local-dir/tags
> Checked out revision 11325.
```

<!-- 
In our example, subversion has added ("A" for "add") all of the directories from the central SVN repository to your local copy.
 -->
この例では、Subversion は中央の SVN リポジトリから、ローカルコピーにすべてのディレクトリを追加 (「A」は「add」) しています。

<!-- 
To add your code, navigate into the `my-local-dir` folder:
 -->
コードを追加するには、フォルダー `my-local-dir` に移動します:

```
cd my-local-dir
```

<!-- 
Now you can add your files to the `trunk/` directory of your local copy of the repository using copy/paste commands via command line, or dragging and dropping. Whatever you're comfortable with.
 -->
コマンドラインからコピー & ペーストコマンドを使うか、ドラッグ & ドロップで、リポジトリのローカルコピーの `trunk/` ディレクトリに、ファイルを追加できます。あなたがやりやすい方法でかまいません。

<!-- 
[warning]Do not put your _main_ plugin file in a subfolder of trunk, like `/trunk/my-plugin/my-plugin.php` as that will break downloads. You may use subfolders for included files.[/warning]
 -->
[warning]ダウンロードができなくなるので、_メイン_ プラグインファイルは、`/trunk/my-plugin/my-plugin.php` のように、trunk のサブフォルダーに置かないでください。インクルードされたファイルにはサブフォルダーを使うことができます。[/warning]

<!-- 
Once your files are in the trunk folder, you must let subversion know you want to add those new files back into the central repository.
 -->
いったんファイルが trunk フォルダーに入ったら、それらの新しいファイルを中央リポジトリに加え戻したいことを Subversion に知らせる必要があります。

```
cd my-local-dir
svn add trunk/*
> A trunk/my-plugin.php
> A trunk/readme.txt
```

<!-- 
After you add all your files, you'll check in the changes back to the central repository.
 -->
すべてのファイルを追加したら、中央リポジトリに変更をチェックインします。

```
svn ci -m 'Adding first version of my plugin'
> Adding trunk/my-plugin.php
> Adding trunk/readme.txt
> Transmitting file data .
> Committed revision 11326.
```

<!-- 
It's required to include a commit message for all checkins.
 -->
すべてのチェックインにコミットメッセージを含めることが義務付けられています。

<!-- 
If the commit fails because of ‘Access forbidden' and you **know** you have commit access, add your username and password to the check-in command.
 -->
「Access forbidden (アクセス禁止)」という理由でコミットが失敗し、あなたがコミットアクセス権を持っていることが **分かっている** 場合は、チェックインコマンドにユーザー名とパスワードを追加してください。

```
svn ci -m 'Adding first version of my plugin' --username your_username --password your_password
```

<!-- 
Remember your username is _case sensitive_.
 -->
ユーザー名は _大文字と小文字を区別する_ ということを忘れないでください。

<!-- 
### Editing Existing Files
 -->
### 既存ファイルの編集

<!-- 
Once your plugin is in the directory, you will likely need to edit the code at some point.
 -->
プラグインをディレクトリに入れたら、どこかの時点でコードを編集する必要があるでしょう。

<!-- 
First go into your your local copy of the repository and make sure it's up to date.
 -->
まず、リポジトリのローカルコピーに入り、最新の状態であることを確認してください。

```
cd my-local-dir/
svn up
> At revision 11326.
```

<!-- 
In the above example, we're all up to date. If there had been changes in the central repository, they would have been downloaded and merged into your local copy.
 -->
上記の例では、すべて最新の状態です。中央リポジトリに変更があった場合、それらはダウンロードされ、あなたのローカルコピーにマージされたでしょう。

<!-- 
Now you can edit the file that needs changing using whatever editor you prefer.
 -->
あとは好きなエディターを使って、変更が必要なファイルを編集すれば良いでしょう。

<!-- 
If you're not using an SVN GUI tool (like SubVersion or Coda) you can still check and see what's different between your local copy and the central repository after you make changes. First we check the status of the local copy:
 -->
SVN の GUI ツール (Subversion や Coda など) を使っていない場合でも、変更後にローカルコピーと中央リポジトリで何が違うかを確認できます。まずローカルコピーの状態を確認します:

```
svn stat
> M trunk/my-plugin.php
```

<!-- 
This tells us that our local `trunk/my-plugin.php` is different from the copy we downloaded from the central repository ("M" for "modified").
 -->
これは、ローカルの `trunk/my-plugin.php` が、中央リポジトリからダウンロードしたコピーとは異なる (「M」は「modified」) ことを示しています。

<!-- 
Let's see what exactly has changed in that file, so we can check it over and make sure things look right.
 -->
このファイルのどこが変わったのか見てみましょう。それをチェックして、きちんと表示されているか確認しましょう。

```
svn diff
> * What comes out is essentially the result of a
  * standard `diff -u` between your local copy and the
  * original copy you downloaded.
```

<!-- 
If it all looks good then it's time to check in those changes to the central repository.
 -->
すべて問題がなさそうなら、変更を中央リポジトリにチェックインするときです。

```
svn ci -m "fancy new feature: now you can foo *and* bar at the same time"
> Sending trunk/my-plugin.php
> Transmitting file data .
> Committed revision 11327.
```

<!-- 
And now you've successfully updated trunk.
 -->
これで trunk のアップデートは完了です。

<!-- 
### "Tagging" New Versions
 -->
### 新バージョンへの「タグ付け」

<!-- 
Each time you make a formal release of your plugin, you should tag a copy of that release's code. This lets your users easily grab the latest (or an older) version, it lets you keep track of changes more easily, and lets the WordPress.org Plugin Directory know what version of your plugin it should tell people to download.
 -->
プラグインを正式リリースする都度、そのリリースのコードのコピーに tag を付けるべきです。こうすることで、ユーザーは最新版 (または旧版) を簡単に入手でき、あなたは変更点をより簡単に追跡できます。また、WordPress.org プラグイン・ディレクトリは、どのバージョンのプラグインをダウンロードするように指示すべきかを知ることができます。

<!-- 
First copy your code to a subdirectory in the `tags/` directory. For the sake of the WordPress.org plugin browser, the new subdirectory should always look like a version number. `2.0.1.3` is good. `Cool hotness tag` is **bad**.
 -->
まず、コードを `tags/` ディレクトリのサブディレクトリにコピーします。WordPress.org のプラグイン・ブラウザのために、新しいサブディレクトリは常にバージョン番号のように見えるようにします。`2.0.1.3` が良いでしょう。`Cool hotness tag` は **bad** です。

<!-- 
We want to use `svn cp` instead of the regular `cp` in order to take advantage of SVN's features.
 -->
SVN の機能を利用するために、通常の `cp` の代わりに `svn cp` を使用したいと考えています。

```
svn cp trunk tags/2.0
> A tags/2.0
```

<!-- 
As always, check in the changes.
 -->
いつものように、変更点をチェックしましょう。

```
svn ci -m "tagging version 2.0"
> Adding tags/2.0
> Adding tags/2.0/my-plugin.php
> Adding tags/2.0/readme.txt
> Committed revision 11328.
```

<!-- 
When tagging a new version, **remember to update** the `Stable Tag` field in [`trunk/readme.txt`](https://wordpress.org/plugins/developers/#readme) to the new version.
 -->
新バージョンに tag を付けるときは、[`trunk/readme.txt`](https://wordpress.org/plugins/developers/#readme) の `Stable Tag` フィールドを新バージョンに **忘れずに更新** してください。

<!-- 
Congratulations! You've updated your code!
 -->
おめでとう ! あなたはコードを更新しました !

<!-- 
## Notes
 -->
## 備考

<!-- 
Don't put anything in SVN that you're not willing and prepared to have deployed to everyone who uses your plugin. This _includes_ vendor files, `.gitignore` and everything else.
 -->
あなたのプラグインを使うすべての人に配布する意思と準備がないものは SVN に置かないでください。これには、ベンダーファイルや `.gitignore` など、あらゆるものが _含まれます_。

<!-- 
You also should never upload zip files. Like most code repository systems, SVN expects you to upload individual files.
 -->
また、zip ファイルをアップロードしては、いけません。ほとんどのコードリポジトリ・システムがそうであるように、SVN は個々のファイルをアップロードすることを想定しています。

<!-- 
### See Also
 -->
### 関連記事

<!-- 
- [How the readme.txt works](https://developer.wordpress.org/plugins/wordpress-org/how-your-readme-txt-works/).
- [How plugin assets (header images and icons) work](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/).
- [The SVN Book](https://svnbook.red-bean.com/).
 -->
- [readme.txt の仕組み](https://developer.wordpress.org/plugins/wordpress-org/how-your-readme-txt-works/).
- [プラグイン・アセット (ヘッダー画像やアイコン) の仕組み](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/).
- [The SVN Book](https://svnbook.red-bean.com/).
