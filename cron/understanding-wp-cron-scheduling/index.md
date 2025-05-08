<!--
# Understanding WP-Cron Scheduling
-->

# WP-Cron スケジューリングの理解

<!--
Unlike a traditional system cron that schedules tasks for specific times (e.g. "every hour at 5 minutes past the hour"), WP-Cron uses intervals to simulate a system cron.
-->

特定の時間 (たとえば、「毎時5分過ぎ」) にタスクを予定する伝統的なシステム cron とは異なり、WP-Cron は、システム cron を模倣するために、間隔 (インターバル) を使用します。

<!--
WP-Cron is given two arguments: the time for the first task, and an interval (in seconds) after which the task should be repeated. For example, if you schedule a task to begin at 2:00PM with an interval of 300 seconds (five minutes), the task would first run at 2:00PM and then again at 2:05PM, then again at 2:10PM, and so on, every five minutes.
-->

WP-Cron には2つの引数が与えられます: 最初のタスクの時間と、タスクが繰り返されるインターバル (秒) です。たとえば、午後02時00分に開始するタスクを300秒 (5分) のインターバルで予定した場合、タスクはまず午後02時00分に実行され、午後02時05分に再び実行され、午後02時10分に再び実行され、といった具合に5分ごとに実行されます。

<!--
To simplify scheduling tasks, WordPress provides some default intervals and an easy method for adding custom intervals.
-->

WordPress では、スケジューリング作業を簡素化するために、いくつかのデフォルト・インターバルと、カスタム・インターバルを追加する、簡単な方法を提供しています。

<!--
The default intervals provided by WordPress are:
-->

WordPress が提供するデフォルト・インターバルは、次のようになっています:

<!--
- hourly
- twicedaily
- daily
- weekly (since WP 5.4)
-->

- `hourly` (毎時)
- `twicedaily` (1日2回)
- `daily` (毎日)
- `weekly` (毎週。WordPress 5.4以降)

<!--
## Custom Intervals
-->

## カスタム・インターバル

<!--
To add a custom interval, you can create a filter, such as:
-->

カスタム・インターバルを追加するには、次のようなフィルターを作成します:

```
add_filter( 'cron_schedules', 'example_add_cron_interval' );
function example_add_cron_interval( $schedules ) { 
  $schedules['five_seconds'] = array(
    'interval' => 5,
    'display'  => esc_html__( 'Every Five Seconds' ),
  );
  return $schedules;
}
```

<!--
This filter function creates a new interval that will allow us to run a cron task every five seconds.
-->

このフィルター関数は、5秒ごとに cron タスクを実行するための、新しいインターバルを作成します。

<!--
[info]All intervals are in seconds.[/info]
-->

[info]インターバルはすべて秒単位。[/info]
