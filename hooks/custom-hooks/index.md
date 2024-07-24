<!-- 
# Custom Hooks
 -->
# カスタム・フック

<!-- 
An important, but often overlooked practice is using custom hooks in your plugin so that other developers can extend and modify it.
 -->
重要ですが、見落とされがちな特徴として、プラグイン内でカスタムフックを使用すると、他の開発者がプラグインを拡張し、修正できます。

<!-- 
Custom hooks are created and called in the same way that WordPress Core hooks are.
 -->
カスタムフックは、WordPress コアフックと同じように作成され、呼び出されます。

<!-- 
## Create a Hook
 -->
## フックの作成

<!-- 
To create a custom hook, use [`do_action()`](https://developer.wordpress.org/reference/functions/do_action/) for [Actions](https://developer.wordpress.org/plugins/hooks/actions/) and [`apply_filters()`](https://developer.wordpress.org/reference/functions/apply_filters/) for [Filters](https://developer.wordpress.org/plugins/hooks/filters/).
 -->
カスタムフックを作成する場合、[アクション](https://developer.wordpress.org/plugins/hooks/actions/)には [`do_action()`](https://developer.wordpress.org/reference/functions/do_action/) を、[フィルター](https://developer.wordpress.org/plugins/hooks/filters/)には [`apply_filters()`](https://developer.wordpress.org/reference/functions/apply_filters/) を使用します。

<!-- 
[info]We recommend using [`apply_filters()`](https://developer.wordpress.org/reference/functions/apply_filters/) on any text that is output to the browser. Particularly on the frontend.
 -->
[info]ブラウザに出力されるテキストには [`apply_filters()`](https://developer.wordpress.org/reference/functions/apply_filters/) を使うことをおすすめします。とりわけフロントエンドでは。

<!-- 
This makes it easier for plugins to be modified according to the user's needs.[/info]
 -->
これにより、ユーザーのニーズに応じてプラグインを簡単に修正できます。[/info]

<!-- 
## Add a Callback to the Hook
 -->
## フックへのコールバックの追加

<!-- 
To add a callback function to a custom hook, use [`add_action()`](https://developer.wordpress.org/reference/functions/add_action/) for [Actions](https://developer.wordpress.org/plugins/hooks/actions/) and [`add_filter()`](https://developer.wordpress.org/reference/functions/add_filter/) for [Filters](https://developer.wordpress.org/plugins/hooks/filters/).
 -->
カスタムフックにコールバック関数を追加する場合、[アクション](https://developer.wordpress.org/plugins/hooks/actions/)には [`add_action()`](https://developer.wordpress.org/reference/functions/add_action/) を、[フィルター](https://developer.wordpress.org/plugins/hooks/filters/)には [`add_filter()`](https://developer.wordpress.org/reference/functions/add_filter/) を使用します。

<!-- 
## Naming Conflicts
 -->
## 名前の競合

<!-- 
Naming conflicts ("collisions") occur when two developers use the same hook name for completely different purposes. This leads to difficult to find bugs. So it's important to prefix your hook names with a unique string to avoid hook name collisions.collisions with other plugins.
 -->
名前の競合 (「衝突」) は、2人の開発者が同じフック名をまったく異なる目的で使用する場合に発生します。これは発見しにくいバグにつながります。そのため、他のプラグインとのフック名の衝突を避けるために、フック名の前にユニークな文字列を付けることが重要です。

<!-- 
For example, a filter named `email_body` is generic enough that two or more developers could use this hook in different plugins for different purposes. So to avoid this, a prefix is added. For example, functions used as examples in this handbook use `wporg_` as the prefix.
 -->
たとえば、`email_body` という名前のフィルターは、2人以上の複数の開発者が異なるプラグインで異なる目的のためにこのフックを使うことができるほど汎用的です。そのため、これを避けるために接頭辞を付けます。たとえば、このハンドブックで例として使われている関数は、接頭辞として `wporg_` を使っています。

<!-- 
When you choose your prefix, you can use your company name, your wp handle, the plugin name, anything you like really. The goal is to make it unique so choose wisely.
 -->
接頭辞を選ぶ際には、会社名、WordPress ハンドルネーム、プラグイン名など、なんでも好きなものを使うことができます。目標はユニークなものにすることですので、賢く選びましょう。

<!-- 
## Examples
 -->
## 例

<!-- 
### Extensible Action: Settings Form
 -->
### 拡張可能なアクション: 設定フォーム

<!-- 
If your plugin adds a settings form to the Administrative Panels, you can use Actions to allow other plugins to add their own settings to it.
 -->
プラグインが管理パネルに設定フォームを追加する場合、アクションを使用して、他のプラグインが独自の設定を追加できるようにできます。

```
do_action( 'wporg_after_settings_page_html' );
```

<!-- 
Now another plugin can register a callback function for the `wporg_after_settings_page_html` hook and inject new settings:
 -->
これで、別のプラグインが `wporg_after_settings_page_html` フック用のコールバック関数を登録し、新しい設定を注入できるようになりました:

```
add_action( 'wporg_after_settings_page_html', 'myprefix_add_settings' );
```

<!-- 
Note that because this is an action, no value is returned. Also note that since no priority is given, it will run at default priority 10.
 -->
これはアクションですので、値は返されないことに注意してください。また、優先順位が与えられていないので、デフォルトの優先順位10で作動されることにも注意してください。

<!-- 
### Extensible Filter: Custom Post Type
 -->
### 拡張可能なフィルター: カスタム投稿タイプ

<!-- 
In this example, when the new post type is registered, the parameters that define it are passed through a filter, so another plugin can change them before the post type is created.
 -->
この例では、新しい投稿タイプが登録されるときに、それを定義するパラメータはフィルターを通して渡されるので、投稿タイプが作成される前に別のプラグインがそれらを変更できます。

```
function wporg_create_post_type() {
  $post_type_params = [/* ... */];

  register_post_type(
    'post_type_slug',
    apply_filters( 'wporg_post_type_params', $post_type_params )
  );
}
```

<!-- 
Now another plugin can register a callback function for the `wporg_post_type_params` hook and change post type parameters:
 -->
これで、別のプラグインが `wporg_post_type_params` フック用のコールバック関数を登録し、投稿タイプのパラメータを変更できるようになりました:

```
function myprefix_change_post_type_params( $post_type_params ) {
  $post_type_params['hierarchical'] = true;
  return $post_type_params;
}
add_filter( 'wporg_post_type_params', 'myprefix_change_post_type_params' );
```

<!-- 
Note that filters take data, modify it, and return it. So the code called ( `myprefix_change_post_type_params` ) doesn't output anything using echo or html, or anything else directly to the screen. Also note that the returned value is used directly by `register_post_type` without being assigned to a variable first. This is simple to skip that extra (an unnecessary) step.
 -->
フィルターはデータを受け取り、修正し、それを返すことに注意してください。そのため、( `myprefix_change_post_type_params` ) というコードは、echo や html などを使って直接画面に何も出力しません。また、返された値は変数に代入されることなく `register_post_type` によって直接使用されることにも注意してください。これは、その余分な (不必要な) ステップを省略するための単純なものです。

<!-- 
Also note that since no priority is given, it will run at default priority 10. And since there is no value for the number of parameters expected, the default of one is assumed.
 -->
また、優先順位が与えられていないので、デフォルトの優先順位10で作動されることにも注意してください。また、予想されるパラメータの数の値がないので、デフォルトの1つと仮定されます。