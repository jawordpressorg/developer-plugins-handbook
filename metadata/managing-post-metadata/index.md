<!--
# Managing Post Metadata
-->

# 投稿メタデータの管理

<!--
## Adding Metadata
-->

## メタデータの追加

<!--
Adding metadata can be done quite easily with [`add_post_meta()`](https://developer.wordpress.org/reference/functions/add_post_meta/). The function accepts a `post_id`, a `meta_key`, a `meta_value`, and a `unique` flag.
-->

メタデータの追加は、[`add_post_meta()`](https://developer.wordpress.org/reference/functions/add_post_meta/) で簡単に行うことができます。この関数は `post_id`、`meta_key`、`meta_value`、そして `unique` フラグを受け付けます。

<!--
The `meta_key` is how your plugin will reference the meta value elsewhere in your code. Something like `mycrazymetakeyname` would work, however a prefix related to your plugin or theme followed by a description of the key would be more useful. `wporg_featured_menu` might be a good one. It should be noted that the same `meta_key` may be used multiple times to store variations of the metadata (see the unique flag below).
-->

`meta_key` は、プラグインがコードの他の場所でメタ値を参照する方法です。`mycrazymetakeyname` のようなものでも良いですが、プラグインやテーマに関連する接頭辞の後にキーの説明をつけると、より便利です。`wporg_featured_menu` などが良いかもしれません。メタデータのバリエーションを保存するために、同じ `meta_key` を複数回使用できることに注意してください (下記のユニークフラグを参照)。

<!--
The `meta_value` can be a string, integer, or an array. If it's an array, it will be automatically serialized before being stored in the database.
-->

`meta_value` には、文字列、整数、配列を指定できます。配列の場合は、データベースに格納する前に自動的にシリアライズされます。

<!--
The `unique` flag allows you to declare whether this key should be unique. A **non** unique key is something a post can have multiple variations of, like price.
-->

`unique` フラグにより、このキーがユニーク (一意) であるか否かを宣言できます。「非」ユニークキーとは、価格のように、投稿が複数のバリエーションを持つことができるキーのことです。

<!--
If you only ever want **one** price for a post, you should flag it `unique` and the `meta_key` will have one value only.
-->

投稿には価格を **1つ** だけ持たせたい場合は、`unique` フラグを立て、`meta_key` の値は1つだけ保持できるようにします。

<!--
## Updating Metadata
-->

## メタデータの更新

<!--
If a key already exists and you want to update it, use [`update_post_meta()`](https://developer.wordpress.org/reference/functions/update_post_meta/). If you use this function and the key does **NOT** exist, then it will create it, as if you'd used [`add_post_meta()`](https://developer.wordpress.org/reference/functions/add_post_meta/).
-->

キーがすでに存在していて、それを更新したい場合は、[`update_post_meta()`](https://developer.wordpress.org/reference/functions/update_post_meta/) を使用します。この関数を使用し、キーが存在 **しない** 場合は、[`add_post_meta()`](https://developer.wordpress.org/reference/functions/add_post_meta/) を使用した際と同じように、キーが作成されます。

<!--
Similar to [`add_post_meta()`](https://developer.wordpress.org/reference/functions/add_post_meta/), the function accepts a `post_id`, a `meta_key`, and `meta_value`. It also accepts an optional `prev_value` – which, if specified, will cause the function to only update existing metadata entries with this value. If it isn't provided, the function defaults to updating all entries.
-->

[`add_post_meta()`](https://developer.wordpress.org/reference/functions/add_post_meta/) と同様に、この関数は `post_id`、`meta_key`、`meta_value` を受け付けます。また、オプションで `prev_value` を指定でき、この値が指定された場合、この関数は、既存のメタデータ・エントリのみを、この値で更新します。この値が指定されない場合、関数はデフォルトですべてのエントリを更新します。

<!--
## Deleting Metadata
-->

## メタデータの削除

<!--
[`delete_post_meta()`](https://developer.wordpress.org/reference/functions/delete_post_meta/) takes a `post_id`, a `meta_key`, and optionally `meta_value`. It does exactly what the name suggests.
-->

[`delete_post_meta()`](https://developer.wordpress.org/reference/functions/delete_post_meta/) は、`post_id`、`meta_key`、そしてオプションで `meta_value` を受け取ります。これは、名前が示すとおりのことを行います。

<!--
## Character Escaping
-->

## 文字エスケープ

<!--
Post meta values are passed through the [`stripslashes()`](https://www.php.net/manual/en/function.stripslashes.php) function upon being stored, so you will need to be careful when passing in values (such as JSON) that might include escaped characters.
-->

投稿メタの値は、保存時に [`stripslashes()`](https://www.php.net/manual/en/function.stripslashes.php) 関数を通して渡されるため、エスケープされた文字を含む可能性のある値 (JSON など) を渡す際には注意が必要です。

<!--
Consider the JSON value `{"key":"value with \"escaped quotes\""}`:
-->

`{"key":"value with \"escaped quotes\""}` という JSON 値を考えてみましょう:

```
$escaped_json = '{"key":"value with \"escaped quotes\""}';
update_post_meta( $id, 'escaped_json', $escaped_json );
$broken = get_post_meta( $id, 'escaped_json', true );
/*
$broken, after stripslashes(), ends up unparsable:
{"key":"value with "escaped quotes""}
*/
```

<!--
### Workaround
-->

### 回避方法

<!--
By adding one more level of escaping using the function [`wp_slash()`](https://developer.wordpress.org/reference/functions/wp_slash/) (introduced in WP 3.6), you can compensate for the call to [`stripslashes()`](https://www.php.net/manual/en/function.stripslashes.php):
-->

(WordPress 3.6で導入された) 関数 [`wp_slash()`](https://developer.wordpress.org/reference/functions/wp_slash/) を使って、もう1段階エスケープを追加することで、[`stripslashes()`](https://www.php.net/manual/en/function.stripslashes.php) の呼び出しを補うことができます:

```
$escaped_json = '{"key":"value with \"escaped quotes\""}';
update_post_meta( $id, 'double_escaped_json', wp_slash( $escaped_json ) );
$fixed = get_post_meta( $id, 'double_escaped_json', true );
/*
$fixed, after stripslashes(), ends up as desired:
{"key":"value with \"escaped quotes\""}
*/
```

<!--
## Hidden Custom Fields
-->

## 非表示のカスタムフィールド

<!--
If you are a plugin or theme developer and you are planning to use custom fields to store parameters, it is important to note that WordPress will not show custom fields which have `meta_key` starting with an "_" (underscore) in the custom fields list on the post edit screen or when using the [`get_post_meta()`](https://developer.wordpress.org/reference/functions/get_post_meta/) template function.
-->

プラグインやテーマの開発者で、カスタムフィールドを使ってパラメータを格納しようと考えている場合、WordPress では、投稿編集画面や [`get_post_meta()`](https://developer.wordpress.org/reference/functions/get_post_meta/) テンプレート関数のカスタムフィールド一覧で、`meta_key` が「_」(アンダースコア) で始まるカスタムフィールドは表示されないことに注意してください。

<!--
This can be useful in order to show these custom fields in an unusual way by using the [`add_meta_box()`](https://developer.wordpress.org/reference/functions/add_meta_box/) function.
-->

これは、[`add_meta_box()`](https://developer.wordpress.org/reference/functions/add_meta_box/) 関数を使用して、これらのカスタムフィールドを通常とは異なる方法で表示するのに便利です。

<!--
The example below will add a unique custom field with the `meta_key` name '_color' and the `meta_value` of 'red' but this custom field will not display in the post edit screen:
-->

以下の例では、`meta_key` の名前が '_color'、`meta_value` が 'red' のユニークなカスタムフィールドが追加されますが、このカスタムフィールドは投稿編集画面には表示されません:

```
add_post_meta( 68, '_color', 'red', true );
```

<!--
### Hidden Arrays
-->

### 非表示の配列

<!--
In addition, if the `meta_value` is an array, it will not be displayed on the page edit screen, even if you don't prefix the `meta_key` name with an underscore.
-->

また、`meta_value` が配列の場合、`meta_key` の名前の前にアンダースコアを付けなかったとしても、ページ編集画面には表示されません。
