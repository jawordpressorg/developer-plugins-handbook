<!--
# Checking User Capabilities
-->

# ユーザー権限の確認

<!--
If your plugin allows users to submit data—be it on the Admin or the Public side—it should check for User Capabilities.
-->

プラグインがユーザーにデータを送信させる場合、— それが管理者側であれ、公開側であれ —「ユーザー権限」をチェックする必要があります。

<!--
## User Roles and Capabilities
-->

## ユーザーの権限グループと権限

<!--
The most important step in creating an efficient security layer is having a user permission system in place. WordPress provides this in the form of [User Roles and Capabilities](https://developer.wordpress.org/plugins/users/roles-and-capabilities/).
-->

効率的なセキュリティ・レイヤを構築するうえで、最も重要なステップは、ユーザー・アクセス許可システムを導入することです。WordPress は、これを[ユーザーの権限グループと権限](https://ja.wordpress.org/team/handbook/plugin-development/users/roles-and-capabilities/)という形で提供しています。

<!--
Every user logged into WordPress is automatically assigned specific User capabilities depending on their User role.
-->

WordPress にログインしているすべてのユーザーには、ユーザーの権限グループに応じて、特定のユーザー権限が自動的に割り当てられます。

<!--
**User roles** is just a fancy way of saying which group the user belongs to. Each group has a specific set of predefined capabilities.
-->

**ユーザー権限グループ** は、ユーザーがどのグループに属しているかを示す、洒落た表現です。各グループは、事前に定義された権限の、特定のセットを持っています。

<!--
For example, the main user of your website will have the User role of an Administrator while other users might have roles like Editor or Author. You could have more than one user assigned to a role, i.e. there might be two Administrators for a website.
-->

たとえば、Web サイトのメインユーザーは管理者というユーザー権限グループを持ち、他のユーザーは編集者や投稿者といった権限グループを持つかもしれません。1つの権限グループに複数のユーザーを割り当てることもできます。たとえば、1つの Web サイトに2人の管理者がいるような場合です。

<!--
**User capabilities** are the specific permissions that you assign to each user or to a User role.
-->

**ユーザー権限** は、各ユーザーまたはユーザー権限グループに割り当てる、特定のアクセス許可です。

<!--
For example, Administrators have the `manage_options` capability which allows them to view, edit and save options for the website. Editors on the other hand lack this capability which will prevent them from interacting with options.
-->

たとえば、管理者は権限 `manage_options` を持っており、Web サイトのオプションを表示、編集、保存できます。一方、編集者にはこの権限がないため、オプションを操作できません。

<!--
These capabilities are then checked at various points within the Admin. Depending on the capabilities assigned to a role; menus, functionality, and other aspects of the WordPress experience may be added or removed.
-->

これらの権限は、管理画面のさまざまな場所でチェックされます。ユーザー権限グループに割り当てられた権限によって、メニュー、機能、その他の WordPress 体験の側面が追加または削除される可能性があります。

<!--
**As you build a plugin, make sure to run your code only when the current user has the necessary capabilities.**
-->

**プラグインを作成する際には、現在のユーザーが必要な権限を持っている場合にのみ、コードを実行するようにしてください。**

<!--
### Hierarchy
-->

### ヒエラルキー (階層構造)

<!--
The higher the user role, the more capabilities the user has. Each user role inherits the previous roles in the hierarchy.
-->

ユーザー権限グループが高いほど、ユーザーはより多くの権限を持ちます。各ユーザー権限グループは、ヒエラルキーの直前の権限グループを継承します。

<!--
For example, the "Administrator", which is the highest user role on a single site installation, inherits the following roles and their capabilities: "Subscriber", "Contributor", "Author" and "Editor".
-->

たとえば、「管理者」は、1つのサイト・インストールにおける最高のユーザー権限グループであり、「購読者」、「寄稿者」、「投稿者」、「編集者」の権限グループとその権限を継承します。

<!--
## Examples
-->

## 例

<!--
### No Restrictions
-->

### 制限なし

<!--
The example below creates a link on the frontend which gives the ability to trash posts. Because this code does not check user capabilities, **it allows any visitor to the site to trash posts!**
-->

以下の例では、投稿をゴミ箱に捨てるためのリンクを、フロントエンドに作成しています。このコードはユーザーの権限をチェックしないため、**サイトへの訪問者なら誰でも、投稿をゴミ箱に捨てることができます !**

```
/**
 * Generate a Delete link based on the homepage url.
 *
 * @param string $content   Existing content.
 *
 * @return string|null
 */
function wporg_generate_delete_link( $content ) {
  // Run only for single post page.
  if ( is_single() && in_the_loop() && is_main_query() ) {
    // Add query arguments: action, post.
    $url = add_query_arg(
      [
        'action' => 'wporg_frontend_delete',
        'post'   => get_the_ID(),
      ], home_url()
    );

    return $content . ' <a href="' . esc_url( $url ) . '">' . esc_html__( 'Delete Post', 'wporg' ) . '</a>';
  }

  return null;
}

/**
 * Request handler
 */
function wporg_delete_post() {
  if ( isset( $_GET['action'] ) && 'wporg_frontend_delete' === $_GET['action'] ) {

    // Verify we have a post id.
    $post_id = ( isset( $_GET['post'] ) ) ? ( $_GET['post'] ) : ( null );

    // Verify there is a post with such a number.
    $post = get_post( (int) $post_id );
    if ( empty( $post ) ) {
      return;
    }

    // Delete the post.
    wp_trash_post( $post_id );

    // Redirect to admin page.
    $redirect = admin_url( 'edit.php' );
    wp_safe_redirect( $redirect );

    // We are done.
    die;
  }
}

/**
 * Add the delete link to the end of the post content.
 */
add_filter( 'the_content', 'wporg_generate_delete_link' );

/**
 * Register our request handler with the init hook.
 */
add_action( 'init', 'wporg_delete_post' );
```

<!--
### Restricted to a Specific Capability
-->

### 特定の権限に限定

<!--
The example above allows any visitor to the site to click on the "Delete" link and trash the post. However, we only want Editors and above to be able to click on the "Delete" link.
-->

上記の例では、サイトの訪問者であれば誰でも「削除」リンクをクリックし、投稿をゴミ箱に捨てることができます。しかし、「削除」リンクをクリックできるのは、「編集者」以上に限定したいと思っています。

<!--
To accomplish this, we will check that the current user has the capability `edit_others_posts`, which only Editors or above would have:
-->

これを実現するため、「編集者」以上しか持っていない、権限 `edit_others_posts` を現在のユーザーが持っているかどうかをチェックします:

```
/**
 * Generate a Delete link based on the homepage url.
 *
 * @param string $content   Existing content.
 *
 * @return string|null
 */
function wporg_generate_delete_link( $content ) {
  // Run only for single post page.
  if ( is_single() && in_the_loop() && is_main_query() ) {
    // Add query arguments: action, post.
    $url = add_query_arg(
      [
        'action' => 'wporg_frontend_delete',
        'post'   => get_the_ID(),
      ], home_url()
    );

    return $content . ' <a href="' . esc_url( $url ) . '">' . esc_html__( 'Delete Post', 'wporg' ) . '</a>';
  }

  return null;
}

/**
 * Request handler
 */
function wporg_delete_post() {
  if ( isset( $_GET['action'] ) && 'wporg_frontend_delete' === $_GET['action'] ) {

    // Verify we have a post id.
    $post_id = ( isset( $_GET['post'] ) ) ? ( $_GET['post'] ) : ( null );

    // Verify there is a post with such a number.
    $post = get_post( (int) $post_id );
    if ( empty( $post ) ) {
      return;
    }

    // Delete the post.
    wp_trash_post( $post_id );

    // Redirect to admin page.
    $redirect = admin_url( 'edit.php' );
    wp_safe_redirect( $redirect );

    // We are done.
    die;
  }
}

/**
 * Add delete post ability
 */
add_action('plugins_loaded', 'wporg_add_delete_post_ability');

function wporg_add_delete_post_ability() {    
  if ( current_user_can( 'edit_others_posts' ) ) {
    /**
     * Add the delete link to the end of the post content.
     */
    add_filter( 'the_content', 'wporg_generate_delete_link' );

    /**
     * Register our request handler with the init hook.
     */
    add_action( 'init', 'wporg_delete_post' );
  }
}
```
