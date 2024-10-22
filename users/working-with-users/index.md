<!-- 
# Working with Users
 -->
# ユーザーの操作

<!-- 
## Adding Users
 -->
## ユーザーの追加

<!-- 
To add a user you can use `wp_create_user()` or `wp_insert_user()`.
 -->
ユーザーを追加するには、`wp_create_user()` か `wp_insert_user()` を使います。

<!-- 
`wp_create_user()` creates a user using only the username, password and email parameters while `wp_insert_user()` accepts an array or object describing the user and its properties.
 -->
`wp_create_user()` はユーザー名、パスワード、メールアドレスのパラメータのみを使用してユーザーを作成します。一方、`wp_insert_user()` はユーザーとそのプロパティを記述する配列またはオブジェクトを受け取ってユーザーを作成します。

<!-- 
### Create User
 -->
### ユーザーの作成

<!-- 
`wp_create_user()` allows you to create a new WordPress user.
 -->
`wp_create_user()` を使用して新しい WordPress ユーザーを作成できます。

<!-- 
[info]It uses [`wp_slash()`](https://developer.wordpress.org/reference/functions/wp_slash/) to escape the values. The PHP compact() function to create an array with these values. The [`wp_insert_user()`](https://developer.wordpress.org/reference/functions/wp_insert_user/) to perform the insert operation.[/info]
 -->
[info]値をエスケープするには、[`wp_slash()`](https://developer.wordpress.org/reference/functions/wp_slash/) を使用します。PHP の `compact()` 関数を使用して、これらの値から配列を作成します。[`wp_insert_user()`](https://developer.wordpress.org/reference/functions/wp_insert_user/) は、挿入操作を実行します。[/info]

<!-- 
Please refer to the Function Reference about `wp_create_user()` for full explanation about the used parameters.
 -->
使用パラメータについての完全な説明は、`wp_create_user()` に関する関数リファレンスを参照してください。

<!-- 
#### Example Create
 -->
#### 作成の例

```
// check if the username is taken
$user_id = username_exists( $user_name );

// check that the email address does not belong to a registered user
if ( ! $user_id && email_exists( $user_email ) === false ) {
  // create a random password
  $random_password = wp_generate_password( 12, false );
  // create the user
  $user_id = wp_create_user(
    $user_name,
    $random_password,
    $user_email
  );
}
```

<!-- 
## Insert User
 -->
## ユーザーの挿入

```
wp_insert_user( $userdata );
```

<!-- 
[info]The function calls a filter for most predefined properties.
 -->
[info]この関数は、ほとんどの定義済みのプロパティに対するフィルターを呼び出します。

<!-- 
The function performs the action `user_register` when creating a user (user ID does not exist).
 -->
この関数は、(ユーザー ID が存在しない場合) ユーザーを作成する際に `user_register` というアクションを実行します。

<!-- 
The function performs the action `profile_update` when updating the user (user ID exists).[/info]
 -->
この関数は、(ユーザー ID が存在する場合) ユーザーを更新する際に、`profile_update` というアクションを実行します。[/info]

<!-- 
Please refer to the Function Reference about `wp_insert_user()` for full explanation about the used parameters.
 -->
使用パラメータについての完全な説明は、`wp_insert_user()` に関する関数リファレンスを参照してください。

<!-- 
### Example Insert
 -->
### 挿入の例

<!-- 
Below is an example showing how to insert a new user with the website profile field filled in.
 -->
以下は、Web サイト・プロフィール・フィールドに記入された新規ユーザーを挿入する方法を示す例です。

```
$username  = $_POST['username'];
$password  = $_POST['password'];
$website   = $_POST['website'];
$user_data = [
  'user_login' => $username,
  'user_pass'  => $password,
  'user_url'   => $website,
];

$user_id = wp_insert_user( $user_data );

// success
if ( ! is_wp_error( $user_id ) ) {
  echo 'User created: ' . $user_id;
}
```

<!-- 
## Updating Users
 -->
## ユーザーの更新

<!-- 
`wp_update_user()` Updates a single user in the database. The update data is passed along in the `$userdata` array/object.
 -->
`wp_update_user()` は、データベース内の単一のユーザーを更新します。更新データは、配列/オブジェクト `$userdata` で渡されます。

<!-- 
To update a single piece of user meta data, use `update_user_meta()` instead. To create a new user, use `wp_insert_user()` instead.
 -->
単一のユーザー・メタデータを更新するには、代わりに `update_user_meta()` を使用します。新しいユーザーを作成するには、代わりに `wp_insert_user()` を使用します。

<!-- 
[info]If current user's password is being updated, then the cookies will be cleared![/info]
 -->
[info]現在のユーザーのパスワードが更新される場合、Cookies はクリアされます ! [/info]

<!-- 
Please refer to the Function Reference about `wp_update_user()` for full explanation about the used parameters.
 -->
使用パラメータについての完全な説明は、`wp_update_user()` に関する関数リファレンスを参照してください。

<!-- 
### Example Update
 -->
### 更新の例

<!-- 
Below is an example showing how to update a user's website profile field.
 -->
以下は、ユーザーの Web サイト・プロフィール・フィールドを更新する方法を示す例です。

```
$user_id = 1;
$website = 'https://wordpress.org';

$user_id = wp_update_user(
  array(
    'ID'       => $user_id,
    'user_url' => $website,
  )
);

if ( is_wp_error( $user_id ) ) {
  // error
} else {
  // success
}
```

<!-- 
## Deleting Users
 -->
## ユーザーの削除

<!-- 
`wp_delete_user()` deletes the user and optionally reassign associated entities to another user ID.
 -->
`wp_delete_user()` はユーザーを削除し、付随するエンティティを別のユーザー ID に再割り当てします。

<!-- 
[info]The function performs the action `deleted_user` after the user have been deleted.[/info]
 -->
[info]この関数は、ユーザーが削除された後に、`deleted_user` というアクションを実行します。[/info]

<!-- 
[alert]If the `$reassign` parameter is not set to a valid user ID, then all entities belonging to the deleted user will be deleted![/alert]
 -->
[alert]`$reassign` パラメータに有効なユーザー ID が設定されていない場合、削除されたユーザーに属するすべてのエンティティが削除されます ! [/alert]

<!-- 
Please refer to the Function Reference about `wp_delete_user()` for full explanation about the used parameters.
 -->
使用パラメータについての完全な説明は、`wp_delete_user()` に関する関数リファレンスを参照してください。
