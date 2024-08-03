<!-- 
# Cron
 -->
# Cron

<!-- 
## What is WP-Cron
 -->
## WP-Cron とは

<!-- 
WP-Cron is how WordPress handles scheduling time-based tasks in WordPress. Several WordPress core features, such as checking for updates and publishing scheduled post, utilize WP-Cron. The "Cron" part of the name comes from the cron time-based task scheduling system that is available on UNIX systems.
 -->
WordPress に於ける時間ベースのタスク・スケジューリング方法として、WP-Cron があります。更新のチェックや 予約投稿の公開など、いくつかの WordPress のコア機能は WP-Cron を利用しています。WP-Cron の「Cron」は、UNIX システムで利用可能な時間ベースのタスク・スケジューリングシステム「cron」に由来しています。

<!-- 
WP-Cron works by checking, on every page load, a list of scheduled tasks to see what needs to be run. Any tasks due to run will be called during that page load.
 -->
WP-Cron は、すべてのページロード時に、予定されたタスクのリストをチェックし、何を実行する必要があるかを確認することによって動作します。実行が予定されているタスクは、そのページのロード中に呼び出されます。

<!-- 
[info]WP-Cron does not run constantly as the system cron does; it is only triggered on page load.[/info]
 -->
[info]WP-Cron は、システム cron のように常時実行されません。ページロード時にのみ起動します。[/info]

<!-- 
Scheduling errors could occur if you schedule a task for 2:00PM and no page loads occur until 5:00PM.
 -->
午後02時にタスクを予定し、午後05時までページロードが発生しなかった場合、スケジューリング・エラーが発生する可能性があります。

<!-- 
## Why use WP-Cron
 -->
## WP-Cron を使用する理由

<!-- 
- WordPress core and many plugins need a scheduling system to perform time-based tasks. However, many hosting services are shared and do not provide access to the system scheduler.
- Using the WordPress API is a simpler method for setting scheduled tasks than going outside of WordPress to the system scheduler.
- With the system scheduler, if the time passes and the task did not run, it will not be re-attempted. With WP-Cron, all scheduled tasks are put into a queue and will run at the next opportunity (meaning the next page load). So while you can’t be 100% sure _when_ your task will run, you can be 100% sure that it will run _eventually_.
 -->
- WordPress のコアと多くのプラグインは、時間ベースのタスクを実行するためにスケジューリングシステムを必要とします。しかし、多くのホスティングサービスは共有であり、システムスケジューラへのアクセスを提供していません。
- WordPress API を使用することは、WordPress の外からシステムスケジューラにアクセスするよりも、予約タスクをよりシンプルに設定する方法です。
- システムスケジューラでは、時間が経過してタスクが実行されなかった場合、再試行されません。WP-Cron では、すべての予約タスクはキューに入れられ、次の機会 (つまり次のページロード) に実行されます。そのため、タスクが _いつ_ 実行されるかを100%確認できませんが、_いずれ_ 実行されることを100%確認できます。