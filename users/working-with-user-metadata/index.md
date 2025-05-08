<!--
# Working with User Metadata 
-->

# ユーザー・メタデータの操作

<!--
## Introduction
-->

## はじめに

<!--
WordPress' `users` table was designed to contain only the essential information about the user.
-->

WordPress の `users` テーブルは、ユーザーに関する重要な情報のみを格納するように設計されています。

<!--
[info]As of WP 4.7 the table contains: `ID`, `user_login`, `user_pass`, `user_nicename`, `user_email`, `user_url`, `user_registered`, `user_activation_key`, `user_status` and `display_name`.[/info]
-->

[info]WordPress 4.7では、テーブルには以下のものが含まれます: `ID`、`user_login`、`user_pass`、`user_nicename`、`user_email`、`user_url`、`user_registered`、`user_activation_key`、`user_status`、`display_name`。[/info]

<!--
Because of this, to store additional data, the `usermeta` table was introduced, which can store any arbitrary amount of data about a user.
-->

このため、ユーザーに関するあらゆる種類のデータを保存できる追加データを保存するために、`usermeta` テーブルが導入されました。

<!--
Both tables are tied together using one-to-many relationship based on the `ID` in the `users` table.
-->

両テーブルは `users` テーブルの `ID` をもとにした一対多のリレーションシップで結ばれています。

<!--
## Manipulating User Metadata
-->

## ユーザーメタデータの操作

<!--
There are two main ways for manipulating User Metadata.
-->

ユーザーメタデータを操作するには、主に2つの方法があります。

<!--
1. A form field in the user's profile screen.
2. Programmatically, via a function call.
-->

1. ユーザーのプロフィール画面のフォームフィールド。
2. プログラムによる、関数呼び出し。

<!--
### via a Form Field
-->

### フォームフィールド経由

<!--
The form field option is suitable for cases where the user will have access to the WordPress admin area, in which he will be able to view and edit profiles.
-->

フォームフィールドオプションは、ユーザーが WordPress の管理エリアにアクセスでき、そこでプロフィールを閲覧・編集できる場合に適しています。

<!--
Before we dive into an example, it's important to understand the hooks involved in the process and why they are there.
-->

例を取り上げる前に、そのプロセスに関わるフックとその理由を理解することが重要です。

<!--
#### `show_user_profile` hook
-->

#### `show_user_profile` フック

<!--
This action hook is fired whenever a user edits **it's own** user profile.
-->

このアクションフックは、ユーザーが**自分の**ユーザープロファイルを編集するたびに発生します。

<!--
**Remember,** a user that doesn't have the capability of editing his own profile won't fire this hook.
-->

自分のプロフィールを編集する権限を持っていないユーザーは、このフックを使うことができないということを、**覚えておいてください**。

<!--
#### `edit_user_profile` hook
-->

#### `edit_user_profile` フック

<!--
This action hook is fired whenever a user edits a user profile of **somebody else**.
-->

このアクションフックは、ユーザーが**誰か**のユーザープロファイルを編集するたびに発生します。

<!--
**Remember,** a user that doesn't have the capability for editing 3rd party profiles won't fire this hook.
-->

サードパーティのプロフィールを編集する権限を持っていないユーザーは、このフックを使うことができないということを、**覚えておいてください**。

<!--
#### Example Form Field
-->

#### フォーム・フィールドの例

<!--
In the example below we will be adding a birthday field to the all profile screens. Saving it to the database on profile updates.
-->

以下の例では、すべてのプロフィール画面に誕生日フィールドを追加します。プロフィールの更新時にそれをデータベースに保存します。

```
/**
 * The field on the editing screens.
 *
 * @param $user WP_User user object
 */
function wporg_usermeta_form_field_birthday( $user ) {
  ?>
  <h3>It's Your Birthday</h3>
  <table class="form-table">
    <tr>
      <th>
        <label for="birthday">Birthday</label>
      </th>
      <td>
        <input type="date"
          class="regular-text ltr"
          id="birthday"
          name="birthday"
          value="<?= esc_attr( get_user_meta( $user->ID, 'birthday', true ) ) ?>"
          title="Please use YYYY-MM-DD as the date format."
          pattern="(19[0-9][0-9]|20[0-9][0-9])-(1[0-2]|0[1-9])-(3[01]|[21][0-9]|0[1-9])"
          required>
        <p class="description">
          Please enter your birthday date.
        </p>
      </td>
    </tr>
  </table>
  <?php
}

/**
 * The save action.
 *
 * @param $user_id int the ID of the current user.
 *
 * @return bool Meta ID if the key didn't exist, true on successful update, false on failure.
 */
function wporg_usermeta_form_field_birthday_update( $user_id ) {
  // check that the current user have the capability to edit the $user_id
  if ( ! current_user_can( 'edit_user', $user_id ) ) {
    return false;
  }

  // create/update user meta for the $user_id
  return update_user_meta(
    $user_id,
    'birthday',
    $_POST['birthday']
  );
}

// Add the field to user's own profile editing screen.
add_action(
  'show_user_profile',
  'wporg_usermeta_form_field_birthday'
);

// Add the field to user profile editing screen.
add_action(
  'edit_user_profile',
  'wporg_usermeta_form_field_birthday'
);

// Add the save action to user's own profile editing screen update.
add_action(
  'personal_options_update',
  'wporg_usermeta_form_field_birthday_update'
);

// Add the save action to user profile editing screen update.
add_action(
  'edit_user_profile_update',
  'wporg_usermeta_form_field_birthday_update'
);
```

