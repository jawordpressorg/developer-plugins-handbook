<!-- 
# Plugin Developer FAQ
 -->
# プラグイン開発者 FAQ

<!-- 
There are lot of ins and outs to hosting WordPress plugins. Please take a minute to see if your question is answered here before reaching out for assistance.
 -->
WordPress プラグインのホスティングには、多くの心得があります。お問い合わせの前に、あなたの質問がここで解決されるかどうか、少し時間を取って見てください。

<!-- 
## The Plugin Review Team
 -->
## プラグイン・レビューチーム

<!-- 
### How do I contact the Plugin Review team?
 -->
### プラグイン・レビューチームへの連絡方法は ?

<!-- 
You can contact us by email at `plugins@wordpress.org` – we reply to all emails within 7 business days.
 -->
お問い合わせは `plugins@wordpress.org` 宛ての E メールにて承っています。7営業日以内に返信します。

<!-- 
### Does the review team work for Automattic?
 -->
### レビューチームは、Automattic のために働いているのですか ?

<!-- 
No. The review team is made up of 100% volunteers. Some are compensated by their full-time employers, but no one is hired by WordPress.org, Automattic, or WordPress.com
 -->
いいえ。レビューチームは、100%ボランティアで構成されています。フルタイムの雇用主から報酬を得ている人もいますが、WordPress.org、Automattic、WordPress.com に雇われている人はいません。

<!-- 
### Can I join the team?
 -->
### チームに参加できますか ?

