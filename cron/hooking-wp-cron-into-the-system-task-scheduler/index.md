<!-- 
# Hooking WP-Cron Into the System Task Scheduler
 -->
# WP-Cron をシステム・タスク・スケジューラーにフック

<!-- 
As previously mentioned, WP-Cron does not run continuously, which can be an issue if there are critical tasks that must run on time. There is an easy solution for this. Simply set up your system's task scheduler to run on the intervals you desire (or at the specific time needed). The easiest solution is to use a tool to make a web request to the `wp-cron.php` file.
 -->
前述したように、WP-Cron は継続的に実行されませんので、時間通りに実行しなければならない重要なタスクがある場合には、問題となります。これには簡単な解決策があります。システムのタスク・スケジューラーを設定し、必要な間隔で (または必要な特定の時間に) 実行させるだけです。最も簡単な解決策は、ファイル `wp-cron.php` に Web リクエストを行うツールを使用することです。

<!-- 
After scheduling the task on your system, there is one more step to complete. WordPress will continue to run WP-Cron on each page load. This is no longer necessary and will contribute to extra resource usage on your server. WP-Cron can be disabled in the `wp-config.php` file. Open the `wp-config.php` file for editing and add the following line:
 -->
システム上でタスクをスケジューリングした後、ステップがもう一つあります。WordPress は各ページのロード時に WP-Cron を実行し続けます。これはもはや必要なく、サーバーのリソースを余分に使用することになります。WP-Cron は、ファイル `wp-config.php` で無効にできます。ファイル `wp-config.php` を開いて編集し、以下の行を追加してください:

```
define( 'DISABLE_WP_CRON', true );
```

<!-- 
## Windows
 -->
## Windows

<!-- 
Windows calls their time based scheduling system the Task Scheduler. It can be accessed via the **Administrative Tools** in the control panel.
 -->
Windows では、時間ベースのスケジューリング・システムを「タスク・スケジューラー」と呼んでいます。コントロールパネルの **管理ツール** からアクセスできます。

<!-- 
How you setup the task varies with server setup. One method is to use PowerShell and a Basic Task. After creating a Basic Task the following command can be used to call the WordPress Cron script.
 -->
タスクをどのようにセットアップするかは、サーバーのセットアップによって異なります。一つの方法は、PowerShell と基本タスクを使用することです。基本タスクを作成した後、以下のコマンドを使って WordPress Cron スクリプトを呼び出すことができます。

```
powershell "Invoke-WebRequest http://YOUR_SITE_URL/wp-cron.php"
```

<!-- 
## MacOS and Linux
 -->
## macOS と Linux

<!-- 
Mac OS X and Linux both use cron as their time based scheduling system. It is typically access from the terminal with the `crontab -e` command. It should be noted that tasks will be run as a regular user or as root depending on the system user running the command.
 -->
macOS も Linux も、時間ベースのスケジューリング・システムとして cron を使用しています。通常、ターミナルからコマンド `crontab -e` でアクセスします。コマンドを実行するシステムユーザーによって、タスクは一般ユーザーとして実行されるか、root として実行されることに注意してください。

<!-- 
Cron has a specific syntax that needs to be followed and contains the following parts:
 -->
Cron には従うべき特定の構文があり、以下のパーツから構成されています:

<!-- 
- Minute
- Hour
- Day of month
- Month
- Day of week
- Command to execute
 -->
- 分 (Minute)
- 時 (Hour)
- 日 (Day of month)
- 月 (Month)
- 曜日 (Day of week)
- 実施するコマンド

<!-- 
![Cron Scheduling](https://i3.wp.com/developer.wordpress.org/files/2014/10/plugin-wp-cron-cron-scheduling.png)
 -->
![Cron スケジューリング](https://i3.wp.com/developer.wordpress.org/files/2014/10/plugin-wp-cron-cron-scheduling.png)

<!-- 
If a command should be run regardless of one of the time sections an asterisk (`*`) should be used. For example if you wanted to run a command every 15 minutes regardless of the hour, day, or month it would look like:
 -->
時間セクションのいずれかに関係なくコマンドを実行する場合は、アスタリスク (`*`) を使用します。たとえば、時・日・月に関係なく15分ごとにコマンドを実行したい場合は、以下のようになります:

<!-- 
Many servers have `wget` installed and this is an easy tool to call the WordPress Cron script.
 -->
多くのサーバーには `wget` がインストールされていて、これは WordPress の Cron スクリプトを呼び出すための簡単なツールです。

```
wget --delete-after https://example.com/wp-cron.php
```

<!-- 
[info]Without –delete-after option, wget would save the output of the HTTP GET request.[/info]
 -->
[info]`--delete-after` オプションがない場合、`wget` は、HTTP GET リクエストの出力を保存します。[/info]

<!-- 
A daily call to your site's WordPress Cron that triggers at midnight every night could look similar to:
 -->
毎日、毎晩深夜にトリガーされる、あなたのサイトの WordPress Cron への呼び出しは、次のようになります:

```
0 0 * * * wget --delete-after https://example.com/wp-cron.php
```