<!--
### Programmatically
-->

### プログラム的に

<!--
This option is suitable for cases where you're building a custom user area and/or plan to disable access to the WordPress admin area.
-->

このオプションは、カスタムユーザーエリアを構築している場合、および/または、WordPress 管理エリアへのアクセスを無効にする予定がある場合に適しています。

<!--
The functions available for manipulating User Metadata are: [`add_user_meta()`](https://developer.wordpress.org/reference/functions/add_user_meta/), [`update_user_meta()`](https://developer.wordpress.org/reference/functions/update_user_meta/), [`delete_user_meta()`](https://developer.wordpress.org/reference/functions/delete_user_meta/) and [`get_user_meta()`](https://developer.wordpress.org/reference/functions/get_user_meta/).
-->

ユーザーメタデータを操作するために利用できる関数は以下の通りです: [`add_user_meta()`](https://developer.wordpress.org/reference/functions/add_user_meta/)、[`update_user_meta()`](https://developer.wordpress.org/reference/functions/update_user_meta/)、[`delete_user_meta()`](https://developer.wordpress.org/reference/functions/delete_user_meta/)、[`get_user_meta()`](https://developer.wordpress.org/reference/functions/get_user_meta/)。

<!--
#### Add
-->

#### 追加

```
add_user_meta(
  int $user_id,
  string $meta_key,
  mixed $meta_value,
  bool $unique = false
);
```

<!--
Please refer to the Function Reference about [`add_user_meta()`](https://developer.wordpress.org/reference/functions/add_user_meta/) for full explanation about the used parameters.
-->

使用パラメータについての完全な説明は、[`add_user_meta()`](https://developer.wordpress.org/reference/functions/add_user_meta/) に関する関数リファレンスを参照してください。

<!--
#### Update
-->

#### 更新

```
update_user_meta(
  int $user_id,
  string $meta_key,
  mixed $meta_value,
  mixed $prev_value = ''
);
```

<!--
Please refer to the Function Reference about [`update_user_meta()`](https://developer.wordpress.org/reference/functions/update_user_meta/) for full explanation about the used parameters.
-->

使用パラメータについての完全な説明は、[`update_user_meta()`](https://developer.wordpress.org/reference/functions/update_user_meta/) に関する関数リファレンスを参照してください。

<!--
#### Delete
-->

#### 削除

```
delete_user_meta(
  int $user_id,
  string $meta_key,
  mixed $meta_value = ''
);
```

<!--
Please refer to the Function Reference about [`delete_user_meta()`](https://developer.wordpress.org/reference/functions/delete_user_meta/) for full explanation about the used parameters.
-->

使用パラメータについての完全な説明は、[`delete_user_meta()`](https://developer.wordpress.org/reference/functions/delete_user_meta/) に関する関数リファレンスを参照してください。

<!--
#### Get
-->

#### 取得

```
get_user_meta(
  int $user_id,
  string $key = '',
  bool $single = false
);
```

<!--
Please refer to the Function Reference about [`get_user_meta()`](https://developer.wordpress.org/reference/functions/get_user_meta/) for full explanation about the used parameters.
-->

使用パラメータについての完全な説明は、[`get_user_meta()`](https://developer.wordpress.org/reference/functions/get_user_meta/) に関する関数リファレンスを参照してください。

<!--
Please note, if you pass only the `$user_id`, the function will retrieve all Metadata as an associative array.
-->

`$user_id` のみを渡すと、この関数はすべてのメタデータを連想配列として取得することに注意してください。

<!--
You can render User Metadata anywhere in your plugin or theme.
-->

ユーザーメタデータは、プラグインやテーマのどこにでも表示できます。
