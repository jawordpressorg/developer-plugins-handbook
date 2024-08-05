<!-- 
# Scheduling WP Cron Events
 -->
# WP Cron イベントのスケジューリング

<!-- 
The WP Cron system uses hooks to add new scheduled tasks.
 -->
WP Cron システムは、新しい予定タスクを追加するためにフックを使用します。

<!-- 
## Adding the Hook
 -->
## フックの追加

<!-- 
In order to get your task to run you must create your own custom hook and give that hook the name of a function to execute. This is a very important step. Forget it and your task will never run.
 -->
タスクを実行させるには、独自のカスタム・フックを作り、そのフックに実行する関数名を付ける必要があります。これはとても重要なステップです。これを忘れると、タスクは実行されません。

<!-- 
The following example will create a hook. The first parameter is the name of the hook you are creating, and the second is the name of the function to call.
 -->
次の例ではフックを作成します。最初のパラメータは作成するフックの名前で、2番目は呼び出す関数の名前です。

```
add_action( 'bl_cron_hook', 'bl_cron_exec' );
```

<!-- 
[info]Remember, the `bl_` part of the function name is a _function prefix_. You can learn why prefixes are important [here](https://developer.wordpress.org/plugins/plugin-basics/best-practices/#prefix-everything).[/info]
 -->
[info]関数名の `bl_` の部分は _関数の接頭辞_ であることを忘れないでください。なぜ接頭辞が重要なのかは、[こちら](https://developer.wordpress.org/plugins/plugin-basics/best-practices/#prefix-everything)を参照してください。[/info]

<!-- 
[info]You can read more about actions [here](https://developer.wordpress.org/plugins/hooks/actions/).[/info]
 -->
[info]アクションについての詳細は、[こちら](https://developer.wordpress.org/plugins/hooks/actions/)をご覧ください。[/info]

<!-- 
## Scheduling the Task
 -->
## タスクのスケジューリング

<!-- 
An important note is that WP-Cron is a simple task scheduler. As we know, tasks are added by the hook created to call the function that runs the desired task. However if you call `wp_schedule_event()` multiple times, even with the same hook name, the event will be scheduled multiple times. If your code adds the task on each page load this could result in the task being scheduled several thousand times. This is not what you want.
 -->
重要なことは、WP-Cron は単純なタスク・スケジューラーであるということです。ご存じのように、タスクは、目的のタスクを実行する関数を呼び出すために作成されたフックによって追加されます。しかし、同じフック名であっても `wp_schedule_event()` を複数回呼び出すと、イベントは複数回予定されます。あなたのコードが各ページのロード時にタスクを追加する場合、タスクは数千回予定されることになります。これはあなたが望むことではないでしょう。

<!-- 
WordPress provides a convenient function called [`wp_next_scheduled()`](https://developer.wordpress.org/reference/functions/wp_next_scheduled/) to check if a particular hook is already scheduled. `wp_next_scheduled()` takes one parameter, the hook name. It will return either a string containing the timestamp of the next execution or false, signifying the task is not scheduled. It is used like so:
 -->
WordPress は、特定のフックがすでに予定されているかどうかをチェックするために、[`wp_next_scheduled()`](https://developer.wordpress.org/reference/functions/wp_next_scheduled/) という便利な関数を提供しています。`wp_next_scheduled()` は、1つのパラメータとして、フック名を受け取ります。次の実行のタイムスタンプを含む文字列か、タスクが予定されていないことを示す false を返します。次のように使います:

```
wp_next_scheduled( 'bl_cron_hook' );
```

<!-- 
Scheduling a recurring task is accomplished with [`wp_schedule_event()`](https://developer.wordpress.org/reference/functions/wp_schedule_event/). This function takes three required parameters, and one additional parameter that is an array that can be passed to the function executing the wp-cron task. We will focus on the first three parameters. The parameters are as follows:
 -->
定期的なタスクのスケジューリングは [`wp_schedule_event()`](https://developer.wordpress.org/reference/functions/wp_schedule_event/) で行います。この関数は、必須パラメータ3つと、追加パラメータとして、wp-cron タスクを実行する関数に渡す配列を受け取ります。ここでは最初の3つのパラメータに焦点を当てます。パラメータは以下の通りです:

<!-- 
1. `$timestamp` – The UNIX timestamp of the first time this task should execute.
2. `$recurrence` – The name of the interval in which the task will recur in seconds.
3. `$hook` – The name of our custom hook to call.
 -->
1. `$timestamp` – このタスクが最初に実行される UNIX タイムスタンプ。
2. `$recurrence` – タスクが繰り返し実行されるインターバルの名前 (秒単位)。
3. `$hook` – 呼び出すカスタムフックの名前。

<!-- 
We will use the 5 second interval we created [here](https://developer.wordpress.org/plugins/cron/understanding-wp-cron-scheduling/) and the hook we created above, like so:
 -->
[ここ](https://developer.wordpress.org/plugins/cron/understanding-wp-cron-scheduling/)で作成した5秒のインターバルと、上で作成したフックを次のように使います:

```
wp_schedule_event( time(), 'five_seconds', 'bl_cron_hook' );
```

<!-- 
Remember, we need to first ensure the task is not already scheduled. So we wrap the scheduling code in a check like this:
 -->
まず、タスクがすでに予定されていないことを確認する必要があります。そこで、スケジューリングコードを次のようにチェックで囲みます:

```
if ( ! wp_next_scheduled( 'bl_cron_hook' ) ) {
  wp_schedule_event( time(), 'five_seconds', 'bl_cron_hook' );
}
```

<!-- 
## Unscheduling tasks
 -->
## タスクのスケジューリング解除

<!-- 
When you no longer need a task scheduled you can unschedule tasks with [`wp_unschedule_event()`](https://developer.wordpress.org/reference/functions/wp_unschedule_event/). This function takes the following two parameters:
 -->
予定されているタスクが不要になったら、[`wp_unschedule_event()`](https://developer.wordpress.org/reference/functions/wp_unschedule_event/) でタスクをアンスケジュールできます。この関数は以下の2つのパラメータを受け取ります:

<!-- 
1. `$timestamp` – Timestamp of the next occurrence of the task.
2. `$hook` – Name of the custom hook to be called.
 -->
1. `$timestamp` – タスクの次の実行のタイムスタンプ。
2. `$hook` – 呼び出されるカスタムフックの名前。

<!-- 
This function will not only unschedule the task indicated by the timestamp, it will also unschedule all future occurrences of the task. Since you probably will not know the timestamp for the next task, there is another handy function, [`wp_next_scheduled()`](https://developer.wordpress.org/reference/functions/wp_next_scheduled/) that will find it for you. `wp_next_scheduled()` takes one parameter (that we care about):
 -->
この関数は、タイムスタンプで示されたタスクのスケジュールを解除するだけでなく、将来発生するすべてのタスクのスケジュールを解除します。おそらく「次のタスクのタイムスタンプ」を知らないでしょうから、それを探してくれるもう一つの便利な関数 [`wp_next_scheduled()`](https://developer.wordpress.org/reference/functions/wp_next_scheduled/) があります。`wp_next_scheduled()` は1つのパラメータを取ります (気になるそれは):

<!-- 
1. `$hook` – The name of the hook that is called to execute the task.
 -->
1. `$hook` – タスクを実行するために呼ばれるフックの名前。

<!-- 
Put it all together and the code looks like:
 -->
これをすべてまとめると、コードは次のようになります:

```
$timestamp = wp_next_scheduled( 'bl_cron_hook' );
wp_unschedule_event( $timestamp, 'bl_cron_hook' );
```

<!-- 
It is very important to unschedule tasks when you no longer need them because WordPress will continue to attempt to execute the tasks, even though they are no longer in use (or even after your plugin has been deactivated or removed). An important place to remember to unschedule your tasks is upon plugin deactivation.
 -->
不要になったタスクのスケジュールを解除することは非常に重要です。WordPress はタスクが使われなくなっても (またはプラグインが無効化または削除された後でも)、実行しようとし続けるからです。タスクのスケジュールを解除するために覚えておくべき重要な場所は、プラグインの無効化時です。

<!-- 
Unfortunately there are many plugins in the WordPress.org Plugin Directory that do not clean up after themselves. If you find one of these plugins please let the author know to update their code. WordPress provides a function called [`register_deactivation_hook()`](https://developer.wordpress.org/reference/functions/register_deactivation_hook/) that allows developers to run a function when their plugin is deactivated. It is very simple to setup and looks like:
 -->
残念ながら、WordPress.org のプラグイン・ディレクトリには、後始末をしないプラグインがたくさんあります。そのようなプラグインを見つけたら、コードを更新するよう作者に知らせてください。WordPress は [`register_deactivation_hook()`](https://developer.wordpress.org/reference/functions/register_deactivation_hook/) という関数を提供しており、プラグインが無効化されたときに関数を実行できます。設定はとても簡単で、次のようになります:

```
register_deactivation_hook( __FILE__, 'bl_deactivate' ); 

function bl_deactivate() {
  $timestamp = wp_next_scheduled( 'bl_cron_hook' );
  wp_unschedule_event( $timestamp, 'bl_cron_hook' );
}
```

<!-- 
[info]You can read more about activation and deactivation hooks [here](https://developer.wordpress.org/plugins/plugin-basics/activation-deactivation-hooks/).[/info]
 -->
[info]有効化フックと無効化フックについては、[こちら](https://developer.wordpress.org/plugins/plugin-basics/activation-deactivation-hooks/)をご覧ください。[/info]