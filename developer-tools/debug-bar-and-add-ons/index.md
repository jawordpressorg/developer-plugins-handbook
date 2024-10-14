<!-- 
# Debug Bar and Add-Ons
 -->
# Debug Bar とアドオン

<!-- 
The Debug Bar is a plugin that adds a debug menu to the admin bar that shows query, cache, and other helpful debugging information.
 -->
Debug Bar は、管理バーにデバグメニューを追加するプラグインで、クエリー、キャッシュ、その他の役立つデバグ情報を表示します。

## Debug Bar

<!-- 
This is the main plugin, adding the base functionality that is extended by the remaining plugins listed on this page.
 -->
これはメインプラグインで、このページにリストされている残りのプラグインによって拡張される基本機能を追加します。

<!-- 
When `WP_DEBUG` is enabled it also tracks PHP Warnings and Notices to make them easier to find.
 -->
`WP_DEBUG` を有効にすると、PHP の警告や通知も追跡し、見つけやすくなります。

<!-- 
When `SAVEQUERIES` is enabled the mysql queries are tracked and displayed.
 -->
`SAVEQUERIES` を有効にすると、MySQL のクエリーが追跡され、表示されます。

<!-- 
[Visit Debug Bar](https://wordpress.org/plugins/debug-bar/)
 -->
[Debug Bar を見る](https://wordpress.org/plugins/debug-bar/)

## Debug Bar Console

<!-- 
This plugin adds a console in which you can run arbitrary PHP. This is excellent for testing the contents of variables, among many other uses.
 -->
このプラグインは、任意の PHP を実行できるコンソールを追加します。変数の内容をテストしたり、その他多くの用途に最適です。

<!-- 
[Visit Debug Bar Console](https://wordpress.org/plugins/debug-bar-console/)
 -->
[Debug Bar Console を見る](https://wordpress.org/plugins/debug-bar-console/)

## Debug Bar Shortcodes

<!-- 
This plugin adds a new panel to the Debug Bar that displays the registered shortcodes for the current request.
 -->
このプラグインは、Debug Bar に対して、現在のリクエストに登録されているショートコードを表示する、新しいパネルを追加します。

<!-- 
Additionally it will show you:
 -->
さらに、以下のような情報も表示されます:

<!-- 
- Which function/method is called by the shortcode.
- Whether the shortcode is used on the current post/page/post type and how (only when on singular).
- Any additional information available about the shortcode, such as a description, which parameters it takes, whether or not it is self-closing.
- Find out all pages/posts/etc on which a shortcode is used.
 -->
- ショートコードによって呼び出される関数/メソッド。
- ショートコードが現在の投稿/ページ/投稿タイプで使用されているかどうか、そしてどのように使用されているか (singular の場合のみ)。
- ショートコードに関する追加情報、たとえば説明、どのパラメータを取るか、自動で閉じるかどうか。
- ショートコードが使用されているすべてのページ/投稿/その他を調べる。

<!-- 
[Visit Debug Bar Shortcodes](https://wordpress.org/plugins/debug-bar-shortcodes/)
 -->
[Debug Bar Shortcodes を見る](https://wordpress.org/plugins/debug-bar-shortcodes/)

## Debug Bar Constants

<!-- 
This plugin adds three new panels to the Debug Bar that display the defined constants available to you as a developer for the current request:
 -->
このプラグインは、Debug Bar に対して、現在のリクエストに対して開発者として利用可能な定数を表示する、3つの新しいパネルを追加します:

<!-- 
- WP Constants
- WP Class Constants
- PHP Constants
 -->
- WP 定数
- WP クラス定数
- PHP 定数

<!-- 
[Visit Debug Bar Constants](https://wordpress.org/plugins/debug-bar-constants/)
 -->
[Debug Bar Constants を見る](https://wordpress.org/plugins/debug-bar-constants/)

## Debug Bar Post Types

<!-- 
This plugin adds a new panel to the Debug Bar that displays detailed information about the registered post types for your site.
 -->
このプラグインは、Debug Bar に対して、サイトに登録されている投稿タイプに関する詳細情報を表示する、新しいパネルを追加します。

<!-- 
[Visit Debug Bar Post Types](https://wordpress.org/plugins/debug-bar-post-types/)
 -->
[Debug Bar Post Types を見る](https://wordpress.org/plugins/debug-bar-post-types/)

## Debug Bar Cron

<!-- 
This plugin adds a new panel in the Debug Bar displaying information about WordPress' scheduled events.
 -->
このプラグインは、Debug Bar に対して、WordPress のスケジュールされたイベントに関する情報を表示する、新しいパネルを追加します。

<!-- 
Once installed, you will have access to the following information:
 -->
インストールすると、以下の情報にアクセスできます:

<!-- 
- Number of scheduled events.
- If cron is currently running.
- Time of next event.
- Current time.
- List of custom scheduled events.
- List of core scheduled events.
- List of schedules.
 -->
- スケジュールされたイベントの数
- cron が現在実行されている場合
- 次のイベントの時刻
- 現在の時刻
- カスタム・スケジュールイベントのリスト
- コア・スケジュールイベントのリスト
- スケジュールのリスト

<!-- 
[Visit Debug Bar Cron](https://wordpress.org/plugins/debug-bar-cron/)
 -->
[Debug Bar Cron を見る](https://wordpress.org/plugins/debug-bar-cron/)

## Debug Bar Actions and Filters Addon

<!-- 
This plugin adds two more tabs in the Debug Bar to display hooks (Actions and Filters) attached to the current request. Actions tab displays the actions hooked to current request. Filters tab displays the filter tags along with the functions attached to it with respective priority.
 -->
このプラグインは、Debug Bar に対して、現在のリクエストに接続されているフック (アクションとフィルター) を表示するために、2つのタブを追加します。アクションタブは、現在のリクエストにフックされたアクションを表示します。フィルタータブは、フィルタータグとそれに接続された関数を、それぞれの優先順位とともに表示します。

<!-- 
[Visit Debug Bar Actions and Filters Addon](https://wordpress.org/plugins/debug-bar-actions-and-filters-addon/)
 -->
[Debug Bar Actions and Filters Addon を見る](https://wordpress.org/plugins/debug-bar-actions-and-filters-addon/)

## Debug Bar Transients

<!-- 
This plugin adds information about WordPress transients to a new panel in the Debug Bar.
 -->
このプラグインは、Debug Bar に対して、WordPress の Transient に関する情報を表示する、新しいパネルを追加します。

<!-- 
Once installed, you will have access to the following information:
 -->
インストールすると、以下の情報にアクセスできます:

<!-- 
- Number of existing transients.
- List of custom transients.
- List of core transients.
- List of custom site transients.
- List of core site transients.
- An option to delete a transient.
 -->
- 既存 transient の数
- カスタム transient のリスト
- コア transient のリスト
- カスタム・サイト transient のリスト
- コア・サイト transient のリスト
- transient を削除するオプション

<!-- 
[Visit Debug Bar Transients](https://wordpress.org/plugins/debug-bar-transients/)
 -->
[Debug Bar Transients を見る](https://wordpress.org/plugins/debug-bar-transients/)

## Debug Bar List Script & Style Dependencies

<!-- 
This plugin lists scripts and styles that are loaded, in which order they're loaded, and what dependencies exist.
 -->
このプラグインは、読み込まれるスクリプトとスタイル、読み込まれる順番、依存関係を一覧表示します。

<!-- 
[Visit Debug Bar List Script & Style Dependencies](https://wordpress.org/plugins/debug-bar-list-dependencies/)
 -->
[Debug Bar List Script & Style Dependencies を見る](https://wordpress.org/plugins/debug-bar-list-dependencies/)

<!-- 
## Debug Bar Remote Requests
 -->
## Debug Bar Remote Requests

<!-- 
This plugin will add a new panel to Debug Bar that will display and profile remote requests made through the HTTP API.
 -->
このプラグインは、Debug Bar に対して、HTTP API 経由のリモートリクエストを表示しプロファイリングする、新しいパネルを追加します。

<!-- 
Once installed, you will have access to the following information:
 -->
インストールすると、以下の情報にアクセスできます:

<!-- 
- Request method (GET, POST, etc).
- URL.
- Time per request.
- Total time for all requests.
- Total number of requests.
 -->
- リクエスト・メソッド (GET、POST、等)
- URL
- リクエストごとの時間
- 全リクエストの総時間
- リクエスト総数

<!-- 
Optionally, you can add `?dbrr_full=1` to your URL to get additional information, including all request parameters and a full dump of the response with headers.
 -->
必要に応じて、URL に `?dbrr_full=1` を追加して、すべてのリクエストパラメータと、ヘッダーを含むレスポンスの完全なダンプを含む、追加情報を得ることができます。

<!-- 
[Visit Debug Bar Remote Requests](https://wordpress.org/plugins/debug-bar-remote-requests/)
 -->
[Debug Bar Remote Requests を見る](https://wordpress.org/plugins/debug-bar-remote-requests/)