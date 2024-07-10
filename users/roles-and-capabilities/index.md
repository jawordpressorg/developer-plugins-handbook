<!-- 
# Roles and Capabilities
 -->
# 権限グループと権限

<!-- 
Roles and capabilities are two important aspects of WordPress that allow you to control user privileges.
 -->
権限グループと権限は、WordPress の2つの重要な側面で、ユーザー権限をコントロールできます。

<!-- 
WordPress stores the Roles and their Capabilities in the `options` table under the `user_roles` key.
 -->
WordPress は、権限グループとその権限を、テーブル `options` のキー `user_roles` の下に格納します。

<!-- 
## Roles
 -->
## 権限グループ

<!-- 
A role defines a set of capabilities for a user. For example, what the user may see and do in his dashboard.
 -->
権限グループは、ユーザーの一連の権限を定義します。たとえば、ユーザーが自分のダッシュボードで何を見たり、何をしたりできるかです。

<!-- 
**By default, WordPress have six roles:**
 -->
**デフォルトでは、WordPress には6つの権限グループがあります:**

<!-- 
- Super Admin
- Administrator
- Editor
- Author
- Contributor
- Subscriber
 -->
- 特権管理者 (Super Admin)
- 管理者 (Administrator)
- 編集者 (Editor)
- 投稿者 (Author)
- 寄稿者 (Contributor)
- 購読者 (Subscriber)

<!-- 
More roles can be added and the default roles can be removed.
 -->
権限グループを追加したり、デフォルトの権限グループを削除できます。

