<!--
# Options API
-->

# オプション API

<!--
The Options API, added in WordPress 1.0, allows creating, reading, updating and deleting of WordPress options. In combination with the [Settings API](https://developer.wordpress.org/plugins/settings/settings-api/) it allows controlling of options defined in settings pages.
-->

WordPress 1.0で追加されたオプション API は、WordPress のオプションの作成、読み込み、更新、削除を可能にします。[設定 API](https://ja.wordpress.org/team/handbook/plugin-development/settings/settings-api/) と組み合わせることで、設定ページで定義されたオプションの制御が可能になります。

<!--
## Where Options are Stored?
-->

## オプションはどこに格納されますか ?

<!--
Options are stored in the `{$wpdb->prefix}_options` table. `$wpdb->prefix` is defined by the `$table_prefix` variable set in the `wp-config.php` file.
-->

オプションは、テーブル `{$wpdb->prefix}_options` に格納されます。`$wpdb->prefix` は、ファイル `wp-config.php` で設定された変数 `$table_prefix` によって定義されます。

<!--
## How Options are Stored?
-->

## オプションはどのように格納されますか ?

<!--
Options may be stored in the WordPress database in one of two ways: as a single value or as an array of values.
-->

オプションは、単一の値または値の配列として、WordPress のデータベースに2つの方法で格納されます。

<!--
### Single Value
-->

### 単一の値

<!--
When saved as a single value, the option name refers to a single value.
-->

単一の値として保存された場合、オプション名は単一の値を参照します。

```
// add a new option
add_option('wporg_custom_option', 'hello world!');
// get an option
$option = get_option('wporg_custom_option');
```

<!--
### Array of Values
-->

### 値の配列

<!--
When saved as an array of values, the option name refers to an array, which itself may be comprised key/value pairs.
-->

値の配列として保存される場合、オプション名は配列を参照し、それ自体が KVP (キーと値のペア) で構成されることもあります。

```
// array of options
$data_r = array('title' => 'hello world!', 1, false );
// add a new option
add_option('wporg_custom_option', $data_r);
// get an option
$options_r = get_option('wporg_custom_option');
// output the title
echo esc_html($options_r['title']);
```

<!--
If you are working with a large number of related options, storing them as an array can have a positive impact on overall performance.
-->

関連するオプションを大量に扱う場合、それらを配列として格納することは、全体的なパフォーマンスに良い影響を与える可能性があります。

<!--
[info]Accessing data as individual options may result in many individual database transactions, and as a rule, database transactions are expensive operations (in terms of time and server resources). When you store or retrieve an array of options, it happens in a single transaction, which is ideal.[/info]
-->

[info]個別のオプションとしてデータにアクセスすると、多くの個別のデータベース・トランザクションが発生する可能性があります。一般にデータベース・トランザクションは (時間とサーバー・リソースの点で) 高コストな操作です。オプションを配列で格納したり取得したりすると、単一のトランザクションで行われるため、理想的です。[/info]

<!--
## Function Reference
-->

## 関数リファレンス

<!--
### Add Option
-->

### オプションの追加

<!--
- [`add_option()`](https://developer.wordpress.org/reference/functions/add_option/)
- [`add_site_option()`](https://developer.wordpress.org/reference/functions/add_site_option/)
-->

- [`add_option()`](https://developer.wordpress.org/reference/functions/add_option/)
- [`add_site_option()`](https://developer.wordpress.org/reference/functions/add_site_option/)

<!--
### Get Option
-->

### オプションの取得

<!--
- [`get_option()`](https://developer.wordpress.org/reference/functions/get_option/)
- [`get_site_option()`](https://developer.wordpress.org/reference/functions/get_site_option/)
-->

- [`get_option()`](https://developer.wordpress.org/reference/functions/get_option/)
- [`get_site_option()`](https://developer.wordpress.org/reference/functions/get_site_option/)

<!--
### Update Option
-->

### オプションの更新

<!--
- [`update_option()`](https://developer.wordpress.org/reference/functions/update_option/)
- [`update_site_option()`](https://developer.wordpress.org/reference/functions/update_site_option/)
-->

- [`update_option()`](https://developer.wordpress.org/reference/functions/update_option/)
- [`update_site_option()`](https://developer.wordpress.org/reference/functions/update_site_option/)

<!--
### Delete Option
-->

### オプションの削除

<!--
- [`delete_option()`](https://developer.wordpress.org/reference/functions/delete_option/)
- [`delete_site_option()`](https://developer.wordpress.org/reference/functions/delete_site_option/)
-->

- [`delete_option()`](https://developer.wordpress.org/reference/functions/delete_option/)
- [`delete_site_option()`](https://developer.wordpress.org/reference/functions/delete_site_option/)
