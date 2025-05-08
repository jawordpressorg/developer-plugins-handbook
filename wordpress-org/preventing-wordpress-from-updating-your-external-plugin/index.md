<!--
# Preventing WordPress from Updating Your External Plugin
-->

# WordPress が外部プラグインを更新しないようにする

<!--
[warning]The information on this page is meant for use only on plugins **not** hosted on WordPress.org. Do not attempt to use this on your code hosted in the directory.[/warning]
-->

[warning]このページの情報は、WordPress.org でホスト **されていない** プラグインにのみ使用するためのものです。ディレクトリでホストされているコードに適用しないでください。[/warning]

<!--
If you host your plugin on WordPress.org, we handle all updates for you. As such, the steps in this document are **prohibited** in all plugins submitted to the directory. Any plugin hosted here that is found to include this plugin will be closed and the developer required to remove it in order for their plugin to be restored.
-->

WordPress.org でプラグインをホストしている場合、すべてのアップデートを WordPress が代行します。その為、この文書内の手順はディレクトリに提出されたすべてのプラグインで **禁止** されています。ここでホストされているプラグインで、この手順が含まれていることが判明すると、プラグインはクローズされ、開発者は自分のプラグインを復活させる為に、この手順を削除する必要があります。

<!--
We have chosen to document it here for the education of developers, as well as to ensure the global WordPress community can be safer.
-->

私たちは、開発者の教育のため、また世界の WordPress コミュニティがより安全であることを保証するために、ここにドキュメント化することにしました。

<!--
## Always Use Good Folder Names
-->

## 常に適切なフォルダー名を使用する

<!--
Before we get into the code, we must stress the absolute best way to ensure your plugin won’t get overwritten by an update from WordPress.org is to use a good name. If you’re making a plugin for your company, give it a folder name like `companyname-function-plugin` — for example, if you work for FaceRange and you’re making a status plugin, you could name it `facerange-status-plugin`
-->

コードに入る前に、WordPress.org からのアップデートによってプラグインが上書きされないようにする、絶対的な最善の方法は、良い名前を使うことだと断言しなければなりません。あなたの会社の為のプラグインを作るなら、`companyname-function-plugin` のようなフォルダー名をつけてください — たとえば、あなたが FaceRange に勤務していて、ステータスのプラグインを作っているのであれば、`facerange-status-plugin` という名前にできます。

<!--
Not only would we not accept it for using the prohibited term ‘plugin’, the plugin team would validate that the plugin owner **legally** represents FaceRange.
-->

使用禁止の単語「プラグイン」を使用しているため、私たちはそれを受け入れないだけでなく、プラグイン・チームは、プラグイン所有者が **法的に** FaceRange を代表していることを検証します。

<!--
## Update URI
-->

## Update URI

<!--
As of WordPress 5.8, we have added in a feature to how the WordPress.org API checks for updates, and allowed it to be blocked by the use of a new header: Update URI.
-->

WordPress 5.8から、WordPress.org の API がアップデートをチェックする方法に機能を追加し、新しいヘッダー「Update URI」を使用することでブロックできるようにしました。

<!--
Let’s say you have a plugin you made for your own site, and you gave it the folder name of `my-plugin`. That is a generic folder name, and has a high probability that someone else may use it. It’s also not a name we would allow you to block in our system, due to it’s generic nature.
-->

たとえば、自分のサイト用に作ったプラグインがあり、`my-plugin` というフォルダー名をつけたとしましょう。これは一般的なフォルダー名で、他の人が使う可能性が高い名前です。また、一般的な名前であるため、私たちのシステムでブロックできません。

<!--
The Update URI header can be added to the plugin headers. Look in your main plugin file for this section:
-->

Update URI ヘッダーはプラグインヘッダーに追加できます。メインのプラグインファイルで、このセクションを探してください:

```
/**
 * Plugin Name: My Cool Plugin
 * Plugin URI: https://example.com/my-plugin/
 * Description: My Plugin does cool things.
 * Version: 1.0
 * Author: the team
 * Author URI: https://example.com/
 * Text Domain: my-plugin
 * License: GPLv2
 * License URI: https://opensource.org/licenses/gpl-2.0.php
 */
```

<!--
To apply it, add a new header for **Update URI** and put a **non** WordPress.org URI in the value:
-->

これを適用するには、**Update URI** という新しいヘッダーを追加し、**非** WordPress.org の URI を値に入れます:

```
 * Update URI: https://example.com/my-updater/
```

<!--
You can also set it to `Update URI: false` if you want. As long as it does not include `worpress.org/plugins` or `w.org/plugins` it will be protected.
-->

また、必要なら `Update URI: false` に設定できます。`worpress.org/plugins` または `w.org/plugins` を含まない限り、保護されます。

<!--
## Filtering Updates
-->

## アップデートのフィルタリング

<!--
Another method, which is supported on older versions of WordPress, is to filter external API requests and discard any for your plugin.
-->

WordPress の古いバージョンでサポートされているもう一つの方法は、外部 API リクエストをフィルタリングし、あなたのプラグインへのリクエストをすべて破棄することです。

<!--
This code, which was written by [Mark Jaquith](https://markjaquith.wordpress.com/2009/12/14/excluding-your-plugin-or-theme-from-update-checks/), can be added to your own plugin:
-->

このコードは [Mark Jaquith](https://markjaquith.wordpress.com/2009/12/14/excluding-your-plugin-or-theme-from-update-checks/) によって書かれたもので、あなた自身のプラグインに追加できます:

```
function example_hidden_plugin_12345( $r, $url ) {
    if ( 0 !== strpos( $url, 'https://api.wordpress.org/plugins/update-check' ) )
        return $r; // Not a plugin update request. Bail immediately.

    $plugins = unserialize( $r['body']['plugins'] );
    unset( $plugins->plugins[ plugin_basename( __FILE__ ) ] );
    unset( $plugins->active[ array_search( plugin_basename( __FILE__ ), $plugins->active ) ] );
    $r['body']['plugins'] = serialize( $plugins );
    return $r;
}

add_filter( 'http_request_args', 'example_hidden_plugin_12345', 5, 2 );
```

<!--
What that does is check if the update request is from the WordPress.org api, and if it matches the plugin folder and file name of _this_ plugin. If it does, the plugin is removed from the list of plugins to check for updates.
-->

これは、WordPress.org api からのアップデートリクエストが、_この_ プラグインのプラグインフォルダーとファイル名に一致するか否かをチェックするものです。一致すれば、そのプラグインは、アップデートをチェックするプラグインのリストから削除されます。
