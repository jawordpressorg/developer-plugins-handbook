<!-- 
# Best Practices
 -->
# ベスト・プラクティス

<!-- 
Here are some best practices to help organize your code so it works well alongside WordPress core and other WordPress plugins.
 -->
WordPress コアや他の WordPress プラグインとうまく協調して動作するように、コードを構成するのに役立つベスト・プラクティスをいくつか紹介します。

<!-- 
## Avoid Naming Collisions
 -->
## ネーミング衝突の回避

<!-- 
A naming collision happens when your plugin is using the same name for a variable, function or a class as another plugin.
 -->
ネーミング衝突は、あなたのプラグインが他のプラグインと同じ変数名、関数名、クラス名を使用している場合に起こります。

<!-- 
Luckily, you can avoid naming collisions by using the methods below.
 -->
幸いなことに、以下の方法でネーミングの衝突を避けることができます。

<!-- 
## Procedural Coding Method
 -->
## 手続き的コーディング手法

<!-- 
By default, all variables, functions and classes are defined in the **global namespace**, which means that it is possible for your plugin to override variables, functions and classes set by another plugin and vice-versa. Variables that are defined _inside_ of functions or classes are not affected by this.
 -->
デフォルトでは、すべての変数、関数、クラスは**グローバル名前空間**で定義されます。つまり、あなたのプラグインは、他のプラグインによって設定された変数、関数、クラスをオーバーライドできます (逆もまた然り)。関数やクラスの_内部_で定義された変数は、この影響を受けません。

<!-- 
### Prefix Everything
 -->
### すべてに接頭辞をつける

<!-- 
All globally accessible code should be prefixed with a _unique_ identifier. Prefixes prevent conflicts with other plugins and prevents them from overwriting your variables and accidentally calling your functions and classes.
 -->
グローバルにアクセス可能なすべてのコードには、_ユニークな_識別子を接頭辞として付ける必要があります。接頭辞は他のプラグインとの競合を防ぎ、プラグインがあなたの変数を上書きしたり、誤ってあなたの関数やクラスを呼び出したりするのを防ぎます。

<!-- 
In order to prevent conflicts with other plugins, your prefix should be at least 3 letters long, though we recommend 5. You should avoid using a common English word, and instead choose something unique to your plugin. We host tens of thousands of plugins on WordPress.org alone. There are hundreds of thousands more outside our servers. You're _going_ to run into conflicts.
 -->
他のプラグインとの競合を避けるため、接頭辞は、少なくとも3文字、5文字以上を推奨します。一般的な英単語を使うのは避け、プラグイン独自のものを選ぶべきです。私たちは WordPress.org だけで何万ものプラグインをホストしています。私たちのサーバーの外側には、さらに何十万ものプラグインがあります。競合に_遭遇する_ことになるでしょう。

<!-- 
A good way to do this is with a prefix. For example, if your plugin is called "Easy Custom Post Types" then you could use names like these:
 -->
これを可能にする良い方法は、接頭辞を使うことです。たとえば、あなたのプラグインが「Easy Custom Post Types」という名前なら、以下のような名前を使うことができます:

- `function ecpt_save_post()`
- `define( 'ECPT_LICENSE', true );`
- `class ECPT_Admin{}`
- `namespace EasyCustomPostTypes;`
- `update_option( 'ecpt_settings', $settings );`

<!-- 
[info]Because you are making code as a part of the **WordPress** project, you must avoid the use of prefixes that have a high probability of conflicting with the core WordPress. This includes but is not limited to: `__` (double underscores), `wp_` , `WordPress`, or `_` (single underscore)
 -->
[info]**WordPress** プロジェクトの一部としてコードを作成するため、WordPress のコアと競合する可能性の高い接頭辞の使用は避けなければなりません。これには右記のものが含まれますが、これらに限定されません: `__` (アンダースコア2つ)、`wp_`、`WordPress`、`_` (アンダースコア1つ)

<!-- 
If you are making code for a 'sub' plugin (such as a WooCommece extension), you would similarly need to avoid using any of their normal/common prefixes (i.e. Woo, WooCommerce).
 -->
「サブ」プラグイン (WooCommece 機能拡張など) のコードを作成する場合、同様に通常の接頭辞 (Woo、WooCommerce など) を使用しないようにする必要があります。

<!-- 
You can use them _inside_ your classes or namespace, but not as stand-alone function/namespace/class.[/info]
 -->
クラスや名前空間の_内部_で使用できますが、独立した関数/名前空間/クラスとして使用できません。[/info]

<!-- 
If you're using `_n()` or `__()` for translation, that's fine. We're **only** talking about functions you've created for your plugin, not the core functions from WordPress. In fact, those core features are _why_ you need to not use those prefixes in your own plugin! You wouldn't want to break WordPress for your users.
 -->
