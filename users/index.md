<!--
# Users
-->

# ユーザー

<!--
A _User_ is an access account with corresponding capabilities within the WordPress installation. Each WordPress user has, at the bare minimum, a username, password and email address.
-->

「ユーザー」とは、WordPress のインストール内で対応する権限を持つアクセスアカウントのことです。WordPress の各ユーザーは、最低限、ユーザー名、パスワード、メールアドレスを持っています。

<!--
Once a user account is created, that user may log in using the WordPress Admin (or programmatically) to access WordPress functions and data. WordPress stores the Users in the `users` table.
-->

ユーザーアカウントが作成されると、そのユーザーは WordPress 管理画面を使って (またはプログラムを使って) ログインし、WordPress の機能やデータにアクセスできます。WordPress は、ユーザーを `users` テーブルに格納します。

<!--
## Roles and Capabilities
-->

## 権限グループと権限

<!--
Users are assigned [roles](https://developer.wordpress.org/plugins/users/roles-and-capabilities/#roles), and each role has a set of [capabilities](https://developer.wordpress.org/plugins/users/roles-and-capabilities/#capabilities).
-->

ユーザーには[権限グループ](https://ja.wordpress.org/team/handbook/plugin-development/users/roles-and-capabilities/#roles)が割り当てられ、各権限グループには[権限](https://ja.wordpress.org/team/handbook/plugin-development/users/roles-and-capabilities/#capabilities)のセットがあります。

<!--
You can create new roles with their own set of capabilities. Custom capabilities can also be created and assigned to existing roles or new roles.
-->

独自の権限を持つ新しい権限グループを作成できます。カスタム権限を作成して、既存の権限グループや新しい権限グループに割り当てることもできます。

<!--
In WordPress, developers can take advantage of user roles to limit the set of actions an account can perform.
-->

WordPress では、開発者はユーザー権限グループを利用して、アカウントが実行できる一連のアクションを制限できます。

<!--
## The Principle of Least Privileges
-->

## 最小権限の原則

<!--
WordPress adheres to the principal of least privileges, the practice of giving a user _only_ the privileges that are essential for performing the desired work. You should follow this lead when possible by creating roles where appropriate and checking capabilities before performing sensitive tasks.
-->

WordPress は、最小権限の原則を遵守しています。最小権限の原則とは、目的の作業をするために必要な権限_のみ_をユーザーに与えるという慣習です。必要に応じて権限グループを作成し、機密性の高い作業をする前に権限を確認することで、可能な限りこの原則に従うべきです。
