<!-- 
# Advanced Topics
 -->
# 高度な話題

<!-- 
## Removing Actions and Filters
 -->
## アクションおよびフィルターの削除

<!-- 
Sometimes you want to remove a callback function from a hook that another plugin, theme or even WordPress Core has registered.
 -->
他のプラグインやテーマ、あるいは WordPress Core が登録したフックからコールバック関数を削除したいことがあります。

<!-- 
To remove a callback function from a hook, you need to call `remove_action()` or `remove_filter()`, depending whether the callback function was added as an Action or a Filter.
 -->
フックからコールバック関数を削除する場合は、コールバック関数がアクションとして追加されたのかフィルターとして追加されたのかによって、`remove_action()` か `remove_filter()` を呼び出す必要があります。

<!-- 
The parameters passed to `remove_action()` / `remove_filter()` must be identical to the parameters passed to `add_action()` / `add_filter()` that registered it, or the removal won't work.
 -->
`remove_action()` / `remove_filter()` に渡されるパラメータは、それを登録した `add_action()` / `add_filter()` に渡されるパラメータと同一でなければ、削除がうまく働きません。

<!-- 
[alert]To successfully remove a callback function you must perform the removal after the callback function was registered. The order of execution is important.[/alert]
 -->
[alert]コールバック関数を正常に削除する場合は、コールバック関数が登録された後に削除する必要があります。実行順序は重要です。[/alert]

<!-- 
## Example
 -->
## 例

<!-- 
Let's say we want to improve the performance of a large theme by removing unnecessary functionality.
 -->
たとえば、不要な機能を削除して大規模テーマのパフォーマンスを向上させたいとしましょう。

<!-- 
Let's analyze the theme's code by looking into `functions.php`.
 -->
`functions.php` を見て、テーマのコードを分析してみましょう。

```
function wporg_setup_slider() {
  // ...
}
add_action( 'template_redirect', 'wporg_setup_slider', 9 );
```

<!-- 
The `wporg_setup_slider` function is adding a slider that we don't need, which probably loads a huge CSS file followed by a JavaScript initialization file which uses a custom written library the size of 1MB. We can can get rid of that.
 -->
`wporg_setup_slider` 関数は、必要のないスライダーを追加しており、おそらく巨大な CSS ファイルをロードし、その後に、1MB サイズのカスタムライブラリを使用する JavaScript の初期化ファイルをロードしています。それを取り除くことができます。

<!-- 
Since we want to hook into WordPress after the `wporg_setup_slider` callback function was registered (`functions.php` executed) our best chance would be the [`after_setup_theme`](https://developer.wordpress.org/reference/hooks/after_setup_theme/) hook.
 -->
`wporg_setup_slider` コールバック関数が登録された (`functions.php` が実行された) 後に WordPress にフックしたいので、最善の機会は [`after_setup_theme`](https://developer.wordpress.org/reference/hooks/after_setup_theme/) フックでしょう。

```
function wporg_disable_slider() {
  // Make sure all parameters match the add_action() call exactly.
  remove_action( 'template_redirect', 'wporg_setup_slider', 9 );
}
// Make sure we call remove_action() after add_action() has been called.
add_action( 'after_setup_theme', 'wporg_disable_slider' );
```

<!-- 
## Removing All Callbacks
 -->
## すべてのコールバックの削除

<!-- 
You can also remove all of the callback functions associated with a hook by using `remove_all_actions()` / `remove_all_filters()`.
 -->
`remove_all_actions()` / `remove_all_filters()` を使えば、フックに関連するコールバック関数をすべて削除できます。

<!-- 
## Determining the Current Hook
 -->
## 現在のフックの特定

<!-- 
Sometimes you want to run an Action or a Filter on multiple hooks, but behave differently based on which one is currently calling it.
 -->
複数のフックに対してアクションやフィルターを作動させたいが、現在どのフックが呼び出しているかによって動作を変えたいことがあります。

<!-- 
You can use the `current_action()` / `current_filter()` to determine the current Action / Filter.
 -->
`current_action()` / `current_filter()` を使用して、現在のアクション/フィルターを特定できます。

```
function wporg_modify_content( $content ) {
  switch ( current_filter() ) {
    case 'the_content':
      // Do something.
      break;
    case 'the_excerpt':
      // Do something.
      break;
  }
  return $content;
}

add_filter( 'the_content', 'wporg_modify_content' );
add_filter( 'the_excerpt', 'wporg_modify_content' );
```

<!-- 
## Checking How Many Times a Hook Has Run
 -->
## フックの作動回数の確認

<!-- 
Some hooks are called multiple times in the course of execution, but you may only want your callback function to run once.
 -->
フックの中には実行の過程で何度も呼び出されるものもあるが、コールバック関数は一度だけ実行させたい場合もあるでしょう。

<!-- 
In this situation, you can check how many times the hook has run with the [` did_action()`](https://developer.wordpress.org/reference/functions/did_action/).
 -->
この場合、フックが何回作動したかを [`did_action()`](https://developer.wordpress.org/reference/functions/did_action/) で確認できます。

```
function wporg_custom() {
  // If save_post has been run more than once, skip the rest of the code.
  if ( did_action( 'save_post' ) !== 1 ) {
    return;
  }
  // ...
}
add_action( 'save_post', 'wporg_custom' );
```

<!-- 
## Debugging with the "all" Hook
 -->
## 「all」フックを使ったデバッグ

<!-- 
If you want a callback function to fire on every single hook, you can register it to the `all` hook. Sometimes this is useful in debugging situations to help determine when a particular event is happening or when a page is crashing.
 -->
すべてのフックに対してコールバック関数を起動させたい場合は、`all` フックに登録します。これはデバッグの場面で、ある特殊なイベントが発生したときや、ページがクラッシュしたときを確定するのに役立つことがあります。

```
function wporg_debug() {
  echo '<p>' . current_action() . '</p>';
}
add_action( 'all', 'wporg_debug' );
```