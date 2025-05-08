<!--
# Filters
-->

# フィルター

<!--
**Filters** are one of the two types of [Hooks](https://developer.wordpress.org/plugins/hooks/).
-->

**フィルター**は、2種類の[フック](https://developer.wordpress.org/plugins/hooks/)のうちの1つです。

<!--
They provide a way for functions to modify data during the execution of WordPress Core, plugins, and themes. They are the counterpart to [Actions](https://developer.wordpress.org/plugins/hooks/actions/).
-->

WordPress Core、プラグイン、テーマの実行中にデータを修正するための関数を提供します。[アクション](https://developer.wordpress.org/plugins/hooks/actions/)と対になるものです。

<!--
Unlike [Actions](https://developer.wordpress.org/plugins/hooks/actions/), filters are meant to work in an isolated manner, and should never have [side effects](https://en.wikipedia.org/wiki/Side_effect_(computer_science)) such as affecting global variables and output. Filters expect to have something returned back to them.
-->

[アクション](https://developer.wordpress.org/plugins/hooks/actions/)とは異なり、フィルターは単独で動作するものであり、グローバル変数や出力に影響を与えるような[副作用](https://en.wikipedia.org/wiki/Side_effect_(computer_science))を持つべきではありません。フィルターは、何かが返ってくることを期待します。

<!--
## Add Filter
-->

## フィルターの追加

<!--
The process of adding a filter includes two steps.
-->

フィルターを追加するプロセスには、2つのステップがあります。

<!--
First, you need to create a Callback function which will be called when the filter is run. Second, you need to add your Callback function to a hook which will perform the calling of the function.
-->

まず、フィルターが実行されたときに呼び出されるコールバック関数を作成する必要があります。次に、コールバック関数を、関数呼び出しするフックに追加します。

<!--
You will use the [`add_filter()`](https://developer.wordpress.org/reference/functions/add_filter/) function, passing at least two parameters:
-->

[`add_filter()`](https://developer.wordpress.org/reference/functions/add_filter/) 関数を使い、少なくとも2つのパラメータを渡します:

<!--
1. `string $hook_name` which is the name of the filter you’re hooking to, and
2. `callable $callback` the name of your callback function.
-->

1. `string $hook_name` は、フックするフィルターの名前です。
2. `callable $callback` は、コールバック関数の名前です。

<!--
The example below will run when the `the_title` filter is executed.
-->

以下の例は、`the_title` フィルターが実行されたときに作動します。

```
function wporg_filter_title( $title ) {
  return 'The ' . $title . ' was filtered';
}
add_filter( 'the_title', 'wporg_filter_title' );
```

<!--
Lets say we have a post title, "Learning WordPress", the above example will modify it to be "The Learning WordPress was filtered".
-->

たとえば、「Learning WordPress」という投稿タイトルがあるとすると、上記の例では「The Learning WordPress was filtered」に修正されます。

<!--
You can refer to the [Hooks](https://developer.wordpress.org/plugins/hooks/) chapter for a list of available hooks.
-->

利用可能なフックのリストについては、[フック](https://developer.wordpress.org/plugins/hooks/)の章を参照してください。

<!--
As you gain more experience, looking through WordPress Core source code will allow you to find the most appropriate hook.
-->

経験を積むにつれ、WordPress Core のソースコードに目を通すことで、最も適切なフックを見つけることができます。

<!--
### Additional Parameters
-->

### 追加パラメータ

<!--
[`add_filter()`](https://developer.wordpress.org/reference/functions/add_filter/) can accept two additional parameters, `int $priority` for the priority given to the callback function, and `int $accepted_args` for the number of arguments that will be passed to the callback function.
-->

[`add_filter()`](https://developer.wordpress.org/reference/functions/add_filter/) は2つの追加パラメータを受け取ることができ、`int $priority` にはコールバック関数に与える優先度を、`int $accepted_args` にはコールバック関数に渡す引数の数を指定します。

<!--
For detailed explanation of these parameters please read the article on [Actions](https://developer.wordpress.org/plugins/hooks/actions/).
-->

これらのパラメータの詳細については、[アクション](https://developer.wordpress.org/plugins/hooks/actions/)の記事をお読みください。

<!--
### Example
-->

### 例

<!--
To add a CSS class to the `<body>` tag when a certain condition is met:
-->

`<body>` タグに、ある条件を満たした場合に CSS クラスを追加するには:

```
function wporg_css_body_class( $classes ) {
  if ( ! is_admin() ) {
    $classes[] = 'wporg-is-awesome';
  }
  return $classes;
}
add_filter( 'body_class', 'wporg_css_body_class' );
```