翻訳に `_n()` や `__()` を使っているのであれば、それでかまいません。WordPress のコア機能ではなく、あなたのプラグイン用に作成した関数について**だけ**述べています。実際、これらのコア機能こそが、自分のプラグインでこれらの接頭辞を使わないようにする_理由_なのです ! ユーザーのために WordPress を壊したくはないでしょう。

<!-- 
Remember: Good prefix names are unique and distinct to your plugin. This will help you and the next person in debugging, as well as prevent conflicts.
 -->
忘れないでください: 良い接頭辞名とは、あなたのプラグインに固有のものです。これは、あなたや後から参加する人のデバグに役立ちますし、競合を防ぐことにもなります。

<!-- 
Code that **must** be prefixed includes:
 -->
接頭辞をつけなければ**ならない**コードには、以下のようなものがあります:

<!-- 
- Functions (unless namespaced)
- Classes, interfaces, and traits (unless namespaced)
- Namespaces
- Global variables
- Options and transients
 -->
- (名前空間がない場合) 関数
- (名前空間がない場合) クラス、インターフェイス、および Trait
- 名前空間
- グローバル変数
- オプションおよび Transient

<!-- 
### Check for Existing Implementations
 -->
### 既存の実装に対するチェック

<!-- 
PHP provides a number of functions to verify existence of variables, functions, classes and constants. All of these will return true if the entity exists.
 -->
PHP には、変数や関数、クラス、定数の実在性を検証するための関数が多数用意されています。これらはすべて、実体が存在すれば true を返します。