<!-- 
Please take a look at [this handbook page](https://make.wordpress.org/plugins/handbook/apply/).
 -->
[このハンドブックのページ](https://make.wordpress.org/plugins/handbook/apply/)をご覧ください。

<!-- 
## Submissions and Reviews
 -->
## Submissions and Reviews

<!-- 
### Where do I submit my plugin?
 -->
### Where do I submit my plugin?

<!-- 
Go to the [Add](https://wordpress.org/plugins/developers/add/) page and upload your zip. Your file should be under **10 MegaBytes** and be a complete plugin. We do not accept placeholders or plugins that aren't ready to be used.
 -->
Go to the [Add](https://wordpress.org/plugins/developers/add/) page and upload your zip. Your file should be under **10 MegaBytes** and be a complete plugin. We do not accept placeholders or plugins that aren't ready to be used.

<!-- 
### What if my plugin is over 10 MegaBytes?
 -->
### What if my plugin is over 10 MegaBytes?

<!-- 
Double check that you aren't including unused files (like test folders, documentation, and full node/vendor folders). The majority of plugins who face this issue have included all sorts of development content that has no place in the final code.
 -->
Double check that you aren't including unused files (like test folders, documentation, and full node/vendor folders). The majority of plugins who face this issue have included all sorts of development content that has no place in the final code.

<!-- 
### What happens after submission?
 -->
### What happens after submission?

<!-- 
You will get an automated email telling you about the submission immediately. At that point, someone will manually download and review your code. If we find no issues with the security, documentation, or presentation, your plugin will be approved. If we determine there are issues, you will receive a second email with details explaining what needs to be fixed.
 -->
You will get an automated email telling you about the submission immediately. At that point, someone will manually download and review your code. If we find no issues with the security, documentation, or presentation, your plugin will be approved. If we determine there are issues, you will receive a second email with details explaining what needs to be fixed.

<!-- 
### What will my plugin permalink (slug) be?
 -->
### What will my plugin permalink (slug) be?

<!-- 
When you submit a plugin, you get an automated email telling you what the slug will be. This is populated based on the value of Plugin Name in your main plugin file (the one with the plugin headers). If you set yours as `Plugin Name: Boaty McBoatface` then your URL will be `wordpress.org/plugins/boaty-mcboatface` and your slug will be `boaty-mcboatface` for example. If there is an existing plugin with your name, then you'll get a warning on submission.
 -->
When you submit a plugin, you get an automated email telling you what the slug will be. This is populated based on the value of Plugin Name in your main plugin file (the one with the plugin headers). If you set yours as `Plugin Name: Boaty McBoatface` then your URL will be `wordpress.org/plugins/boaty-mcboatface` and your slug will be `boaty-mcboatface` for example. If there is an existing plugin with your name, then you'll get a warning on submission.

<!-- 
This is _also_ the folder name (in SVN and installed on WordPress) for your plugin and your text-domain, so pay attention carefully.
 -->
This is _also_ the folder name (in SVN and installed on WordPress) for your plugin and your text-domain, so pay attention carefully.

<!-- 
Once your plugin is approved, this name **cannot** be renamed. Please chose wisely.
 -->
Once your plugin is approved, this name **cannot** be renamed. Please chose wisely.

<!-- 
### Why did I get a different slug than I was told?
 -->
### Why did I get a different slug than I was told?

<!-- 
If we have to change your permalink (slug) we will always email you to explain why. In general, we change your permalink when you have obvious typos or mistakes (_foundre_ instead of _founder_, for example) or if there are conflicts with existing trademarks or other plugins. Please make sure you read your review email carefully, as we do explain why we have do to things.
 -->
If we have to change your permalink (slug) we will always email you to explain why. In general, we change your permalink when you have obvious typos or mistakes (_foundre_ instead of _founder_, for example) or if there are conflicts with existing trademarks or other plugins. Please make sure you read your review email carefully, as we do explain why we have do to things.

<!-- 
### Why is my submission failing saying my plugin name already exists?
 -->
### Why is my submission failing saying my plugin name already exists?

<!-- 
There are two reasons this happens:
 -->
There are two reasons this happens:

<!-- 
1. You're trying to use a plugin with a permalink that already exists on WordPress.org.
2. You're trying to use a plugin with a permalink that exists **outside** WordPress.org and has a significant user base.
 -->
1. You're trying to use a plugin with a permalink that already exists on WordPress.org.
2. You're trying to use a plugin with a permalink that exists **outside** WordPress.org and has a significant user base.

<!-- 
The first one is obvious. You can't have two plugins with the same permalink so you need to pick a new one.
 -->
The first one is obvious. You can't have two plugins with the same permalink so you need to pick a new one.

<!-- 
The second one is confusing because it's telling you that somewhere, not on WordPress.org, that permalink is in use. It's important to understand that the way the plugin update API works is that it compares the plugin folder name (i.e. the permalink) to every plugin it has hosted on WordPress.org. If there's a match, then it checks for updates and users are prompted to upgrade.
 -->
The second one is confusing because it's telling you that somewhere, not on WordPress.org, that permalink is in use. It's important to understand that the way the plugin update API works is that it compares the plugin folder name (i.e. the permalink) to every plugin it has hosted on WordPress.org. If there's a match, then it checks for updates and users are prompted to upgrade.

<!-- 
When that happens, users of the 'original' plugin (the one we don't host) would upgrade to the one from WordPress.org and, if that isn't what you actually wanted to do, you could break their sites.
 -->
When that happens, users of the 'original' plugin (the one we don't host) would upgrade to the one from WordPress.org and, if that isn't what you actually wanted to do, you could break their sites.

<!-- 
Sometimes this situation develops when a company or person releases their plugin privately (via Github for example) and decides they want to re-release it on WordPress.org. In those cases, we recommend you email us and we'll walk you through how to get past the error.
 -->
Sometimes this situation develops when a company or person releases their plugin privately (via Github for example) and decides they want to re-release it on WordPress.org. In those cases, we recommend you email us and we'll walk you through how to get past the error.

<!-- 
### Why am I getting an error that says I cannot begin my plugin name with a term?
 -->
### Why am I getting an error that says I cannot begin my plugin name with a term?

<!-- 
That error is to inform you that you may not begin your Display Name with someone else's trademarked term. This is to protect you and the directory from legal issues regarding trademark abuse. To correct the issue, you must change the Display Name in your plugin's readme and main PHP files.
 -->
That error is to inform you that you may not begin your Display Name with someone else's trademarked term. This is to protect you and the directory from legal issues regarding trademark abuse. To correct the issue, you must change the Display Name in your plugin's readme and main PHP files.

<!-- 
Please do not try to 'work around' this by cleverly renaming your plugin (WuuCommerce for example). All that does is make us worry you're not going to be able to follow guidelines in the future.
 -->
Please do not try to 'work around' this by cleverly renaming your plugin (WuuCommerce for example). All that does is make us worry you're not going to be able to follow guidelines in the future.

<!-- 
### Why am I getting an error that says I cannot use a term entirely in my plugin name?
 -->
### Why am I getting an error that says I cannot use a term entirely in my plugin name?

<!-- 
Some trademark owners have requested we no longer permit the use of specific terms in plugin names entirely. If you see this error, then you must remove the term from your plugin name.
 -->
Some trademark owners have requested we no longer permit the use of specific terms in plugin names entirely. If you see this error, then you must remove the term from your plugin name.

<!-- 
> To proceed with this submission you must remove "_TERM_" from the Plugin Name: line in both your main plugin file and readme entirely.
 -->
> To proceed with this submission you must remove "_TERM_" from the Plugin Name: line in both your main plugin file and readme entirely.

<!-- 
If you attempt to get around this by changing your term from 'Facerange' to 'Face-Range', we will pend your submission and reiterate that you cannot use the term. Please don't try to be sneaky or clever to get past this restriction.
 -->
If you attempt to get around this by changing your term from 'Facerange' to 'Face-Range', we will pend your submission and reiterate that you cannot use the term. Please don't try to be sneaky or clever to get past this restriction.

<!-- 
### How do I submit an official plugin?
 -->
### How do I submit an official plugin?

<!-- 
Log in as the official company user account and submit with that account _only_.
 -->
Log in as the official company user account and submit with that account _only_.

<!-- 
We cannot accept plugins submitted by individual developer accounts, unless they're clearly company ones as well. For example, submitting your official Facerange plugin with a user that has a gmail address is likely to be flagged for trademark infringement.
 -->
We cannot accept plugins submitted by individual developer accounts, unless they're clearly company ones as well. For example, submitting your official Facerange plugin with a user that has a gmail address is likely to be flagged for trademark infringement.

<!-- 
What if I submitted the plugin with the wrong user ID?
 -->
What if I submitted the plugin with the wrong user ID?

<!-- 
Just reply to the email right away and let us know. We can transfer ownership for you. If you forget to do this, you can fix it yourself by [adding the correct account as a committer](https://developer.wordpress.org/plugins/wordpress-org/plugin-developer-faq/#how-do-i-give-someone-else-access-to-my-plugin) and then having that account remove your own.
 -->
Just reply to the email right away and let us know. We can transfer ownership for you. If you forget to do this, you can fix it yourself by [adding the correct account as a committer](https://developer.wordpress.org/plugins/wordpress-org/plugin-developer-faq/#how-do-i-give-someone-else-access-to-my-plugin) and then having that account remove your own.

<!-- 
**DO NOT** resubmit your plugin. Just tell us right away and we'll fix it.
 -->
**DO NOT** resubmit your plugin. Just tell us right away and we'll fix it.

<!-- 
### How long does it take to get a plugin approved?
 -->
### How long does it take to get a plugin approved?

<!-- 
There's no official average, as no two plugins are the same. If your plugin is small and all the code is correct, it should be approved within **fourteen** days of _initial review_.
 -->
There's no official average, as no two plugins are the same. If your plugin is small and all the code is correct, it should be approved within **fourteen** days of _initial review_.

<!-- 
If your plugin has any code issues, it will take as long as it takes for you to correct the issues. Either way, you _will_ get an email from `plugins@wordpress.org` with the status, so please add that to your email whitelist and patiently wait for our response.
 -->
If your plugin has any code issues, it will take as long as it takes for you to correct the issues. Either way, you _will_ get an email from `plugins@wordpress.org` with the status, so please add that to your email whitelist and patiently wait for our response.

<!-- 
### I sent in the fixes but no one replied. How long should I wait?
 -->
### I sent in the fixes but no one replied. How long should I wait?

<!-- 
We aim to reply to all reviews within seven (7) business days. If it's been less than that, it just means we've been really busy. If it's been two days, like over a weekend or a holiday, then you should not **reasonably** expect a reply.
 -->
We aim to reply to all reviews within seven (7) business days. If it's been less than that, it just means we've been really busy. If it's been two days, like over a weekend or a holiday, then you should not **reasonably** expect a reply.

<!-- 
Remember the review team is made up of 100% volunteers, all of whom have full time day jobs, and other volunteer duties. We do reply promptly, but we also have lives outside of WordPress.
 -->
Remember the review team is made up of 100% volunteers, all of whom have full time day jobs, and other volunteer duties. We do reply promptly, but we also have lives outside of WordPress.

<!-- 
### If my plugin has a problem, how long do I have to fix it?
 -->
### If my plugin has a problem, how long do I have to fix it?

<!-- 
There's no timeline and as long as we know you're working on it and we feel you're making progress, we'll leave the review open. Your plugin will be rejected after 3 months, but the review will remain open.
 -->
There's no timeline and as long as we know you're working on it and we feel you're making progress, we'll leave the review open. Your plugin will be rejected after 3 months, but the review will remain open.

<!-- 
### Why was my plugin rejected after three months?
 -->
### Why was my plugin rejected after three months?

<!-- 
If your plugin review is not complete after three (3) months, we will reject your submission in order to keep the queue maintainable. At any point in time, we have 700 people mid-review, and we figure that 3 months is a pretty reasonable time frame.
 -->
If your plugin review is not complete after three (3) months, we will reject your submission in order to keep the queue maintainable. At any point in time, we have 700 people mid-review, and we figure that 3 months is a pretty reasonable time frame.

<!-- 
### I finally fixed my plugin. Should I resubmit?
 -->
### I finally fixed my plugin. Should I resubmit?

<!-- 
No. Reply to the email. Even if it's been 18 months. The longest time to date has been 3 years. We don't mind if it takes a while.
 -->
No. Reply to the email. Even if it's been 18 months. The longest time to date has been 3 years. We don't mind if it takes a while.

<!-- 
### How many plugins can I submit for review at a time?
 -->
### How many plugins can I submit for review at a time?

<!-- 
Just one.
 -->
Just one.

<!-- 
### Why can't I submit more than one plugin at a time?
 -->
### Why can't I submit more than one plugin at a time?

<!-- 
Allowing people to have multiple submissions at once was proven to be detrimental to the review process. Errors were regularly found in all the plugins, resulting in the same emails being sent multiple times. In addition, people often got confused as to which review they were working on, muddying the waters about what needed to be solved. By changing this to one-at-a-time, confusion in those matters dropped significantly.
 -->
Allowing people to have multiple submissions at once was proven to be detrimental to the review process. Errors were regularly found in all the plugins, resulting in the same emails being sent multiple times. In addition, people often got confused as to which review they were working on, muddying the waters about what needed to be solved. By changing this to one-at-a-time, confusion in those matters dropped significantly.

<!-- 
In addition, many new users don't know how to use SVN, and wound up submitting multiple plugins and never using any. That can be a drain on our resources, so we do limit people.
 -->
In addition, many new users don't know how to use SVN, and wound up submitting multiple plugins and never using any. That can be a drain on our resources, so we do limit people.

<!-- 
Since all plugins get an initial review within two weeks, this should not be a hardship.
 -->
Since all plugins get an initial review within two weeks, this should not be a hardship.

<!-- 
### Can I submit multiple plugins with multiple accounts?
 -->
### Can I submit multiple plugins with multiple accounts?

<!-- 
No. And if you do so, we will suspend all your secondary accounts. Don't try to get around the one-at-a-time rule please.
 -->
No. And if you do so, we will suspend all your secondary accounts. Don't try to get around the one-at-a-time rule please.

<!-- 
### I need my plugin approved by a specific date, what should I do?
 -->
### I need my plugin approved by a specific date, what should I do?

<!-- 
Submit it as early as possible. Unless the plugin is meant to address a security or legal issue, we don't permit queue jumping. If it _is_ related to one of those, please email `plugins@wordpress.org` and explain the situation.
 -->
Submit it as early as possible. Unless the plugin is meant to address a security or legal issue, we don't permit queue jumping. If it _is_ related to one of those, please email `plugins@wordpress.org` and explain the situation.

<!-- 
### Are there specific things that I should avoid doing?
 -->
### Are there specific things that I should avoid doing?

<!-- 
We look for some pretty obvious things, all of which are listed [in our guidelines](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/). Most can be summed up as "Don't be a spammer," but to touch on the ones people do the most:
 -->
We look for some pretty obvious things, all of which are listed [in our guidelines](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/). Most can be summed up as "Don't be a spammer," but to touch on the ones people do the most:

<!-- 
- Not including a `readme.txt` file when acting as a service.
- Not testing the plugin with `WP_DEBUG`.
- Including custom versions of packaged JavaScript libraries.
- Calling external files unnecessarily.
- "Powered By" links.
- Phoning home.
 -->
- Not including a `readme.txt` file when acting as a service.
- Not testing the plugin with `WP_DEBUG`.
- Including custom versions of packaged JavaScript libraries.
- Calling external files unnecessarily.
- "Powered By" links.
- Phoning home.

<!-- 
Again, this is a brief overview. Please read the guidelines, as the full list is quite detailed.
 -->
Again, this is a brief overview. Please read the guidelines, as the full list is quite detailed.

<!-- 
### Are there plugins you don't accept?
 -->
### Are there plugins you don't accept?

<!-- 
We don't accept plugins that do 'nothing,' are illegal, or encourage bad behavior. This includes black hat SEO spamming, content spinners, hate-plugins, and so on.
 -->
We don't accept plugins that do 'nothing,' are illegal, or encourage bad behavior. This includes black hat SEO spamming, content spinners, hate-plugins, and so on.

<!-- 
Similarly we do not accept framework plugins or library plugins. If your plugin has to require other plugins or themes to edit themselves in order to use your plugin, it's a library. If your plugin is a template from which more code can be built by customizing the files directly, it's a framework or boilerplate. Frameworks and libraries should be packaged with each plugin (hopefully in a way that doesn't conflict with other plugins using the framework or libraries). At least until core supports plugin dependencies.
 -->
Similarly we do not accept framework plugins or library plugins. If your plugin has to require other plugins or themes to edit themselves in order to use your plugin, it's a library. If your plugin is a template from which more code can be built by customizing the files directly, it's a framework or boilerplate. Frameworks and libraries should be packaged with each plugin (hopefully in a way that doesn't conflict with other plugins using the framework or libraries). At least until core supports plugin dependencies.

<!-- 
We also don't accept 100% copies of other people's work or plugins that duplicate functionality found in WordPress Core. Basically, your plugin should do something new, or in a new way, or solve a specific issue.
 -->
We also don't accept 100% copies of other people's work or plugins that duplicate functionality found in WordPress Core. Basically, your plugin should do something new, or in a new way, or solve a specific issue.

<!-- 
### I want to redo, upgrade, or rebrand my existing plugin. I just submit again, right?
 -->
### I want to redo, upgrade, or rebrand my existing plugin. I just submit again, right?

<!-- 
No, you should rewrite and upgrade the existing plugin. Make it a major version release. We can't rename plugins or transfer users, so a new one wouldn't carry over any existing users, reviews, support topics, ratings, downloads, favorites, etc. Basically you'd leave _all_ your current users out in the cold, and that's mean.
 -->
No, you should rewrite and upgrade the existing plugin. Make it a major version release. We can't rename plugins or transfer users, so a new one wouldn't carry over any existing users, reviews, support topics, ratings, downloads, favorites, etc. Basically you'd leave _all_ your current users out in the cold, and that's mean.

<!-- 
### I made a mistake with my submission. How can I fix it?
 -->
### I made a mistake with my submission. How can I fix it?

<!-- 
Every submission gets an automated reply with directions. Reply to that or email `plugins@wordpress.org` and explain the situation.
 -->
Every submission gets an automated reply with directions. Reply to that or email `plugins@wordpress.org` and explain the situation.

<!-- 
We can correct plugin slugs before approval, so we are often able to fix that for you. If not, we'll let you know what to do. We try to catch typos in names before we approve anything, but we make mistakes too.
 -->
We can correct plugin slugs before approval, so we are often able to fix that for you. If not, we'll let you know what to do. We try to catch typos in names before we approve anything, but we make mistakes too.

<!-- 
### Are there things I can't do in a plugin name?
 -->
### Are there things I can't do in a plugin name?

<!-- 
We have the following restrictions:
 -->
We have the following restrictions:

<!-- 
*   Plugins may not use vulgarities in the name or slug
*   Plugins may not use 'WordPress' or 'Plugin' in their slugs except under extreme situations
*   Plugins may not use version numbers in plugin slugs
*   Due to system limitations, only English letters and Arabic numbers are permitted in the slug
*   Plugins may not **start** with a trademarked term or name of a specific project/library/tool _unless_ submitted by an official representative
 -->
*   Plugins may not use vulgarities in the name or slug
*   Plugins may not use 'WordPress' or 'Plugin' in their slugs except under extreme situations
*   Plugins may not use version numbers in plugin slugs
*   Due to system limitations, only English letters and Arabic numbers are permitted in the slug
*   Plugins may not **start** with a trademarked term or name of a specific project/library/tool _unless_ submitted by an official representative

<!-- 
We encourage everyone to be creative and come up with unique slugs. We automatically correct any plugin that has an unacceptable slug. If there's a question as to the best choice, we will contact you to be sure.
 -->
We encourage everyone to be creative and come up with unique slugs. We automatically correct any plugin that has an unacceptable slug. If there's a question as to the best choice, we will contact you to be sure.

<!-- 
## Using The SVN Repository
 -->
## SVN リポジトリの使用

<!-- 
### Where do I put my files?
 -->
### 自分のファイルは、どこに置けばいいの ?

<!-- 
Put your code files directly in the `trunk/` directory of your repository. Whenever you release a new version, [tag that release](https://developer.wordpress.org/plugins/wordpress-org/how-to-use-subversion/#tags) by copying the current trunk revision to a new subdirectory of the `tags/` directory.
 -->
コードファイルをリポジトリの `trunk/` ディレクトリに直接置いてください。新しいバージョンをリリースするたびに、現在のトランク・リビジョンを `tags/` ディレクトリの新しいサブディレクトリにコピーして、[そのリリースにタグを付けます](https://developer.wordpress.org/plugins/wordpress-org/how-to-use-subversion/#tags)。

<!-- 
Make sure you update [`trunk/readme.txt`](https://wordpress.org/plugins/developers/#readme) to reflect the **new** stable tag.
 -->
[`trunk/readme.txt`](https://wordpress.org/plugins/developers/#readme) を更新して、**新しい** 安定版タグを反映させてください。

<!-- 
Images for the readme (such as [screenshots, plugin headers, and plugin icons](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/)), belong in the `assets/` directory (which you may need to create) in the root of your SVN checkout. This will be on the same level as `tags/` and `trunk/`, for example.
 -->
readme 用の画像 ( [スクリーンショット、プラグイン・ヘッダー、プラグイン・アイコン](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/) など) は、SVN チェックアウトの root にある `assets/` ディレクトリ (作成する必要があるかもしれません) に置きます。これは、たとえば、`tags/` や `trunk/` と同じ階層になります。

<!-- 
### Can I put my files in a subdirectory of `trunk`?
 -->
### `trunk` のサブディレクトリに、自分のファイルを置いてもいいの ?

<!-- 
No. Doing that will cause the zip generator to break.
 -->
いいえ。そんなことをすると、ZIP ジェネレータが壊れてしまいます。

<!-- 
If you have complicated plugin with lots of files, you can of course organize them into subdirectories, but the [readme.txt file](https://wordpress.org/plugins/developers/#readme) and the root plugin file should go straight into `trunk/`.
 -->
ファイルがたくさんある複雑なプラグインの場合は、もちろんサブディレクトリに編成できますが、ファイル [readme.txt](https://wordpress.org/plugins/developers/#readme) と root プラグイン・ファイルは、そのまま `trunk/` に入れてください。

<!-- 
### How should I name my tags (a.k.a. releases)?
 -->
### タグ (いわゆる、リリース) には、どのような名前をつければいいの ?

<!-- 
Your Subversion tags should look like version numbers. Specifically, they should only contain **numbers and periods**. `2.8.4` is a good lookin' tag, `my neato releaso` is a bad lookin' tag. We recommend you use [Semantic Versioning](https://semver.org/) to keep track of releases, but we do not enforce this.
 -->
Subversion のタグは、バージョン番号のように見えるべきです。具体的には、**数字とピリオド** だけを含むべきです。`2.8.4` は良いタグで、`my neato releaso` は悪いタグです。[セマンティック・バージョニング](https://semver.org/)を使ってリリース管理することを推奨しますが、強制はしません。

<!-- 
Note that we're talking about _Subversion_ tags here, not `readme.txt` search type tags.
 -->
ここで話しているのは _Subversion_ タグについてであって、`readme.txt` 検索タイプのタグについてではないことに、注意してください。

<!-- 
### How many old releases should I keep in SVN?
 -->
### SVN には、古いリリースをどれくらい残しておくべき ?

<!-- 
As few as possible. Very rarely does anyone need your old code in the release repository. Remember, SVN is **not** meant for your code versioning. You can use Github for stuff like that. SVN should have your current release versions, but you don't need all the minor releases to all the previous versions. Just the last one or two for them is good.
 -->
できるだけ少なく。リリース・リポジトリにあるあなたの古いコードを必要とする人は、めったにいません。SVN はコードのバージョニングのためのものでは **ない** ことを忘れないでください。そのようなことには、GitHub を使えばいいでしょう。SVN には現在のリリース・バージョンがあるはずですが、マイナー・リリースから以前のバージョンまでは必要なものではありません。最後の1つか2つだけで十分です。

<!-- 
### Can I include SVN externals in my plugin?
 -->
### 自分のプラグインに、SVN 外部参照を含めることはできる ?

<!-- 
No. You can add [svn externals](https://svnbook.red-bean.com/en/1.0/ch07s03.html) to your repository, but they won't get added to the downloadable zip file.
 -->
いいえ。リポジトリに[svn 外部参照](https://svnbook.red-bean.com/en/1.0/ch07s03.html)を追加できますが、ダウンロード可能な zip ファイルには追加されません。

<!-- 
### Can I put zips and other compressed files in my plugin?
 -->
### 自分のプラグインに、zip などの圧縮ファイルを入れることはできる ?

<!-- 
No.
 -->
いいえ。

<!-- 
### Can I include minified JS?
 -->
### minify 化 JavaScript を含めることはできる ?

<!-- 
Yes! However you either have to keep the non-minified in your plugin _or_ direct people via your readme as to where they can get the non-minified files.
 -->
できます ! ただし、あなたのプラグインに非ミニファイ化ファイルを残しておくか、_或いは_ readme で非ミニファイ化ファイルを入手できる場所を指示する必要があります。

<!-- 
It's fine to minify, but it's not okay to hide it. All code must be human readable for inclusion in this directory.
 -->
minify 化するのは構わないが、隠すのは駄目です。このディレクトリに入れるコードは、すべて人間が読めるものでなければなりません。

<!-- 
## Your WordPress.Org Page
 -->
## Your WordPress.Org Page

<!-- 
### When does my plugin go 'live'?
 -->
### When does my plugin go 'live'?

<!-- 
As soon as you push code to the SVN folders, your plugin will be live. **DO NOT** push code if you're not ready, as there's no 'off' switch except to [close the plugin](https://developer.wordpress.org/plugins/wordpress-org/plugin-developer-faq/#closed-plugins). As closing a plugin is permanent, we recommend you not push code until you're ready to go live.
 -->
As soon as you push code to the SVN folders, your plugin will be live. **DO NOT** push code if you're not ready, as there's no 'off' switch except to [close the plugin](https://developer.wordpress.org/plugins/wordpress-org/plugin-developer-faq/#closed-plugins). As closing a plugin is permanent, we recommend you not push code until you're ready to go live.

<!-- 
### Where does the WordPress.org Plugin Directory get its data?
 -->
### Where does the WordPress.org Plugin Directory get its data?

<!-- 
From the information you specify in the plugin file and in the [readme.txt file](https://wordpress.org/plugins/developers/#readme), and from the Subversion repository itself. Read [about how the readme.txt works](https://developer.wordpress.org/plugins/wordpress-org/how-your-readme-txt-works/) for more information.
 -->
From the information you specify in the plugin file and in the [readme.txt file](https://wordpress.org/plugins/developers/#readme), and from the Subversion repository itself. Read [about how the readme.txt works](https://developer.wordpress.org/plugins/wordpress-org/how-your-readme-txt-works/) for more information.

<!-- 
You should also make full use of the [Plugin Headers](https://developer.wordpress.org/plugins/plugin-basics/header-requirements/) in your main plugin file. Those will define how your username shows up on the WordPress.org hosting page, as well as in the WordPress Admin. We recommend using all those headers to fully document your plugin.
 -->
You should also make full use of the [Plugin Headers](https://developer.wordpress.org/plugins/plugin-basics/header-requirements/) in your main plugin file. Those will define how your username shows up on the WordPress.org hosting page, as well as in the WordPress Admin. We recommend using all those headers to fully document your plugin.

<!-- 
### Can I specify what version of my plugin the WordPress.org Plugin Directory should use?
 -->
### Can I specify what version of my plugin the WordPress.org Plugin Directory should use?

<!-- 
Yes, by specifying the `Stable Tag` field in your trunk directory's [readme.txt file](https://wordpress.org/plugins/developers/#readme).
 -->
Yes, by specifying the `Stable Tag` field in your trunk directory's [readme.txt file](https://wordpress.org/plugins/developers/#readme).

<!-- 
We ask you **not** use 'trunk' as your stable tag, as that makes rollbacks more complicated than they need to be.
 -->
We ask you **not** use 'trunk' as your stable tag, as that makes rollbacks more complicated than they need to be.

<!-- 
### What version of WordPress should the "Tested Up To" value be?
 -->
### What version of WordPress should the "Tested Up To" value be?

<!-- 
Logically, whatever version you tested up to. However, never go above the current release candidate. If there is none, don't go above the active version. So if WordPress' stable release is 6.0.9, you can use 6.0 to 6.0.9 and everything will be fine. If there is a release of 6.1-RC then you may use 6.1, however you can go no higher.
 -->
Logically, whatever version you tested up to. However, never go above the current release candidate. If there is none, don't go above the active version. So if WordPress' stable release is 6.0.9, you can use 6.0 to 6.0.9 and everything will be fine. If there is a release of 6.1-RC then you may use 6.1, however you can go no higher.

<!-- 
Do not attempt to be clever and use 6.5 or 7. This will result in errors on your page.
 -->
Do not attempt to be clever and use 6.5 or 7. This will result in errors on your page.

<!-- 
### Do I need to release a new version of my plugin every time I update the readme?
 -->
### Do I need to release a new version of my plugin every time I update the readme?

<!-- 
No. If you're only making cosmetic changes to the readme or your icons/headers, you _do not_ need to release a new version. Just make sure you update the trunk and tag folders.
 -->
No. If you're only making cosmetic changes to the readme or your icons/headers, you _do not_ need to release a new version. Just make sure you update the trunk and tag folders.

<!-- 
### Do I need to release a new version of my plugin every time I update the code?
 -->
### Do I need to release a new version of my plugin every time I update the code?

<!-- 
Yes. Otherwise no one gets updated.
 -->
Yes. Otherwise no one gets updated.

<!-- 
### What should be in my changelog?
 -->
### What should be in my changelog?

<!-- 
A changelog is a log or record of all or all notable changes made to your plugin, including records of changes such as bug fixes, new features, etc. If you need help formatting your changelogs, we recommend [Keep A Changelog](https://keepachangelog.com/en/1.1.0/) as that's the format used by many products out there.
 -->
A changelog is a log or record of all or all notable changes made to your plugin, including records of changes such as bug fixes, new features, etc. If you need help formatting your changelogs, we recommend [Keep A Changelog](https://keepachangelog.com/en/1.1.0/) as that's the format used by many products out there.

<!-- 
### How many versions should I keep in my changelog?
 -->
### How many versions should I keep in my changelog?

<!-- 
Always keep the current major release in your change log. For example, if your current version is 3.9.1, you'll want that and 3.9 in the change log. Older versions should be removed and migrated to a `changelog.txt` file. That will allow them to be accessible to users, while keeping your readme shorter and more pertinent. At most, keep the most recent version of your plugin and one major version back in your readme's changelog. Your `changelog.txt` will **not** be visible within the WordPress.org Plugin Directory, but that's okay. Most users just want to know what's new.
 -->
Always keep the current major release in your change log. For example, if your current version is 3.9.1, you'll want that and 3.9 in the change log. Older versions should be removed and migrated to a `changelog.txt` file. That will allow them to be accessible to users, while keeping your readme shorter and more pertinent. At most, keep the most recent version of your plugin and one major version back in your readme's changelog. Your `changelog.txt` will **not** be visible within the WordPress.org Plugin Directory, but that's okay. Most users just want to know what's new.

<!-- 
### How do I include videos on plugin description pages?
 -->
### How do I include videos on plugin description pages?

<!-- 
For YouTube and Vimeo videos, simply paste the video link on a line by itself in your description. Note that the video must be set to allow embedding for the embed process to work. For videos hosted by the WordPress.com VideoPress service, use the `[wpvideo]` shortcode. Shortcodes can also be used for YouTube and Vimeo, if needed, just like in WordPress.
 -->
For YouTube and Vimeo videos, simply paste the video link on a line by itself in your description. Note that the video must be set to allow embedding for the embed process to work. For videos hosted by the WordPress.com VideoPress service, use the `[wpvideo]` shortcode. Shortcodes can also be used for YouTube and Vimeo, if needed, just like in WordPress.

<!-- 
### Why does my plugin say it's not been tested with the most recent WordPress versions?
 -->
### Why does my plugin say it's not been tested with the most recent WordPress versions?

<!-- 
That happens when you neglected to use a proper 'Tested Up To' value in your headers in your readme. That value should be the latest version of WordPress that you've tested your plugin against. If the latest **major** WordPress version is 4.9, then you should have the value `4.9` to indicate compatibility. You do not need to update for minor releases (if your readme is compatible to 4.9 then that will cover 4.9 through 4.9.1000).
 -->
That happens when you neglected to use a proper 'Tested Up To' value in your headers in your readme. That value should be the latest version of WordPress that you've tested your plugin against. If the latest **major** WordPress version is 4.9, then you should have the value `4.9` to indicate compatibility. You do not need to update for minor releases (if your readme is compatible to 4.9 then that will cover 4.9 through 4.9.1000).

<!-- 
Keep in mind, if you put in non-released versions of WordPress (like 6.0) you'll see the same message.
 -->
Keep in mind, if you put in non-released versions of WordPress (like 6.0) you'll see the same message.

<!-- 
### How long does it take for the Plugin Directory to reflect my changes?
 -->
### How long does it take for the Plugin Directory to reflect my changes?

<!-- 
The WordPress.org Plugin Directory updates every few minutes. However, it may take longer for your changes to appear depending on the size of the update queue. Please give it at least **6 hours** before contacting us.
 -->
The WordPress.org Plugin Directory updates every few minutes. However, it may take longer for your changes to appear depending on the size of the update queue. Please give it at least **6 hours** before contacting us.

<!-- 
### How do I make one of those cool banners for my plugin page?
 -->
### How do I make one of those cool banners for my plugin page?

<!-- 
You can make your own [plugin headers](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/#plugin-headers) by uploading the correctly named files into the `assets` folder.
 -->
You can make your own [plugin headers](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/#plugin-headers) by uploading the correctly named files into the `assets` folder.

<!-- 
Read [about plugin headers](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/#plugin-headers) for more information.
 -->
Read [about plugin headers](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/#plugin-headers) for more information.

<!-- 
### How do I make a plugin icon?
 -->
### How do I make a plugin icon?

<!-- 
You can make your own [plugin icons](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/#plugin-icons) by uploading the correctly named files into the `assets` folder.
 -->
You can make your own [plugin icons](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/#plugin-icons) by uploading the correctly named files into the `assets` folder.

<!-- 
Read [about plugin icons](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/#plugin-icons) for more information.
 -->
Read [about plugin icons](https://developer.wordpress.org/plugins/wordpress-org/plugin-assets/#plugin-icons) for more information.

<!-- 
### Can I use official logos in my plugin banner/icons?
 -->
### Can I use official logos in my plugin banner/icons?

<!-- 
Usually no.
 -->
Usually no.

<!-- 
Your plugin icon should _never_ be the unaltered, official logo of, say, Facerange. That would be infringing on their property. You may not use official logos for your branding in your banners or icons. Even if you have permission to do so on your site, _we_ don't have that permission here.
 -->
Your plugin icon should _never_ be the unaltered, official logo of, say, Facerange. That would be infringing on their property. You may not use official logos for your branding in your banners or icons. Even if you have permission to do so on your site, _we_ don't have that permission here.

<!-- 
Much like your plugin name, we recommend your icons and headers be something unique to you. They tend to be more memorable that way.
 -->
Much like your plugin name, we recommend your icons and headers be something unique to you. They tend to be more memorable that way.

<!-- 
### How many tags can I use in my readme?
 -->
### How many tags can I use in my readme?

<!-- 
Per the guidelines, [plugins are limited to 12 tags in their readme](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/#12-public-facing-pages-on-wordpress-org-readmes-must-not-spam). This is to control spam. That said, only the first **FIVE** tags will display on WordPress.org, much for the same reason. The first 12 tags are used for searches, and the rest are ignored, so tag-stuffing won't help you at all.
 -->
Per the guidelines, [plugins are limited to 12 tags in their readme](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/#12-public-facing-pages-on-wordpress-org-readmes-must-not-spam). This is to control spam. That said, only the first **FIVE** tags will display on WordPress.org, much for the same reason. The first 12 tags are used for searches, and the rest are ignored, so tag-stuffing won't help you at all.

<!-- 
In addition, any tags where you are the only one who uses them won't show, because they're not going to help anyone find another, similar, plugin.
 -->
In addition, any tags where you are the only one who uses them won't show, because they're not going to help anyone find another, similar, plugin.

<!-- 
## Plugin Names
 -->
## プラグイン名

<!-- 
### Can I change my plugin's name after it's approved?
 -->
### 承認後に、プラグイン名を変更できますか ?

<!-- 
Yes and no. You can change the display name, but the _slug_ — that part of the plugin URL that is yours — cannot be changed once a plugin is approved. That's why we warn you, multiple times, upon submission.
 -->
イエスでもありノーでもあります。表示名は変更できますが、_スラッグ_ — プラグインの URL のうち、あなたのものである部分 — は、プラグインが承認されると変更できません。そのため、申請時に何度も警告しています。

<!-- 
To change the display name, edit your main plugin file and change the value of "Plugin Name:" to the new name. You also will want to edit your header in your readme.txt to match.
 -->
表示名を変更するには、メインのプラグインファイルを編集し、「Plugin Name:」の値を新しい名前に変更してください。また、readme.txt のヘッダーもそれに合わせて編集してください。

<!-- 
### Why can't I use someone's trademark/brand as my plugin name?
 -->
### 他人の商標やブランドを、自分のプラグイン名として、なぜ使用できないのですか ?

<!-- 
Simply put, because you're not them.
 -->
簡単に言えば、あなたは彼らとは違うからです。

<!-- 
If you have written an add-on plugin for BooCommerce, you may not name it "BooCommerce Improved Product Search" as that would generate the slug `boocommerce-improved-product-search` and that would conflict with the trademark of 'BooCommerce.' That said, it would be acceptable to submit the name "Boo Improved Product Search" which would use the slug `bc-improved-product-search` ("bc" not being trademarked you see).
 -->
BooCommerce のアドオン・プラグインを作成した場合、名称「BooCommerce 改良型商品検索」は、スラッグ `boocommerce-improved-product-search` が生成され、商標「BooCommerce」と競合してしまうため、つけることはできません。とはいえ、スラッグ `bc-improved-product-search` を使用する名称「Boo 改良版商品検索」を申請できます (「bc」は商標登録されていません)。

<!-- 
As another example, if you have a plugin that integrates a service with a a popular cloud hosting company named Amazorn, you may call it "My Service Integration for Amazorn", but you may **not** use "Amazorn – My Service Integration". 
 -->
別の例として、Amazorn という人気のあるクラウドホスティング会社のサービスを統合するプラグインがある場合、「My Service Integration for Amazorn」と名付けることはできますが、「Amazorn – My Service Integration」を使うことはできま **せん**。

<!-- 
Consider the real life example of Keurig. If you made an eco-friendly brew cup, you could market it "EcoBrew Pod for Keurig" but you could NOT attempt to market it as "Keurig EcoBrew Pod." The latter implies a direct relationship to Keurig and is actually against the law in some countries. In order to protect you, we need you to tread lightly with recognized brand names and trademarks. Always err on the side of caution; if they come and tell us to close your plugin because you used their term as the _first_ word in the display name, we have to do it.
 -->
キューリグ (Keurig) の例を考えてみましょう。環境に配慮したコーヒーカップを作ったとしたら、それを「キューリグ用エコ・ブリュー・ポッド」として販売できるが、「キューリグ・エコブリュー・ポッド」として販売することは、決して許されません。後者はキューリグとの直接的な関係を意味し、国によっては法律違反となります。あなたを保護するために、認知されたブランド名や商標を慎重に扱ってください。常に慎重を期してください; もし彼らが、あなたのプラグインが、表示名の _最初の_ 単語として彼らの商標を使用していることを理由に、あなたのプラグインをクローズするように言ってきたら、私たちはそれをせざるを得ません。

<!-- 
[alert]We no longer have permission to permit new plugins to use `woo` as the start of their permalink, and are required to enforce the use of `wc` instead.[/alert]
 -->
[alert]新しいプラグインが、パーマリンクの先頭に `woo` を使用することを許可する権限がなくなり、代わりに `wc` の使用を強制することが求められています。[/alert]

<!-- 
Can a company give me permission to use their trademark in my permalink?
 -->
企業が私のパーマリンクに、その企業の商標を使用する許可を与えてくれることはありますか ?

<!-- 
No.
 -->
いいえ。

<!-- 
While we understand that companies can and do grant usage permissions, we do not accept them for permalinks for a really important reason: we _**cannot**_ change your permalink once the plugin is approved. This means if, later on, the company changes their mind and rescinds approval, the plugin will be closed and all of it's users abandoned.
 -->
私たちは、企業が使用許可を与えることができ、また与えることができることを理解していますが、本当に重要な理由から、パーマリンクについては許可していません: プラグインが承認されると、パーマリンクを変更することが出来 _**ません**_。つまり、後日、会社が考えを変えて承認を取り消した場合、プラグインはクローズされ、すべてのユーザーが見捨てられます。

<!-- 
In order to be forward thinking and proactive about a plugin's long-term life in the directory, we do not accept 'permission.' A permalink may not begin with a trademark (or commonly known brand/term) unless it is by the official owners.
 -->
プラグインがディレクトリ内で長期的に使用されることを前向きに考え、積極的に行動するために、私たちは「許可」を受け付けていません。パーマリンクは、正式な所有者によるものでない限り、商標 (または一般的に知られているブランド/ターム) で始めることはできません。

<!-- 
### Can I change my plugin's URL/slug?
 -->
### プラグインの URL/スラッグを変更できますか ?

<!-- 
It's impossible to change a plugin's URL once it's approved and we warn you about that in multiple places through the process.
 -->
一度承認されたプラグインの URL 変更は不可能で、私たちは、そのことをプロセスを通じて何度も警告しています。

<!-- 
Due to that, we deny most requests for 'new' plugins to replace old ones just to get a better slug.
 -->
そのため、より良いスラッグを得るために古いプラグインを置き換える「新しい」プラグインのリクエストはほとんどお断りしています。

<!-- 
This is because we cannot migrate users between plugins nor can we redirect traffic. This means that submitted a new plugin to change a slug is incredibly detrimental to the plugin's SEO and reputation, as users will be abandoned. The majority of plugins don't actually need a new URL, and instead just want to edit their display name.
 -->
これは、プラグイン間でのユーザー移行も、トラフィックのリダイレクトも、できないからです。つまり、スラッグを変更するために新しいプラグインを提出することは、プラグインの SEO と評判にとって信じられないほど有害であり、ユーザーは見捨てられてしまうということです。大多数のプラグインは実際には新しい URL を必要とせず、代わりに表示名を編集したいだけなのです。

<!-- 
Unless there's an egregious typo, language, or legal issue related to your slug, we are **unlikely** to approve a new slug. If we do, we will flag your account to note that future rename requests are to be denied.
 -->
あなたのスラッグに重大なタイプミス、言語、法律上の問題がない限り、新しいスラッグを承認することは **まずありません**。もし承認された場合は、今後のリネーム要求が拒否されるよう、あなたのアカウントにフラグを立てます。

<!-- 
### How do I change my plugin's display name?
 -->
### プラグインの表示名を変更するには ?

<!-- 
You'll need to change it in the readme _and_ the plugin main file.
 -->
readme _と_ プラグインのメインファイルで、変更する必要があります。

<!-- 
### Can I make my display name anything?
 -->
### 表示名は何でもいいのですか ?

<!-- 
Don't use vulgarities or slurs or other intentionally abusive language. You cannot claim, or appear to claim, to be an official source if you're not. For example, if you've made a plugin that connects to the Frozbaz Service, you should call your plugin "Connector to Frozbaz Service" – in this way, you have made it clear you are making a plugin for a service, rather than being the service.
 -->
下品な言葉や中傷、その他意図的に乱暴な言葉を使用してはなりません。公式な情報源ではない場合、公式な情報源であると主張したり、主張しているように見せかけたりしてはいけません。たとえば、Frozbaz サービスに接続するプラグインを作った場合、プラグイン名を「Connector to Frozbaz Service」とすべきです – こうすることで、サービスではなく、サービスのプラグインを作っていることが明確になります。

<!-- 
If you're combining multiple services (a payment gateway to a popular ecommerce plugin, for example), we strongly recommend you come up with an original, unique, display name.
 -->
複数のサービス (たとえば、人気の e コマースプラグインへの支払いゲートウェイ) を組み合わせる場合は、オリジナルのユニークな表示名をつけることを強くおすすめします。

<!-- 
### Can I use WordPress or Plugin in my display name?
 -->
### WordPress や Plugin を、表示名に使用できますか ?

<!-- 
Currently yes, but you shouldn't. It's incredibly redundant and doesn't actually help your SEO in any way, shape, or form. We already put WordPress _and_ Plugin in your page title.
 -->
現在のところはイエスだが、そうすべきではありません。これは信じられないほど冗長であり、実際にはどのような形であれ SEO の役には立ちません。私たちはあなたのページのタイトルにすでに WordPress _と_ Plugin を入れています。

<!-- 
### Should I use the trademark or registered symbol in my plugin name?
 -->
### プラグイン名に、商標や登録商標を使うべきですか ?

<!-- 
Assuming you actually did apply for trademarks, you certainly _can_ but it's not commonly done. Not even Google or Facebook do that. Simply by using your trademark term and having a log of it (like your SVN log), you have usually done the needed legal action required to protect your brand. Consult a lawyer for details.
 -->
実際に商標を出願したと仮定すれば、確かに _できる_ のですが、一般的には行われていません。Google や Facebook でさえ、そんなことはしません。商標タームを使用し、そのログ (SVN のログのようなもの) を残すだけで、あなたのブランドを保護するために必要な法的措置を取ることができます。詳しくは弁護士に相談してください。

<!-- 
## Search
 -->
## 検索

<!-- 
### How long will it take for my plugin to show up in search?
 -->
### 私のプラグインが検索に表示されるまで、どのくらい掛かりますか ?

<!-- 
Usually 6 to 14 days after a plugin is committed to SVN. This is because we have to add your data, parse it, and share it to all of our _heavily_ cached servers. It's not instantaneous. Also as a new plugin, we have no data on usage, so you may need to wait a bit.
 -->
プラグインが SVN にコミットされてから、通常、6日から14日後です。あなたのデータを追加し、解析し、私たちの _ヘビーな_ キャッシュサーバーすべてに共有する必要があるためです。即座に反映されるわけではありません。また、新しいプラグインである場合は、使用状況に関するデータがないので、少し待つ必要があるかもしれません。

<!-- 
### How do I rank higher?
 -->
### どうすれば、上位にランクインできますか ?

<!-- 
Write a good readme for the language, answer support posts promptly, get good reviews.
 -->
その言語のための良い readme を書き、サポートの投稿に迅速に答え、良いレビューを得ることです。

<!-- 
### What's weighted more, my URL or my display name?
 -->
### URL と表示名とでは、どっちが重みがありますか ?

<!-- 
Neither. Make your display name memorable and descriptive, while keeping it under 5 words, for maximum benefit.
 -->
どちらでもありません。最大限の効果を得るために、英単語5語以内に抑えつつ、印象的で説明的な表示名にしましょう。

<!-- 
## The Support Forums
 -->
## サポート・フォーラム

<!-- 
### How do I get notified for forums posts?
 -->
### フォーラムへの投稿を通知してもらうには ?

<!-- 
Go to `https://wordpress.org/support/plugin/_YOUR_PLUGIN_` and look at the sidebar on the right. Click the Subscribe to this Plugin button for email alerts.
 -->
`https://wordpress.org/support/plugin/_YOUR_PLUGIN_` にアクセスし、右側のサイドバーを見てください。「このプラグインを購読する」ボタンをクリックし、E メールアラートを購読します。

<!-- 
### How do I get notified for all my plugins?
 -->
### すべてのプラグインに、通知されるようにするには ?

<!-- 
Every plugin support forum page has a "Subscribe" button at the top of it. Click that and you will be emailed. You can see which plugin forums sets you are subscribed to at `https://wordpress.org/support/users/_YOUR_ID_/subscriptions`
 -->
どのプラグイン・サポートフォーラムのページにも、一番上に「購読」ボタンがあります。それをクリックするとメールが届きます。どのプラグインフォーラムに登録しているかは、右記リンクで確認できます。`https://wordpress.org/support/users/_YOUR_ID_/subscriptions`

<!-- 
For RSS, visit `https://wordpress.org/support/view/plugin-committer/_YOUR_ID_` will list all of the support requests and reviews for any plugin you have commit access. Not a committer, just someone listed as an author? Use `https://wordpress.org/support/view/plugin-contributor/_YOUR_ID_`
 -->
RSS の場合、`https://wordpress.org/support/view/plugin-committer/_YOUR_ID_` にアクセスすると、あなたがコミットアクセス権を持っているプラグインのサポートリクエストとレビューが一覧表示されます。コミッターではなく、作者としてリストアップされているだけですか ? その場合は、右記リンクを使ってください。`https://wordpress.org/support/view/plugin-contributor/_YOUR_ID_`

<!-- 
You can also go to `https://profiles.wordpress.org/_YOUR_ID_/profile/notifications/` and put in any terms you want to be emailed for. Be careful, this can escalate if you use generic terms.
 -->
また、`https://profiles.wordpress.org/_YOUR_ID_/profile/notifications/` にアクセスし、メールを送ってほしいタームを入力できます。一般的なタームを使用すると、エスカレートする可能性があるので注意してください。

<!-- 
### How do I give a support account access to my plugin?
 -->
### サポートアカウントに、自分のプラグインへのアクセス権を与えるには ?

<!-- 
You can add Support Representatives to your plugin. Support representatives can mark forum topics as resolved or sticky (same as plugin authors and contributors), but don't have commit access to the plugin.
 -->
プラグインにサポート担当者を追加できます。サポート担当者は、フォーラムのトピックに「解決済み」や「付箋」マークを付けることができます (プラグインの作者やコントリビューターと同じです) が、プラグインへのコミット権限はありません。

<!-- 
The UI for managing plugin support reps can be found in Advanced View on the plugin page, next to managing committers. Once someone is added as a support rep, they will get a Plugin Support badge when replying to the plugin support topics or reviews.
 -->
プラグインのサポート担当者を管理する UI は、プラグインページの Advanced View でコミッターの管理の隣にあります。誰かがサポート担当者として追加されると、プラグインのサポートトピックやレビューに返信する際に、プラグインサポートバッジが表示されます。

<!-- 
### Will you delete bad reviews or comments on my plugin?
 -->
### 私のプラグインに関する悪いレビューやコメントを、削除してもらえますか ?

<!-- 
Generally no. A review is a reflection of an individual's experience with your product. If they didn't like it, that's not for us to change. If you feel that a review is invalid (such as for a different plugin), use the `modlook` button on the post. A member of the **forums** team will investigate.
 -->
一般的には、ノーです。レビューとは、あなたのプロダクトに対する個人の経験を反映したものです。もしそれらを気に入らなかったとしても、私たちが変えることはできません。もしレビューが不適切だと感じたら (別のプラグインのレビューなど)、投稿にある `modlook` ボタンを使ってください。**フォーラム** チームのメンバーが調査します。

<!-- 
Abuse of the modlook feature may result in suspension of your plugins. Please, use it wisely.
 -->
modlook 機能を乱用すると、プラグインが一時的に使用停止になる場合があります。賢く使ってください。

<!-- 
### What is ‘Sockpuppeting'?
 -->
### 「ソックパペット (Sockpuppeting)」とは ?

<!-- 
That's what happens when someone makes multiple accounts on the forums, usually to give themselves a number of 5-star reviews, or create fake support tickets to appear more responsive. Sockpuppeting is against our guidelines and will result in the reviews and posts being removed, but also may result in your account and all plugins being removed. Don't do it and don't flagrantly accuse others of doing it.
 -->
これは、誰かがフォーラムに複数のアカウントを作成し、通常、5つ星のレビューを多数つけたり、偽のサポートチケットを作成し、より迅速に対応するように見せかけたりすることです。Sockpuppeting は、ガイドラインに反しており、レビューや投稿が削除されるだけでなく、あなたのアカウントやすべてのプラグインが削除される可能性があります。やめておきましょう。そして、他人がやっていることを公然と糾弾しないようにしましょう。

<!-- 
## Closed Plugins
 -->
## クローズされたプラグイン

<!-- 
### How do I close my plugin?
 -->
### 私のプラグインをクローズするには ?

<!-- 
As of April 2020, you can close your own plugins at any time. To do so, go to the **advanced** tab on your plugin page (i.e. `https://wordpress.org/plugins/_MY_PLUGIN_/advanced/`) and scroll down to the **CLOSE THIS PLUGIN** section. There you will see a warning message and a button.
 -->
2020年4月より、自分のプラグインをいつでもクローズできるようになりました。そのためには、プラグインページの **advanced** タブ (つまり `https://wordpress.org/plugins/_MY_PLUGIN_/advanced/`) に行き、**CLOSE THIS PLUGIN (このプラグインをクローズする)** セクションまでスクロールダウンしてください。そこに警告メッセージとボタンがあります。

<!-- 
![Image of the "Close this plugin" feature, with the note "WARNING: Closing your plugin is intended to be a permanent action. You will not be able to reopen it without contacting the plugins team." Below that is a button saying "I understand."](https://i3.wp.com/developer.wordpress.org/files/2020/04/HowtoClose.png)
 -->
![「警告：プラグインをクローズすることは永久的な行為です。プラグイン・チームに連絡しない限り、プラグインを再オープンできません。」の注記付き、「CLOSE THIS PLUGIN」機能の画像。その下に「I understand.」というボタンがある。](https://i3.wp.com/developer.wordpress.org/files/2020/04/HowtoClose.png)

<!-- 
If you agree to the warning, and want to close your plugin, press the button.
 -->
警告に同意し、プラグインをクローズしたい場合は、ボタンを押してください。

<!-- 
Keep in mind, you _will not_ get your plugin restored unless you can justify your situation. Closing a plugin by request is intended to be **permanent**.
 -->
自分の状況を正当化できない限り、プラグインを復活させることは _できない_ ことを覚えておいてください。リクエストによるプラグインのクローズは **永続的** であることを意図しています。

<!-- 
### What if I accidentally closed my plugin?
 -->
### 私のプラグインを、誤ってクローズしてしまったら ?

<!-- 
Email `plugins@wordpress.org` and ask to please have your plugin reopened. However you will be asked how you managed to do that so that we can improve the functionality of the feature.
 -->
`plugins@wordpress.org` にメールを送り、プラグインを再オープンしてくださいとお願いしてください。ただし、この機能の機能性を向上させるために、どのように管理したかを尋ねられます。

<!-- 
### Why won't it let me close my own plugin?
 -->
### 私のプラグインを、なぜクローズできないの ?

<!-- 
Assuming you're logged in as the correct account, it's probably because you have too many users. If your plugin has more than 10,000 users, you will need to email `plugins@wordpress.org` and request for us to close it.
 -->
正しいアカウントでログインしていると仮定すると、おそらくユーザー数が多すぎることが原因です。もしあなたのプラグインのユーザー数が1万人以上であれば、`plugins@wordpress.org` にメールを送り、プラグインをクローズするようリクエストする必要があります。

<!-- 
### Can I temporarily close my plugin?
 -->
### 私のプラグインを、一時的にクローズできるの ?

<!-- 
No.
 -->
いいえ。

<!-- 
We do not permit this as it creates a poor experience for users. Hiding plugins makes users think the plugin has been pulled for security or guideline issues, which causes them not to trust you anymore. We cannot prevent what they think, so instead we prohibit 'temporary' closures.
 -->
このような行為は、ユーザーにとって好ましくない体験となるため、私たちは許可していません。プラグインを非表示にすることで、ユーザーはそのプラグインがセキュリティやガイドラインの問題で削除されたと思い、あなたのことを信用しなくなります。そのため、私たちは「一時的な」クローズを禁止しています。

<!-- 
Generally people want to do this when their plugin has a bug that is being fixed, or when they're unable to support it. We recommend you instead just fix the bug as soon as possible, or if you cannot support the plugin, update the readme to say it's currently unsupported and why.
 -->
一般的に、プラグインに修正中のバグがあるときや、サポートできないときに、このようなことをしたがります。その代わりに、できるだけ早くバグを修正するか、プラグインをサポートできない場合は、readme を更新して、現在のところサポートされていないこととその理由を書くことをおすすめします。

<!-- 
If this is for a brand new plugin, you should just call it a 'public beta' so people are aware of the status.
 -->
新しいプラグインの場合、「パブリックベータ」と呼ぶべきです。そうすることで、人々は状態を認識できます。

<!-- 
### What happens when a plugin is closed?
 -->
### プラグインがクローズされると、どうなるの ?

<!-- 
When a plugin is closed, the page shows as closed and the zips are no longer generated. No one will be able to download the plugin via the website, nor will they be able to install it via the WordPress admin. The SVN repository will remain accessible to allow others to download and fork the code if desired, per the tenets of the directory.
 -->
プラグインがクローズされると、ページはクローズされたと表示され、zip は生成されなくなります。Web サイトからプラグインをダウンロードすることも、WordPress 管理画面からインストールできなくなります。SVN リポジトリは、ディレクトリの方針に従って、必要であれば他の人がコードをダウンロードしてフォークできるようにアクセス可能なままです。

<!-- 
After 60 days, the closure message will change to alert people as to _why_ it was closed but only in the broadest terms (Guideline Violation, Security, etc) and not with explicit details.
 -->
60日を過ぎると、クローズメッセージは _なぜ_ クローズされたかを警告するものに変わりますが、大まかなものであって (ガイドライン違反、セキュリティなど)、明確な詳細は記載されません。

<!-- 
### Why was my plugin closed?
 -->
### 私のプラグインは、なぜクローズされたの ?

<!-- 
Plugins are closed for guideline violations, security issues, or by author requests. In the case of active issues (such as copyright infringement, abuse, and security), all accounts with commit access to a plugin are notified.
 -->
プラグインは、ガイドライン違反、セキュリティの問題、作者のリクエストによってクローズされます。アクティブな問題 (著作権侵害、不正使用、セキュリティなど) の場合、プラグインにコミットできるすべてのアカウントに通知されます。

<!-- 
If a plugin has never been used within 6 months (i.e. no code has been pushed to SVN), SVN is broken for upwards of 12 months, or a plugin's readme indicates it's deprecated, we _may_ close without notification.
 -->
プラグインが6ヵ月以内に一度も使われていない (つまり、SVN にコードがプッシュされていない) 場合、SVN が12ヵ月以上壊れている場合、またはプラグインの readme が非推奨であることを示している場合、通知なしにクローズすることが _あります_。

<!-- 
### Why was someone else's plugin closed?
 -->
### 他人のプラグインは、なぜクローズされたの ?

<!-- 
As of 2017, plugin closure reasons are tracked in the plugin database. Sixty days after a plugin is closed, the reason for the closure will be made public:
 -->
2017年現在、プラグインのクローズ理由はプラグイン・データベースで追跡されます。プラグインがクローズされてから60日後に、クローズ理由が公開されます:

<!-- 
![Example of a closed plugin with the reason 'Author Request'](https://i3.wp.com/developer.wordpress.org/files/2015/04/not-hello-dolly.jpg)
 -->
![ 「作者のリクエスト」という理由でクローズされたプラグインの例](https://i3.wp.com/developer.wordpress.org/files/2015/04/not-hello-dolly.jpg)

<!-- 
Please note: We do not publicly disclose the details on exactly why a plugin has been closed.
 -->
注意: プラグインがクローズされた、正確な理由の詳細は公表していません。

<!-- 
### Can I get someone else's plugin closed?
 -->
### 他人のプラグインを、クローズしてもらうことはできるの ?

<!-- 
If you report an [security issue](https://developer.wordpress.org/plugins/wordpress-org/plugin-security/reporting-plugin-security-issues/) or a [guideline violation](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/) in a plugin to `plugins@wordpress.org`, we will review and take appropriate action. Most of the time, this involves closing a plugin. Your name will not be disclosed unless you ask for it to be so, in order to protect you from backlash.
 -->
プラグインに関する[セキュリティ上の問題](https://developer.wordpress.org/plugins/wordpress-org/plugin-security/reporting-plugin-security-issues/)や[ガイドライン違反](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/)を `plugins@wordpress.org` に報告いただいた場合、プラグインを確認し、適切な処置をとらせていただきます。ほとんどの場合、プラグインをクローズすることになります。反感からあなたを守るため、あなたが要求しない限り、あなたの名前は公表されません。

<!-- 
### Someone posted a copy of my plugin! What do I do?
 -->
### 私のプラグインのコピーを誰かが投稿した ! どうすればいい ?

<!-- 
Email `plugins@wordpress.org` with a link to the stolen plugin. Include either a link to where we can download yours or attach the zip. We will compare the two files, as well as all the coding history we have, to determine if the plugin is, indeed, theft, or just an uncredited fork.
 -->
盗まれたプラグインへのリンクを `plugins@wordpress.org` にメールしてください。あなたのプラグインをダウンロードできる場所へのリンクか、zip ファイルを添付してください。私たちは2つのファイルと、私たちが持っているすべてのコーディング履歴を比較して、そのプラグインが本当に盗用なのか、それとも単なるクレジットされていないフォークなのかを判断します。

<!-- 
Keep in mind, if you licensed your plugin as GPLv2 or later, then it's perfectly permissible to fork your work, as long as copyright remains intact and you're credited.
 -->
もしあなたが自分のプラグインを GPLv2 またはそれ以降でライセンスしているのであれば、著作権が損なわれず、あなたの名前がクレジットされている限り、あなたの作品をフォークすることは完全に許されていることを覚えておいてください。

<!-- 
### What do I do if someone copied some of my code and didn't credit me?
 -->
### もし誰かが私のコードをコピーし、クレジットをくれなかった場合、どうすればいい ?

<!-- 
Email `plugins@wordpress.org` right away! **Especially** if your code was non-GPL. While we do permit people to fork other plugins and include that code in their own plugins, it must be credited at all times. Copyright and credits are a requirement.
 -->
すぐに `plugins@wordpress.org` にメールしてください ! あなたのコードが非 GPL であった場合は、**特に**。私たちは他のプラグインをフォークして、そのコードを自分のプラグインに含めることを許可していますが、常にクレジットを付けなければなりません。著作権とクレジットは必須条件です。

<!-- 
### Will you close another plugin for violating a brand/trademark?
 -->
### ブランド/商標を侵害したとして、他のプラグインをクローズしますか ?

<!-- 
We do our best to uphold copyright and trademark requirements, as well as prevent brand confusion. Before plugin are approved, we often require them to make some of the more obvious changes. That said, there is a limit to how 'different' a URL or name can be when we have 60,000 plugins in the directory, and when some terms are quite common (like 'popup' or 'all-in-one'). Because of that, we require developers to change the plugin's **display name** to no longer cause conflict or confusion.
 -->
私たちは、著作権や商標の要件を守り、ブランドの混乱を防ぐために最善を尽くします。プラグインが承認される前に、私たちはしばしば、より明白ないくつかの変更を要求します。とはいえ、ディレクトリに6万ものプラグインがあり、いくつかのタームが非常に一般的である場合 (「ポップアップ」や「オールインワン」など)、URL や名前が「異なる」ことには限界があります。そのため、私たちは開発者にプラグインの **表示名** を変更し、衝突や混乱を起こさないようにすることを求めています。

<!-- 
If someone is clearly infringing on your copyright or trademark or existing brand, be it by display name or use of trademarked images, please email us at `plugins@wordpress.org` with some proof and we will contact the developer and require changes.
 -->
もし誰かがあなたの著作権や商標、または既存のブランドを明らかに侵害している場合、それが表示名であれ、商標登録された画像の使用であれ、`plugins@wordpress.org` 宛に証拠を添えてメールしていただければ、開発者に連絡し、変更を求めます。

<!-- 
We do expect these to be _reasonable_ requests. That is, if you send us a complaint and list 12 plugins that all use the term 'best contact form' because that's your plugin name, we will review the plugins and only close them if they're using the phrase excessively. If they use it once (i.e. "This is the best contact form plugin in the Faroe Islands") then it's acceptable. If they're keyword stuffing the phrase, we're more likely to close them for keyword stuffing. Simply, if your plugin name is super generic, this is going to happen, and it's usually **not** an infringement case.
 -->
私たちはこれらが _妥当な_ 要求であることを期待しています。つまり、もしあなたが私たちに苦情を送り、それがあなたのプラグイン名だからという理由で「最高のコンタクトフォーム」という言葉を使った12のプラグインをリストアップした場合、私たちはそのプラグインをレビューし、そのフレーズを過度に使っている場合のみクローズします。一度だけ使用されている場合 (つまり、「これはフェロー諸島で最高のコンタクトフォームプラグインです」) は、許容範囲です。キーワードの詰め込みをしている場合は、キーワードの詰め込みでクローズする可能性が高くなります。単純に、あなたのプラグイン名が超汎用的であれば、このようなことが起こるでしょうし、それは通常、侵害訴訟にはなり **ません**。

<!-- 
Also note that if it's not **your** trademark, we cannot accept your report. It is the responsibility of the trademark owners, not it's users, to manage and maintain that.
 -->
また、それが **あなたの** 商標でない場合、我々はあなたの報告を受け入れることができないことに注意してください。それを管理・維持するのは、ユーザーではなく商標所有者の責任です。

<!-- 
### How can I send a security report?
 -->
### セキュリティ・レポートを送信するには ?

<!-- 
Email `plugins@wordpress.org` a clear and concise description of the issue. [Please read our document on reporting security issues for details](https://developer.wordpress.org/plugins/wordpress-org/plugin-security/reporting-plugin-security-issues/).
 -->
`plugins@wordpress.org` 宛てに、問題の明確で簡潔な説明をメールしてください。詳細については、[セキュリティ問題の報告に関する文書](https://developer.wordpress.org/plugins/wordpress-org/plugin-security/reporting-plugin-security-issues/)をお読みください。

<!-- 
### Do you provide bounties for finding bugs in a plugin?
 -->
### プラグインのバグを発見した場合、報奨金は出るの ?

<!-- 
No. We have no relationship with any bug bounty programs, so we don't file your reports etc to them. The only one with which we work is [hackerone.com/automattic](https://hackerone.com/automattic) and that's for bugs related to Automattic properties. Everything else is on your own, don't ask us to submit things.
 -->
いいえ。私たちはバグ報奨金プログラムとは何の関係もありませんので、バグ報告などを提出することはありません。唯一提携しているのは [hackerone.com/automattic](https://hackerone.com/automattic) のみで、Automattic のプロパティに関連するバグが対象です。それ以外はすべて各自で行ってください。私たちに提出を求めないでください。

<!-- 
### Do you help file or provide CVEs?
 -->
### CVE (Common Vulnerabilities and Exposures。共通脆弱性識別子) のファイリングや提供を手伝ってますか ?

<!-- 
No. We do not have the ability to assist with CVEs.
 -->
いいえ。我々には CVE を支援する能力はありません。

<!-- 
### My plugin was closed, can I reopen it?
 -->
### 私のプラグインがクローズされたのですが、再オープンできますか ?

<!-- 
Maybe. If it was closed for a security reason, fix the issue, reply to the email, and most of the time we'll reopen the plugin unless it has more security issues or severe guideline issues. If it was closed for guideline violations, it depends on the severity and nature of the violation. Repeat offenders are less likely to have a plugin reopened, for example, than first-timers.
 -->
多分。セキュリティ上の理由でクローズされた場合は、問題を修正し、メールに返信してください。ほとんどの場合、セキュリティ上の問題やガイドラインの重大な問題がない限り、プラグインを再オープンします。ガイドライン違反でクローズされた場合は、違反の度合いと性質によります。たとえば、度重なる違反者は、初めての違反者よりもプラグインを再オープンする可能性は低くなります。

<!-- 
If you asked for the plugin to be closed, you will be expected to explain why the change of heart. Plugins are intended to remain closed when a developer requests it, and not reopened again a month later.
 -->
もしあなたがプラグインのクローズを要求した場合、その心変わりの理由を説明することが求められます。プラグインは、開発者がそれを要求したときにクローズされることを意図しており、そして、1ヵ月後に再オープンされることはありません。

<!-- 
_All_ plugins must pass a current standards and security review in order to be restored. This is not optional. Users will lose more faith in you for having your plugin closed multiple times than they would for one longer closure where you address all the potential issues.
 -->
_すべての_ プラグインを復活させるには、現在の標準とセキュリティの審査に合格する必要があります。これは任意ではありません。プラグインが何度もクローズされることは、潜在的な問題にすべて対処する1回のクローズよりも、ユーザーからの信頼を失います。

<!-- 
### Why was my plugin closed when it was my employee/co-worker who violated guidelines?
 -->
### ガイドラインに違反したのは私の従業員/同僚なのに、私のプラグインがなぜクローズされたの ?

<!-- 
Everyone who represents a plugin, from support tech to developer, is the responsibility of the plugin owner. If they violate the guidelines egregiously, then the owners are expected to accept those consequences and correct course. When that doesn't happen, plugins get closed. We notify the plugin owners in these cases and explain why and do our best to keep plugins open.
 -->
サポート技術者から開発者に至るまで、プラグインを代表するすべての人は、プラグイン・オーナーの責任です。もし彼らがガイドラインにひどく違反した場合、オーナーはその結果を受け入れ、軌道修正することが期待されます。そうならない場合、プラグインはクローズされます。このような場合、私たちはプラグイン・オーナーに通知し、理由を説明し、プラグインをオープンし続けるために最善を尽くします。

<!-- 
### _All_ my plugins were closed! How can I get them back?
 -->
### 私のプラグインが _全て_ クローズされました ! どうしたら元に戻せますか ?

<!-- 
It's exceptionally rare that we close all of a developer's plugins. In general it happens because of the following:
 -->
開発者のプラグインをすべてクローズすることは、極めて稀です。一般的には、以下のような理由で起こります:

<!-- 
1. You asked us to close all your plugins.
2. Email issues.
  1. The email bounced and we were unable to get in touch.
  2. The email sent us auto-replies and warnings were sent at least twice to fix that.
3. Guideline issues.
  1. Previous censuring for behaviour and/or a final warning was issued.
  2. Delivering legal threats to the directory and/or the volunteers.
  3. The violation was deemed 'egregious' (death threats, hundreds of sock puppets, harassment, etc).
 -->
1. あなたが、すべてのプラグインをクローズするように依頼した。
2. E メールの問題。
  1. E メールが拒否され、連絡が取れなかった。
  2. E メールが自動返信され、それを修正するために警告が少なくとも2回送られた。
3. ガイドラインの問題。
  1. 過去に行動を厳しく咎められ、最終警告を受けたことがある。
  2. ディレクトリおよび/またはボランティアに、法的脅威を提供した。
  3. 違反が「ひどい」と判断された (殺害予告、何百ものソックパペット、嫌がらせなど)。

<!-- 
If you asked us to close them, you have to explain _why_ the change of heart.
 -->
クローズするよう要請したのであれば、その心変わりの _理由_ を説明しなければなりません。

<!-- 
If you're having email issues, you have to resolve them and you'll be required to bring all your plugins up to current standards of security and guidelines.
 -->
E メールに問題があれば、それを解決しなければならないし、すべてのプラグインを現在のセキュリティ基準やガイドラインに合わせることが求められることになるでしょう。

<!-- 
As for that last one … Generally you don't get to come back from that. If we deliver you a final warning for your behaviour and, within less than a year, you start up again with the issues (or fail to resolve all the issues we mentioned), we're not going to reopen your plugins.
 -->
最後の件については … 一般的に、あなたはそこから戻ってくることはないでしょう。もし私たちがあなたの行動に対して最終警告を出し、1年以内にあなたが再び問題を起こした場合 (あるいは私たちが述べたすべての問題を解決できなかった場合)、私たちはあなたのプラグインを再オープンするつもりはありません。

<!-- 
### I just got a final warning. What do I do?
 -->
### 最終警告を受けたばかりです。どうすればいい ?

<!-- 
First and foremost, _take it seriously_. The email will list exactly what the problems have been and why we've chosen to escalate to a final warning. Plugin Owners are expected to resolve all the issues, to cease causing new guideline violations, and to closely monitor the actions of any coworkers. In short, stop breaking the guidelines, stop making excuses, apologize for any misbehaviour, and correct course.
 -->
何よりもまず、_真摯に受け止める_ ことが大切です。この E メールには、どのような問題があったのか、なぜ最終警告までエスカレーションすることになったのかが正確に記載されます。プラグイン・オーナーは、すべての問題を解決し、新たなガイドライン違反を起こさないようにし、同僚の行動を注意深く監視することが期待されています。要するに、ガイドライン違反をやめ、言い訳をするのをやめ、不作法を謝罪し、軌道修正してください。

<!-- 
The last thing we want to do is ban someone and disable all their plugins. It's not healthy for the community. At the same time, if a developer is unable or unwilling to play by the same rules as everyone else, it's detrimental to keep then in the directory and disrespectful to everyone else.
 -->
私たちが一番やりたくないことは、誰かを BAN (アカウント停止) して、その人のプラグインをすべて使えなくすることです。それはコミュニティにとって健全ではありません。同時に、もし開発者が他の人と同じルールを守れない、あるいは守りたくないのであれば、ディレクトリに残しておくことは有害であり、他の人たちにも敬意を払わないことになります。

<!-- 
## Plugin Ownership
 -->
## プラグインの所有権

<!-- 
### How do I give someone else access to my plugin?
 -->
### 自分のプラグインに、他の人がアクセスできるようにするには ?

<!-- 
To add users as committers, that is give them access to update code, go to `https://wordpress.org/plugins/_YOUR_PLUGIN_/advanced` and add their username in as a committer.
 -->
ユーザーをコミッターとして追加する、つまり、彼らにコードを更新する権限を与えるには、`https://wordpress.org/plugins/_YOUR_PLUGIN_/advanced` に行き、彼らのユーザー名をコミッターとして追加します。

<!-- 
To have them show up as an author, add their username to the `readme.txt` file.
 -->
作者として表示させるには、ファイル `readme.txt` に、彼らのユーザー名を追加してください。

<!-- 
_Do not add regular users as authors._ It's meant for people who help with development only. This means if someone 'inspired' you, you should not add them as an author.
 -->
_一般ユーザーを、作者として追加しないでください。_ これは、開発を手伝ってくれる人だけのためのものです。つまり、誰かがあなたに「インスピレーション」を与えたとしても、その人を作者として加えるべきではありません。

<!-- 
### How do I remove someone's access from my plugin?
 -->
### 自分のプラグインから、誰かのアクセスを削除するには ?

<!-- 
Anyone with commit access can do this. Go to `https://wordpress.org/plugins/_YOUR_PLUGIN_/advanced` and hover over their ID. A delete link will appear. Click on it.
 -->
コミットにアクセスできる人なら誰でもできます。`https://wordpress.org/plugins/_YOUR_PLUGIN_/advanced` にアクセスして、彼らの ID にカーソルを合わせてください。削除リンクが表示されます。それをクリックしてください。

<!-- 
Please don't delete yourself.
 -->
どうか自分自身を削除しないでください。

<!-- 
### How do I change the plugin owner?
 -->
### プラグインの所有者を変更するには ?

<!-- 
Go to the Advanced tab and scroll down to the Danger Zone. There you will see a section for **Transfer Your Plugin**. Pick someone from the dropdown and click the button.
 -->
「Advanced」タブに行き、「Danger Zone」までスクロールダウンします。そこに **Transfer Your Plugin (プラグインを譲渡する)** のセクションがあります。ドロップダウンから誰かを選び、ボタンをクリックしてください。

<!-- 
For more details, please read the [documentation on transferring plugins](https://developer.wordpress.org/plugins/wordpress-org/transferring-your-plugin-to-a-new-owner/).
 -->
詳しくは、[プラグインの譲渡に関するドキュメント](https://developer.wordpress.org/plugins/wordpress-org/transferring-your-plugin-to-a-new-owner/)をお読みください。

<!-- 
### I tried to transfer my plugin but it says I can’t. Why not?
 -->
### プラグインを譲渡しようとしたのですが、できないと言われました。なぜですか ?

<!-- 
Plugins with a large number of users (over 10,000) or ones that are deemed critical to the WordPress project (such as featured or beta plugins) can only be transfered via written request to the plugins team. [Please read the documentation on transfering plugins for details](https://developer.wordpress.org/plugins/wordpress-org/transferring-your-plugin-to-a-new-owner/).
 -->
ユーザー数が多い (1万人以上) プラグインや、WordPress プロジェクトにとって重要であると判断されたプラグイン (注目プラグインやベータ版プラグインなど) は、プラグインチームへの書面によるリクエストによってのみ、譲渡できます。詳しくは、[プラグインの譲渡に関するドキュメント](https://developer.wordpress.org/plugins/wordpress-org/transferring-your-plugin-to-a-new-owner/)をお読みください

<!-- 
### How can I take over an abandoned plugin?
 -->
### 放置されたプラグインを引き継ぐには ?

<!-- 
[We permit users to adopt existing plugins that are no longer currently developed](https://developer.wordpress.org/plugins/wordpress-org/take-over-an-existing-plugin/).
 -->
[私たちは、現在開発されていない既存プラグインの引き継ぎをユーザーに許可しています](https://developer.wordpress.org/plugins/wordpress-org/take-over-an-existing-plugin/)。

<!-- 
We ask you try to connect with the original developers first, so they can add you. In some case, that's not possible and you should start with fixing the plugin. Make sure it meets coding standards, is secure, and update the copyright information to include yourself. Then you can contact us regarding [plugin adoption](https://developer.wordpress.org/plugins/wordpress-org/take-over-an-existing-plugin/).
 -->
まずはオリジナルの開発者と連絡を取ってみてください。そうすれば、彼らはあなたをコミッターとして追加できます。場合によっては、それが不可能で、プラグインの修正から始める必要があります。コーディング標準を満たしていること、安全であることを確認し、あなた自身を含めるために著作権情報を更新してください。その後、[プラグインの引き継ぎ](https://developer.wordpress.org/plugins/wordpress-org/take-over-an-existing-plugin/)について私たちに連絡してください。

<!-- 
We offer **no** guarantee that you will be given anyone's plugin, even following a successful review.
 -->
たとえレビューが成功しても、あなたが誰かのプラグインを与えられることを、私たちは、**一切** 保証しません。

<!-- 
### Are these offers to buy my plugin legit?
 -->
### 私のプラグインを買おうというオファーは、合法ですか ?

<!-- 
Short answer: Probably not.
 -->
簡潔な答え: おそらく無理でしょう。

<!-- 
Many developers receive unsolicited emails or offers to purchase their plugin. We have found the vast majority of these to be fraudulent and do _not_ recommend you follow up with them.
 -->
多くの開発者が、迷惑メールやプラグイン購入のオファーを受け取っています。私たちは、これらの大半が詐欺であることを発見しており、そのようなメールに従うことをおすすめ _しません_。

<!-- 
While legitimate offers do come, they're usually from the official company to whom a plugin is related, or from a well established plugin company. The ones that start "We're reaching out to the WordPress community …" or "We are looking to acquire existing WordPress plugins …" should not be trusted. Such purchases have often destroyed the reputation of the plugin (and the original developer) by engaging in sleazy tactics such as tracking users or other serious guideline violations.
 -->
合法的なオファーが来ることはありますが、たいていはプラグインが関連する公式の会社か、十分に確立されたプラグイン会社からのものです。「WordPress コミュニティに働きかけています…」や「既存の WordPress プラグインを買収しようとしています…」で始まるものは、信用してはいけません。このような買収は、ユーザーを追跡したり、その他の深刻なガイドライン違反のような卑劣な戦術に関与することによって、プラグイン (および元の開発者) の信用をしばしば破壊してきました。

<!-- 
If you do choose to sell your plugin (or give it away to someone else), please make sure the new owners understand all the [guidelines of the repository](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/). Should they violate our terms the plugin will be removed, and we may not give it back depending on the level of the violation. Whomever has commit access to a plugin has the ownership and responsibility of it's behavior for users. Spamming, inserting tracking data, and adding junk features are the fastest way to ruin your plugin.
 -->
もしプラグインを売却する (または他の人に譲る) 場合は、新しい所有者が[リポジトリのガイドライン](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/)をすべて理解していることを確認してください。私たちの規約に違反した場合、プラグインは削除され、違反の度合いによってはプラグインを返さないこともあります。プラグインへのコミットアクセス権を持っている人は、そのプラグインの所有権を持ち、ユーザーに対する振る舞いに責任を負います。スパム、トラッキングデータの挿入、ジャンクな機能の追加は、あなたのプラグインを台無しにする最も早い方法です。

<!-- 
We advocate only giving your plugin to people you _personally_ have vetted, and that you trust with being responsible with your code and your users.
 -->
あなたのコードとユーザーに対して責任を負うということを信頼して、あなたが _個人的に_ 吟味した人にのみ、プラグインを提供することを、私たちは、推奨しています。

<!-- 
### What happens when a plugin developer dies?
 -->
### プラグイン開発者が亡くなったら、どうなりますか ?

<!-- 
When a developer is determined to have died, they are removed from their own plugins in order to prevent the unethical from gaining access and harming users. If they are the only developer, the plugin may be closed. All attempts are made to find their friends and coworkers, to offer them a chance to adopt the code first, but if no one reliable or willing can be found the plugin is closed.
 -->
開発者が死亡したと判断された場合、倫理に反する者がアクセスし、利用者に危害を加えることを防ぐために、その開発者は自分のプラグインから削除されます。もし開発者がその人だけであれば、プラグインはクローズされるかもしれません。開発者の友人や同僚を見つけ、彼らにコードを引き継ぐ機会を与えようと試みますが、信頼できる人や意欲的な人が見つからない場合、プラグインは閉鎖されます。