![Users roles](https://i3.wp.com/developer.wordpress.org/files/2014/09/wp-roles.png)

<!-- 
### Adding Roles
 -->
### 権限グループの追加

<!-- 
Add new roles and assign capabilities to them with [`add_role()`](https://developer.wordpress.org/reference/functions/add_role/).
 -->
[`add_role()`](https://developer.wordpress.org/reference/functions/add_role/) を使用して、新しい権限グループを追加し、権限を割り当てられます。

```
function wporg_simple_role() {
  add_role(
    'simple_role',
    'Simple Role',
    array(
      'read'         => true,
      'edit_posts'   => true,
      'upload_files' => true,
    ),
  );
}

// Add the simple_role.
add_action( 'init', 'wporg_simple_role' );
```

<!-- 
[alert]After the first call to [`add_role()`](https://developer.wordpress.org/reference/functions/add_role/), the Role and it's Capabilities will be stored in the database!
 -->
[alert]最初に [`add_role()`](https://developer.wordpress.org/reference/functions/add_role/) をコールすると、権限グループと権限がデータベースに格納されます !

<!-- 
Sequential calls will do nothing: including altering the capabilities list, which might not be the behavior that you're expecting.[/alert]
 -->
連続してコールしても、権限リストの変更も含めて、何もしません。これはあなたが期待している動作ではないかもしれません。[/alert]

<!-- 
[info]To alter the capabilities list in bulk: remove the role using [`remove_role()`](https://developer.wordpress.org/reference/functions/remove_role/) and add it again using [`add_role()`](https://developer.wordpress.org/reference/functions/add_role/) with the new capabilities.
 -->
[info]権限リストを一括で変更するには: [`remove_role()`](https://developer.wordpress.org/reference/functions/remove_role/) を使って権限グループを削除し、[`add_role()`](https://developer.wordpress.org/reference/functions/add_role/) を使って新しい権限を追加します。

<!-- 
Make sure to do it only if the capabilities differ from what you're expecting (i.e. condition this) or you'll degrade performance considerably![/info]
 -->
必ず、権限が期待しているものと異なる場合 (つまり、このような状態) にのみ実行してください。さもないと、パフォーマンスが著しく低下します ! [/info]

<!-- 
### Removing Roles
 -->
### 権限グループの削除

<!-- 
Remove roles with [`remove_role()`](https://developer.wordpress.org/reference/functions/remove_role/).
 -->
[`remove_role()`](https://developer.wordpress.org/reference/functions/remove_role/) で権限グループを削除します。

```
function wporg_simple_role_remove() {
  remove_role( 'simple_role' );
}

// Remove the simple_role.
add_action( 'init', 'wporg_simple_role_remove' );
```

<!-- 
[alert]After the first call to [`remove_role()`](https://developer.wordpress.org/reference/functions/remove_role/), the Role and it's Capabilities will be removed from the database!
 -->
[alert]最初に [`remove_role()`](https://developer.wordpress.org/reference/functions/remove_role/) をコールすると、権限グループと権限がデータベースから削除されます !

<!-- 
Sequential calls will do nothing.[/alert]
 -->
連続してコールしても、何もしません。[/alert]

<!-- 
[info]If you're removing the default roles:
 -->
[info]デフォルトの権限グループを削除する場合:

<!-- 
- We advise **against** removing the Administrator and Super Admin roles!
- Make sure to keep the code in your plugin/theme as future WordPress updates may add these roles again.
- Run `update_option('default_role', YOUR_NEW_DEFAULT_ROLE)` since you'll be deleting `subscriber` which is WP's default role.[/info]
 -->
- 管理者と特権管理者の権限グループを削除することに**反対**することを推奨します !
- WordPress の将来のアップデートで、これらの権限グループが再び追加される可能性があるので、プラグイン/テーマのコードは必ず保管しておいてください。
- WordPress のデフォルト権限グループである `subscriber` を削除するので、`update_option('default_role', YOUR_NEW_DEFAULT_ROLE)` を実行します。[/info]

<!-- 
## Capabilities
 -->
## 権限

<!-- 
Capabilities define what a **role** can and can not do: edit posts, publish posts, etc.
 -->
権限とは、**権限グループ**ができること、できないことを定義するものです: 投稿の編集、投稿の公開、等。

<!-- 
[info]Custom post types can require a certain set of Capabilities.[/info]
 -->
[info]カスタム投稿タイプは、特定の権限のセットを必要とすることがあります。[/info]

<!-- 
### Adding Capabilities
 -->
### 権限の追加

<!-- 
You may define new capabilities for a role.
 -->
権限グループに新しい権限を定義できます。

<!-- 
Use [`get_role()`](https://developer.wordpress.org/reference/functions/get_role/) to get the role object, then use the `add_cap()` method of that object to add a new capability.
 -->
[`get_role()`](https://developer.wordpress.org/reference/functions/get_role/) を使って権限グループオブジェクトを取得し、そのオブジェクトの `add_cap()` メソッドを使って新しい権限を追加します。

```
function wporg_simple_role_caps() {
  // Gets the simple_role role object.
  $role = get_role( 'simple_role' );

  // Add a new capability.
  $role->add_cap( 'edit_others_posts', true );
}

// Add simple_role capabilities, priority must be after the initial role definition.
add_action( 'init', 'wporg_simple_role_caps', 11 );
```

<!-- 
[info]It's possible to add custom capabilities to any role.
 -->
[info]どの権限グループにもカスタム権限を追加できます。

<!-- 
Under the default WordPress admin, they would have no effect, but they can be used for custom admin screen and front-end areas.[/info]
 -->
WordPress のデフォルトの管理画面では、これらは何の効果もありませんが、カスタムの管理画面やフロントエンドの領域には使用できます。[/info]

<!-- 
### Removing Capabilities
 -->
### 権限の削除

<!-- 
You may remove capabilities from a role.
 -->
権限グループから権限を削除できます。

<!-- 
The implementation is similar to Adding Capabilities with the difference being the use of `remove_cap()` method for the role object.
 -->
実装は「権限の追加」と似ていますが、違いは権限グループオブジェクトに `remove_cap()` メソッドを使うことです。

<!-- 
## Using Roles and Capabilities
 -->
## 権限グループと権限の使用

<!-- 
### Get Role
 -->
### 権限グループの取得

<!-- 
Get the role object including all of it's capabilities with [`get_role()`](https://developer.wordpress.org/reference/functions/get_role/).
 -->
[`get_role()`](https://developer.wordpress.org/reference/functions/get_role/) で、その権限グループのすべての権限を含む、権限グループオブジェクトを取得します。

<!-- 
### User Can
 -->
### ユーザーのできること

<!-- 
Check if a user have a specified **role** or **capability** with [`user_can()`](https://developer.wordpress.org/reference/functions/user_can/).
 -->
ユーザーが指定された**権限グループ**または**権限**を持っているかどうかを [`user_can()`](https://developer.wordpress.org/reference/functions/user_can/) でチェックします。

```
user_can( $user, $capability );
```

<!-- 
[warning]There is an undocumented, third argument, $args, that may include the object against which the test should be performed.
 -->
[warning]ドキュメント化されていない第3引数 $args があり、テスト対象のオブジェクトを含めることができます。

<!-- 
E.g. Pass a post ID to test for the capability of that specific post.[/warning]
 -->
例: 投稿 ID を渡して、特定の投稿の権限をテストする。[/warning]

<!-- 
### Current User Can
 -->
### 現在のユーザーのできること

<!-- 
[`current_user_can()`](https://developer.wordpress.org/reference/functions/current_user_can/) is a wrapper function for [`user_can()`](https://developer.wordpress.org/reference/functions/user_can/) using the current user object as the `$user` parameter.
 -->
[`current_user_can()`](https://developer.wordpress.org/reference/functions/current_user_can/) は [`user_can()`](https://developer.wordpress.org/reference/functions/user_can/) のラッパー関数で、現在のユーザーオブジェクトをパラメータ `$user` として使用します。

<!-- 
Use this in scenarios where back-end and front-end areas should require a certain level of privileges to access and/or modify.
 -->
これは、バックエンドとフロントエンドの領域が、アクセスや変更に一定レベルの権限を必要とするシナリオで使用します。

```
current_user_can( $capability );
```

<!-- 
### Example
 -->
### 例

<!-- 
Here's a practical example of adding an Edit link on the in a template file if the user has the proper capability:
 -->
ここでは、ユーザーが適切な権限を持っている場合に、テンプレート・ファイルに編集リンクを追加する実用的な例を示します:

```
if ( current_user_can( 'edit_posts' ) ) {
  edit_post_link( esc_html__( 'Edit', 'wporg' ), '<p>', '</p>' );
}
```

<!-- 
## Multisite
 -->
## マルチサイト

<!-- 
The [`current_user_can_for_blog()`](https://developer.wordpress.org/reference/functions/current_user_can_for_blog/) function is used to test if the current user has a certain **role** or **capability** on a specific blog.
 -->
[`current_user_can_for_blog()`](https://developer.wordpress.org/reference/functions/current_user_can_for_blog/) 関数は、現在のユーザーが特定のブログで特定の**権限グループ**または**権限**を持っているかどうかをテストするために使用されます。

```
current_user_can_for_blog( $blog_id, $capability );
```

<!-- 
## Reference
 -->
## 参考資料

<!-- 
Codex Reference for [User Roles and Capabilities](https://wordpress.org/documentation/article/roles-and-capabilities/).
 -->
[ユーザーの権限グループと権限](https://wordpress.org/documentation/article/roles-and-capabilities/)の Codex レファレンス。