<!-- 
- **Variables**: [isset()](https://www.php.net/manual/en/function.isset.php) (includes arrays, objects, etc.)
- **Functions**: [function_exists()](https://www.php.net/manual/en/function.function-exists.php)
- **Classes**: [class_exists()](https://www.php.net/manual/en/function.class-exists.php)
- **Constants**: [defined()](https://www.php.net/manual/en/function.defined.php)
 -->
- **変数**: [isset()](https://www.php.net/manual/en/function.isset.php) (配列、オブジェクトなどを含む)
- **関数**: [function_exists()](https://www.php.net/manual/en/function.function-exists.php)
- **クラス**: [class_exists()](https://www.php.net/manual/en/function.class-exists.php)
- **定数**: [defined()](https://www.php.net/manual/en/function.defined.php)

<!-- 
Keep in mind that using `(!function_exists('NAME')) {` around all your functions and classes sounds like a great idea until you realize the fatal flaw. If something else has a function with the same name and their code loads first, your plugin will break. Using if-exists to replace/override a function or class should be reserved for _shared_ libraries only.
 -->
すべての関数やクラスで `(!function_exists('NAME')) {` を使うことはすばらしいアイデアに思えるかもしれませんが、致命的な欠点がある点に注意してください。もし他の何かが同じ名前の関数を持ち、そのコードが先に読み込まると、あなたのプラグインは壊れてしまいます。if-exists を使って関数やクラスを置き換えたりオーバーライドしたりするのは、_共有_ ライブラリだけにとどめてください。

<!-- 
### Example
 -->
### 例

```
// Create a function called "wporg_init" if it doesn't already exist
if ( ! function_exists( 'wporg_init' ) ) {
  function wporg_init() {
    register_setting( 'wporg_settings', 'wporg_option_foo' );
  }
}

// Create a function called "wporg_get_foo" if it doesn't already exist
if ( ! function_exists( 'wporg_get_foo' ) ) {
  function wporg_get_foo() {
    return get_option( 'wporg_option_foo' );
  }
}
```

<!-- 
## Object Oriented Programming Method
 -->
## オブジェクト指向プログラミング手法

<!-- 
An easier way to tackle the naming collision problem is to use a [class](https://www.php.net/manual/en/language.oop5.php) for the code of your plugin.
 -->
名前の衝突問題にもっと簡単に取り組む方法は、プラグインのコードに [class](https://www.php.net/manual/en/language.oop5.php) を使うことです。

<!-- 
You will still need to take care of checking whether the name of the class you want is already taken but the rest will be taken care of by PHP.
 -->
希望するクラス名がすでに使われているかどうかをチェックする必要はありますが、あとは PHP がやってくれます。

<!-- 
### Example
 -->
### 例

```
if ( ! class_exists( 'WPOrg_Plugin' ) ) {
  class WPOrg_Plugin {
    public static function init() {
      register_setting( 'wporg_settings', 'wporg_option_foo' );
    }

    public static function get_foo() {
      return get_option( 'wporg_option_foo' );
    }
  }

  WPOrg_Plugin::init();
  WPOrg_Plugin::get_foo();
}
```

<!-- 
## File Organization
 -->
## ファイル構成

<!-- 
The root level of your plugin directory should contain your `plugin-name.php` file and, optionally, your [uninstall.php](https://developer.wordpress.org/plugins/plugin-basics/uninstall-methods/) file. All other files should be organized into sub folders whenever possible.
 -->
プラグインディレクトリのルートレベルには、ファイル `plugin-name.php` と、必要に応じてファイル [uninstall.php](https://developer.wordpress.org/plugins/plugin-basics/uninstall-methods/) を置いてください。その他のファイルは、可能な限り、サブフォルダーに整理しましょう。

<!-- 
### Folder Structure
 -->
### フォルダー構造

<!-- 
A clear folder structure helps you and others working on your plugin keep similar files together.
 -->
明確なフォルダー構造は、あなたやあなたのプラグインで作業している他の人が同じようなファイルをまとめておくのに役立ちます。

<!-- 
Here's a sample folder structure for reference:
 -->
参考までに、フォルダー構造の例を挙げておきます:

```
/plugin-name
  plugin-name.php
  uninstall.php
  /languages
  /includes
  /admin
    /js
    /css
    /images
  /public
    /js
    /css
    /images
```

<!-- 
## Plugin Architecture
 -->
## プラグイン・アーキテクチャー

<!-- 
The architecture, or code organization, you choose for your plugin will likely depend on the size of your plugin.
 -->
プラグインに選択するアーキテクチャー (またはコード構成) は、プラグインのサイズによって異なります。

<!-- 
For small, single-purpose plugins that have limited interaction with WordPress core, themes or other plugins, there's little benefit in engineering complex classes; unless you know the plugin is going to expand greatly later on.
 -->
WordPress のコアやテーマ、他のプラグインとの相互作用が限られている、小規模で単一目的のプラグインの場合、複雑なクラスを設計するメリットはほとんどありません。ただし、そのプラグインが後で大きく拡張されることがわかっている場合は、別です。

<!-- 
For large plugins with lots of code, start off with classes in mind. Separate style and scripts files, and even build-related files. This will help code organization and long-term maintenance of the plugin.
 -->
コードがたくさんある大規模なプラグインでは、まずクラスを考慮に入れてスタートしましょう。スタイルファイルとスクリプトファイル、そしてビルド関連ファイルも分けてください。こうすることで、コードを構成しやすくなり、プラグインの長期的なメンテナンスがしやすくなります。

<!-- 
### Conditional Loading
 -->
### 条件付き読み込み

<!-- 
It's helpful to separate your admin code from the public code. Use the conditional [is_admin()](https://developer.wordpress.org/reference/functions/is_admin/). You must still perform capability checks as this doesn't indicate the user is authenticated or has Administrator-level access. See [Checking User Capabilities](https://developer.wordpress.org/plugins/security/checking-user-capabilities/).
 -->
管理者用のコードと一般向けのコードを分けておくと便利です。条件式 [is_admin()](https://developer.wordpress.org/reference/functions/is_admin/) を使いましょう。これは、ユーザーが認証済みであること、または管理者レベルのアクセス権を持っていることを示すものではないため、依然として権限チェックを実施する必要があります。[ユーザー権限のチェック](https://developer.wordpress.org/plugins/security/checking-user-capabilities/)を参照してください。

<!-- 
For example:
 -->
例:

```
if ( is_admin() ) {
  // we are in admin mode
  require_once __DIR__ . '/admin/plugin-name-admin.php';
}
```

<!-- 
### Avoiding Direct File Access
 -->
### ファイルへの直接アクセスの回避

<!-- 
As a security precaution, it's a good practice to disallow access if the `ABSPATH` global is not defined. This is only applicable to files which contain code outside of class or function definitions, such as the main plugin file.
 -->
セキュリティの観点から、グローバル `ABSPATH` が定義されていない場合は、アクセスを許可しないようにするのがグッド・プラクティスです。これはメインプラグインファイルのような、クラスや関数の定義以外のコードを含むファイルにのみ適用されます。

<!-- 
You can implement this by including this code at the top of the file:
 -->
このコードをファイルの先頭に記述することで、実装できます:

```
if ( ! defined( 'ABSPATH' ) ) {
  exit; // Exit if accessed directly
}
```

<!-- 
### Architecture Patterns
 -->
### アーキテクチャー・パターン

<!-- 
While there are a number of possible architecture patterns, they can broadly be grouped into three variations:
 -->
アーキテクチャー・パターンはいくつも考えられるが、大まかに3つのバリエーションに分類できます:

<!-- 
- [Single plugin file, containing functions](https://github.com/GaryJones/move-floating-social-bar-in-genesis/blob/master/move-floating-social-bar-in-genesis.php)
- [Single plugin file, containing a class, instantiated object and optionally functions](https://github.com/norcross/wp-comment-notes/blob/master/wp-comment-notes.php)
- [Main plugin file, then one or more class files](https://github.com/DevinVinson/WordPress-Plugin-Boilerplate)
 -->
- [関数を含む、単一のプラグインファイル](https://github.com/GaryJones/move-floating-social-bar-in-genesis/blob/master/move-floating-social-bar-in-genesis.php)
- [クラス、インスタンス化されたオブジェクト、そして必要に応じて関数を含む、単一のプラグインファイル](https://github.com/norcross/wp-comment-notes/blob/master/wp-comment-notes.php)
- [メイン・プラグインファイルと、1つ以上のクラスファイル](https://github.com/DevinVinson/WordPress-Plugin-Boilerplate)

<!-- 
### Architecture Patterns Explained
 -->
### アーキテクチャー・パターンの説明

<!-- 
Specific implementations of the more complex of the above code organizations have already been written up as tutorials and slides:
 -->
上記のうち、より複雑なコード構成の具体的な実装は、すでにチュートリアルやスライドとして書かれています:

<!-- 
- [Slash – Singletons, Loaders, Actions, Screens, Handlers](https://jjj.blog/2012/12/slash-architecture-my-approach-to-building-wordpress-plugins/)
- [Implementing the MVC Pattern in WordPress Plugins](https://iandunn.name/content/presentations/wp-oop-mvc/mvc.php)
 -->
- [SLASH – シングルトン、ローダー、アクション、スクリーン、ハンドラー](https://jjj.blog/2012/12/slash-architecture-my-approach-to-building-wordpress-plugins/)
- [WordPress プラグインでの MVC パターンの実装](https://iandunn.name/content/presentations/wp-oop-mvc/mvc.php)

<!-- 
## Boilerplate Starting Points
 -->
## 起点となる定型文

<!-- 
Instead of starting from scratch for each new plugin you write, you may want to start with a **boilerplate**. One advantage of using a boilerplate is to have consistency among your own plugins. Boilerplates also make it easier for other people to contribute to your code if you use a boilerplate they are already familiar with.
 -->
新しいプラグインを書くたびにゼロから始めるのではなく、**定型文**から始めるとよいでしょう。定型文を使う利点のひとつは、自分のプラグインに一貫性を持たせることです。もしあなたが定型文を使っていれば、定型文を使うことで、他の人はすでに慣れ親しんでいるので、彼らがあなたのコードに貢献しやすくなります。

<!-- 
These also serve as further examples of different yet comparable architectures.
 -->
これらはまた、異なるが同等のアーキテクチャーのさらなる例となります。

<!-- 
- [WordPress Plugin Boilerplate](https://github.com/DevinVinson/WordPress-Plugin-Boilerplate): A foundation for WordPress Plugin Development that aims to provide a clear and consistent guide for building your plugins.
- [WordPress Plugin Bootstrap](https://github.com/claudiosanches/wordpress-plugin-boilerplate): Basic bootstrap to develop WordPress plugins using Grunt, Compass, GIT, and SVN.
- [WP Skeleton Plugin](https://github.com/ptahdunbar/wp-skeleton-plugin): Skeleton plugin that focuses on unit tests and use of composer for development.
- [WP CLI Scaffold](https://developer.wordpress.org/cli/commands/scaffold/plugin/): The Scaffold command of WP CLI creates a skeleton plugin with options such as CI configuration files.
 -->
- [WordPress プラグイン・ボイラープレート](https://github.com/DevinVinson/WordPress-Plugin-Boilerplate): WordPress プラグイン開発のための基盤で、プラグインを構築するための明確で一貫したガイドを提供することを目的としています。
- [WordPress プラグイン・ブートストラップ](https://github.com/claudiosanches/wordpress-plugin-boilerplate): Grunt、Compass、Git、Svn を使って WordPress プラグインを開発するための基本的なブートストラップです。
- [WP Skeleton Plugin](https://github.com/ptahdunbar/wp-skeleton-plugin): ユニットテストと開発用の Composer の使用に焦点を当てた、ひな型プラグインです。
- [WP CLI Scaffold](https://developer.wordpress.org/cli/commands/scaffold/plugin/): WP CLI の Scaffold コマンドは、CI 設定ファイルなどのオプションを持つ、ひな型プラグインを作成します。

<!-- 
Of course, you could take different aspects of these and others to create your own custom boilerplate.
 -->
もちろん、これらや他のものの異なる要素を取り入れて、独自の定型文も作成できます。