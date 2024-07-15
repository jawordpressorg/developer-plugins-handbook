<!-- 
# Uninstall Methods
 -->
# アンインストールの方法

<!-- 
Your plugin may need to do some clean-up when it is uninstalled from a site.
 -->
プラグインがサイトからアンインストールされると、プラグインのクリーンアップが必要になることがあります。

<!-- 
A plugin is considered uninstalled if a user has deactivated the plugin, and then clicks the delete link within the WordPress Admin.
 -->
ユーザーがプラグインを無効化した後、WordPress 管理画面内で削除リンクをクリックすると、プラグインはアンインストールされたとみなされます。

<!-- 
When your plugin is uninstalled, you'll want to clear out any plugin options and/or settings specific to the plugin, and/or other database entities such as tables.
 -->
プラグインがアンインストールされたら、プラグインオプションやプラグイン固有の設定、テーブルなどのデータベースエンティティを消去してください。

<!-- 
Less experienced developers sometimes make the mistake of using the deactivation hook for this purpose.
 -->
経験の浅い開発者は、この目的で非アクティブ化フックを使うという間違いを犯すことがあります。

<!-- 
This table illustrates the differences between deactivation and uninstall.
 -->
この表は、非アクティブ化とアンインストールの違いを示しています。

<!-- 
| Scenario | Deactivation Hook | Uninstall Hook |
| --- | --- | --- |
| Flush Cache/Temp | Yes | No |
| Flush Permalinks | Yes | No |
| Remove Options from {[$wpdb](https://developer.wordpress.org/reference/classes/wpdb/)→prefix}_options | No | Yes |
| Remove Tables from [$wpdb](https://developer.wordpress.org/reference/classes/wpdb/) | No | Yes |
 -->
| シナリオ | 非アクティブ化フック | アンインストール フック |
| --- | --- | --- |
| キャッシュ / Temp を消去する | Yes | No |
| パーマリンクを消去する | Yes | No |
| {[$wpdb](https://developer.wordpress.org/reference/classes/wpdb/)→prefix}_options からオプションを削除する | No | Yes |
| [$wpdb](https://developer.wordpress.org/reference/classes/wpdb/) からテーブルを削除する | No | Yes |

<!-- 
## Method 1: register_uninstall_hook
 -->
## 方法1: register_uninstall_hook

<!-- 
To set up an uninstall hook, use the [register\_uninstall\_hook()](https://developer.wordpress.org/reference/functions/register_uninstall_hook/) function:
 -->
アンインストールフックを設定するには、関数 [register\_uninstall\_hook()](https://developer.wordpress.org/reference/functions/register_uninstall_hook/) を使用します:

```
register_uninstall_hook(
  __FILE__,
  'pluginprefix_function_to_run'
);
```

<!-- 
## Method 2: uninstall.php
 -->
## 方法2: uninstall.php

<!-- 
To use this method you need to create an `uninstall.php` file inside the root folder of your plugin. This magic file is run automatically when the users deletes the plugin.
 -->
この方法を使用するには、プラグインのルートフォルダー内にファイル `uninstall.php` を作成する必要があります。このマジックファイルは、ユーザーがプラグインを削除したときに自動的に実行されます。

<!-- 
For example: `/plugin-name/uninstall.php`
 -->
例: `/plugin-name/uninstall.php`

<!-- 
[alert]Always check for the constant `WP_UNINSTALL_PLUGIN` in `uninstall.php` before doing anything. This protects against direct access.
 -->
[alert]何かをする前に、`uninstall.php` で常に定数 `WP_UNINSTALL_PLUGIN` をチェックします。これは直接アクセスを防ぐためです。

<!-- 
The constant will be defined by WordPress during the `uninstall.php` invocation.
 -->
この定数は WordPress が `uninstall.php` を起動する際に定義されます。

<!-- 
The constant is **NOT** defined when uninstall is performed by [register\_uninstall\_hook()](https://developer.wordpress.org/reference/functions/register_uninstall_hook/).[/alert]
 -->
[register\_uninstall\_hook()](https://developer.wordpress.org/reference/functions/register_uninstall_hook/) でアンインストールする場合、定数は定義**されません**。[/alert]

<!-- 
Here is an example deleting option entries and dropping a database table:
 -->
以下は、オプション・エントリーを削除し、データベース・テーブルを取り除く例です:

```
// if uninstall.php is not called by WordPress, die
if ( ! defined( 'WP_UNINSTALL_PLUGIN' ) ) {
  die;
}

$option_name = 'wporg_option';

delete_option( $option_name );

// for site options in Multisite
delete_site_option( $option_name );

// drop a custom database table
global $wpdb;
$wpdb->query( "DROP TABLE IF EXISTS {$wpdb->prefix}mytable" );
```

<!-- 
[info]In Multisite, looping through all blogs to delete options can be very resource intensive.[/info]
 -->
[info]マルチサイトでは、オプションを削除するためにすべてのブログをループすることは非常にリソースを消費します。[/info]
