<!--
# Activation / Deactivation Hooks
-->

# 有効化フック / 無効化フック

<!--
Activation and deactivation hooks provide ways to perform actions when plugins are activated or deactivated.
-->

有効化フックと無効化フックは、プラグインが有効化または無効化された際にアクションを実行する方法を提供します。

<!--
- On _activation_, plugins can run a routine to add rewrite rules, add custom database tables, or set default option values.
- On _deactivation_, plugins can run a routine to remove temporary data such as cache and temp files and directories.
-->

- _有効化時_ に、プラグインは、書き換えルールを追加したり、カスタムデータベーステーブルを追加したり、デフォルトのオプション値を設定したりするルーチンを実行できます。
- _無効化時_ に、プラグインは。キャッシュや一時ファイルやディレクトリのような一時データを削除するルーチンを実行できます。

<!--
[alert]The deactivation hook is sometimes confused with the [uninstall hook](https://developer.wordpress.org/plugins/plugin-basics/uninstall-methods/). The uninstall hook is best suited to **delete all data permanently** such as deleting plugin options and custom tables, etc.[/alert]
-->

[alert]時々、無効化フックは、[アンインストール・フック](https://ja.wordpress.org/team/handbook/plugin-development/plugin-basics/uninstall-methods/) と混同されます。アンインストールフックは、プラグインオプションやカスタムテーブルなどを削除するような、**すべてのデータを永久に削除する**場合に最適です。[/alert]

<!--
## Activation
-->

## 有効化

<!--
To set up an activation hook, use the [register\_activation\_hook()](https://developer.wordpress.org/reference/functions/register_activation_hook/) function:
-->

有効化フックを設定するには、関数 [register\_activation\_hook()](https://developer.wordpress.org/reference/functions/register_activation_hook/) を使用します:

```
register_activation_hook(
  __FILE__,
  'pluginprefix_function_to_run'
);
```

<!--
## Deactivation
-->

## 無効化

<!--
To set up a deactivation hook, use the [register\_deactivation\_hook()](https://developer.wordpress.org/reference/functions/register_deactivation_hook/) function:
-->

無効化フックを設定するには、関数 [register\_deactivation\_hook()](https://developer.wordpress.org/reference/functions/register_deactivation_hook/) を使用します:

```
register_deactivation_hook(
  __FILE__,
  'pluginprefix_function_to_run'
);
```

<!--
The first parameter in each of these functions refers to your main plugin file, which is the file in which you have placed the [plugin header comment](https://developer.wordpress.org/plugins/plugin-basics/header-requirements/). Usually these two functions will be triggered from within the main plugin file; however, if the functions are placed in any other file, you must update the first parameter to correctly point to the main plugin file.
-->

これらの関数の最初のパラメータは、[プラグイン・ヘッダーコメント](https://ja.wordpress.org/team/handbook/plugin-development/plugin-basics/header-requirements/)を配置した、メイン・プラグイン・ファイルを参照します。通常、これら2つの関数はメイン・プラグイン・ファイルの中からトリガーされます。しかし、これらの関数が他のファイルに配置されている場合は、メイン・プラグイン・ファイルを正しく指すように、最初のパラメータを更新する必要があります。

<!--
## Example
-->

## 例

<!--
One of the most common uses for an activation hook is to refresh WordPress permalinks when a plugin registers a custom post type. This gets rid of the nasty 404 errors.
-->

有効化フックの最も一般的な使い方のひとつは、プラグインがカスタム投稿タイプを登録する際、WordPress のパーマリンクをリフレッシュすることです。これにより、やっかいな404エラーを取り除くことができます。

<!--
Let's look at an example of how to do this:
-->

では、その方法の例を見てみましょう:

```
/**
 * Register the "book" custom post type
 */
function pluginprefix_setup_post_type() {
  register_post_type( 'book', ['public' => true ] ); 
} 
add_action( 'init', 'pluginprefix_setup_post_type' );

/**
 * Activate the plugin.
 */
function pluginprefix_activate() { 
  // Trigger our function that registers the custom post type plugin.
  pluginprefix_setup_post_type(); 
  // Clear the permalinks after the post type has been registered.
  flush_rewrite_rules(); 
}
register_activation_hook( __FILE__, 'pluginprefix_activate' );
```

<!--
If you are unfamiliar with registering custom post types, don't worry – this will be covered later. This example is used simply because it's very common.
-->

カスタム投稿タイプの登録に慣れていない人、ご心配なく – 後で説明します。この例はごく一般的なものですので、簡単に紹介します。

<!--
Using the example from above, the following is how to reverse this process and deactivate a plugin:
-->

上記の例を使って、このプロセスを逆にして、プラグインを無効にする方法を以下に示します:

```
/**
 * Deactivation hook.
 */
function pluginprefix_deactivate() {
  // Unregister the post type, so the rules are no longer in memory.
  unregister_post_type( 'book' );
  // Clear the permalinks to remove our post type's rules from the database.
  flush_rewrite_rules();
}
register_deactivation_hook( __FILE__, 'pluginprefix_deactivate' );
```

<!--
For further information regarding activation and deactivation hooks, here are some excellent resources:
-->

有効化フックと無効化フックに関する詳しい情報については、ここにいくつかの優れたリソースがあります:

<!--
- [register\_activation\_hook()](https://developer.wordpress.org/reference/functions/register_activation_hook/) in the WordPress function reference.
- [register\_deactivation\_hook()](https://developer.wordpress.org/reference/functions/register_deactivation_hook/) in the WordPress function reference.
-->

- WordPress 関数リファレンスの [register\_activation\_hook()](https://developer.wordpress.org/reference/functions/register_activation_hook/)
- WordPress 関数リファレンスの [register\_deactivation\_hook()](https://developer.wordpress.org/reference/functions/register_deactivation_hook/)
