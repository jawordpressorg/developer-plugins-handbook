<!-- 
# Testing of WP-Cron
 -->
# WP-Cron のテスト

## WP-CLI

<!-- 
Cron jobs can be tested using [WP-CLI](https://wp-cli.org/). It offers commands like `wp cron event list` and `wp cron event run {job name}`. [Check the documentation](https://developer.wordpress.org/cli/commands/cron/) for more details.
 -->
Cron ジョブは [WP-CLI](https://wp-cli.org/) を使ってテストできます。`wp cron event list` や `wp cron event run {job name}` のようなコマンドが提供されています。詳しくは、[ドキュメントを参照](https://developer.wordpress.org/cli/commands/cron/)してください。

<!-- 
## WP-Cron Management Plugins
 -->
## WP-Cron 管理プラグイン

<!-- 
Several [plugins are available on the WordPress.org Plugin Directory](https://wordpress.org/plugins/tags/cron/) for viewing, editing, and controlling the scheduled cron events and available schedules on your site.
 -->
あなたのサイトの予定 cron イベントと可能な予定を表示、編集、制御するためのプラグインがあり、[WordPress.org プラグイン・ディレクトリで入手可能です](https://wordpress.org/plugins/tags/cron/)。

## `_get_cron_array()`

<!-- 
The [`_get_cron_array()`](https://developer.wordpress.org/reference/functions/_get_cron_array/) function returns an array of all currently scheduled cron events. Use this function if you need to inspect the raw list of events.
 -->
関数 [`_get_cron_array()`](https://developer.wordpress.org/reference/functions/_get_cron_array/) は、すべての予定 cron イベントの配列を返します。イベントの生のリストを確認する必要がある場合は、この関数を使用してください。

## `wp_get_schedules()`

<!-- 
The [`wp_get_schedules()`](https://developer.wordpress.org/reference/functions/wp_get_schedules/) function returns an array of available event recurrence schedules. Use this function if you need to inspect the raw list of available schedules.
 -->
The [`wp_get_schedules()`](https://developer.wordpress.org/reference/functions/wp_get_schedules/) は、利用可能な繰り返し予定イベントの配列を返します。利用可能な予定の生のリストを確認する必要がある場合は、この関数を使用してください。