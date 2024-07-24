<!-- 
# Actions
 -->
# アクション

<!-- 
**Actions** are one of the two types of [Hooks](https://developer.wordpress.org/plugins/hooks/). They provide a way for running a function at a specific point in the execution of WordPress Core, plugins, and themes. Callback functions for an Action do not return anything back to the calling Action hook. They are the counterpart to [Filters](https://developer.wordpress.org/plugins/hooks/filters/). Here is a refresher of [the difference between actions and filters](https://developer.wordpress.org/plugins/hooks/#actions-vs-filters).
 -->
**アクション**は、[フック](https://developer.wordpress.org/plugins/hooks/)の2つのタイプのうちの1つです。WordPress Core、プラグイン、テーマの実行中の特定のポイントで関数を作動させる方法を提供します。アクション用のコールバック関数は、呼び出したアクションフックに何も返しません。[フィルター](https://developer.wordpress.org/plugins/hooks/filters/)と対になるものです。ここで[アクションとフィルターの違い](https://developer.wordpress.org/plugins/hooks/#actions-vs-filters)を再確認しておきましょう。

<!-- 
## Adding an Action
 -->
## アクションの追加

<!-- 
The process of adding an action includes two steps:
 -->
アクション追加のプロセスには、2つのステップがあります:

<!-- 
### Create a _callback function_
 -->
### _コールバック関数_ の作成

<!-- 
First, create a _callback function_. This function will be run when the action it is hooked to is run.
 -->
まず、_コールバック関数_ を作ります。この関数は、フックされたアクションが実行されたときに作動します。

<!-- 
The callback function is just like a normal function: it should be prefixed, and it should be in `functions.php` or somewhere callable. The parameters it should accept will be defined by the action you are hooking to; most hooks are well defined, so review the hooks docs to see what parameters the action you have selected will pass to your function.
 -->
コールバック関数は通常の関数と同じです: 接頭辞をつけ、`functions.php` または呼び出し可能な場所に記述します。この関数が受け取るべきパラメータは、フック先のアクションによって定義されます; ほとんどのフックはきちんと定義されているので、選択したアクションがどのパラメータを関数に渡すのか、フックのドキュメントを確認してください。

<!-- 
### Assign (_hook_) your callback function
 -->
### コールバック関数の割り当て (_フック_)

<!-- 
Second, add your callback function to the action. This is called _hooking_ and tells the action to run your callback function when the action is run.
 -->
次に、コールバック関数をアクションに追加します。これは _hooking_ と呼ばれ、アクションが実行されたときにコールバック関数を作動させるようにアクションに指示します。

<!-- 
When your callback function is ready, use [add_action()](https://developer.wordpress.org/reference/functions/add_action/) to hook it to the action you have selected. At a minimum, `add_action()` requires two parameters:
 -->
コールバック関数の準備ができたら、[add_action()](https://developer.wordpress.org/reference/functions/add_action/) を使って、選択したアクションにフックします。最低限、`add_action()` は2つのパラメータを必要とします:

<!-- 
1. `string $hook_name` which is the name of the action you're hooking to, and
2. `callable $callback` the name of your callback function.
 -->
1. `string $hook_name` は、フックするアクションの名前で、
2. `callable $callback` は、コールバック関数の名前です。

<!-- 
The example below will run `wporg_callback()` when the `init` hook is executed:
 -->
以下の例では、`init` フックが実行されると `wporg_callback()` が作動します:

```
function wporg_callback() {
  // do something
}
add_action( 'init', 'wporg_callback' );
```

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
`add_action()` can accept two additional parameters, `int $priority` for the priority given to the callback function, and `int $accepted_args` for the number of arguments that will be passed to the callback function.
 -->
`add_action()` は2つの追加パラメータを受け取ることができ、`int $priority` はコールバック関数に与える優先度、`int $accepted_args` はコールバック関数に渡される引数の数です。

<!-- 
#### Priority
 -->
#### 優先順位

<!-- 
Many callback functions can be hooked to a single action. The `init` hook for example gets a lot of use. There may be cases where you need to ensure that your callback function runs before or after other callback functions, even when those other functions may not yet have been hooked.
 -->
多数のコールバック関数を、単一のアクションにフックできます。たとえば、`init` フックはよく使われます。このとき他のコールバック関数の前、または後、ときには他のコールバック関数がまだフックされていないタイミングで、コールバック関数の実行を保証したい場合があります。

<!-- 
WordPress determines the order that callback functions are run based on two things: The first way is by manually setting the _priority_. This is done using the third argument to `add_action()`.
 -->
WordPress は、コールバック関数の実行順序を2つのことにもとづいて決定します: 1つ目は、手動で _優先度_ を設定する方法です。これは `add_action()` の第三引数を使って行います。

<!-- 
Here are some important facts about priorities:
 -->
優先順位に関する重要な事実をいくつか紹介しましょう:

<!-- 
- priorities are positive integers, typically between 1 and 20
- the default priority (meaning, the priority assigned when no `priority` value is manually supplied) is 10
- there is no theoretical upper limit on the priority value, but the realistic upper limit is 100
 -->
- 優先度は、正の整数で、通常は1から20の間です。
- (手動で `priority` 値を指定しなかった場合に割り当てられる) デフォルトの優先度は10です。
- 優先度の理論的な上限はないが、現実的な上限は100です。

<!-- 
A function with a priority of 11 will run _after_ a function with a priority of 10; and a function with a priority of 9 will run _before_ a function with a priority of 10.
 -->
優先度11の関数は、優先度10の関数の _後_ に実行され、優先度9の関数は、優先度10の関数の _前_ に実行されます; 優先度9の関数は、優先度10の関数の_前_ に実行されます。

<!-- 
The second way that callback function order is determined is simply by the order in which it was registered _within the same priority value_. So if two callback functions are registered for the same hook with the same priority, they will be run in the order that they were registered to the hook.
 -->
コールバック関数の順番が決定される2つ目の方法は、単純に _同じ優先度同士_ で登録された順番です。つまり、2つのコールバック関数が同じフックに同じ優先度で登録されている場合、フックに登録された順番に実行されます。

<!-- 
For example, the following callback functions are all registered to the `init` hook, but with different priorities:
 -->
たとえば、以下のコールバック関数はすべて `init` フックに登録されているが、優先順位は異なります:

```
add_action( 'init', 'wporg_callback_run_me_late', 11 );
add_action( 'init', 'wporg_callback_run_me_normal' );
add_action( 'init', 'wporg_callback_run_me_early', 9 );
add_action( 'init', 'wporg_callback_run_me_later', 11 );
```

<!-- 
In the example above:
 -->
上記の例では:

<!-- 
- The first function run will be `wporg_callback_run_me_early()`, because it has a manual priority of 9
- Next, `wporg_callback_run_me_normal(),` because it has no priority set and so its priority is 10
- Next, `wporg_callback_run_me_late()` is run because it has a manual priority of 11
- Finally, `wporg_callback_run_me_later()` is run: it also has a priority of 11, but it was hooked after `wporg_callback_run_me_late()`.
 -->
- 最初に実行される関数は、優先順位は9ですので、`wporg_callback_run_me_early()` となります。
- 次は、優先順位が設定されていないので、優先順位は10になる `wporg_callback_run_me_normal()` です。
- 次が、優先順位が11に手動で設定されている `wporg_callback_run_me_late()` です。
- 最後に `wporg_callback_run_me_later()` が作動します: これも優先順位は11だが、`wporg_callback_run_me_late()` の後にフックされました。

<!-- 
#### Number of Arguments
 -->
#### 引数の数

<!-- 
Sometimes it's desirable for a callback function to receive some extra data related to the action being hooked to.
 -->
コールバック関数が、フックされているアクションに関連する追加データを受け取ることが望ましい場合があります。

<!-- 
For example, when WordPress saves a post and runs the [`save_post`](https://developer.wordpress.org/reference/hooks/save_post/) hook, it passes two parameters to the callback function: the ID of the post being saved, and the post object itself:
 -->
たとえば、WordPress が投稿を保存して [`save_post`](https://developer.wordpress.org/reference/hooks/save_post/) フックを実行すると、コールバック関数に2つのパラメータが渡されます: 保存される投稿の ID と、投稿オブジェクト自身です:

```
do_action( 'save_post', $post->ID, $post );
```

<!-- 
When a callback function is registered for the [`save_post`](https://developer.wordpress.org/reference/hooks/save_post/) hook, it can specify that it wants to receive those two parameters. It does so by telling `add_action` to expect them by (in this case) putting `2` as the fourth argument:
 -->
[`save_post`](https://developer.wordpress.org/reference/hooks/save_post/) フックにコールバック関数が登録されると、この2つのパラメータを受け取るように指定できます。(この例では) 4番目の引数として `2` を指定することで、`add_action` にそれらを受け取るように指示することで行います。:

```
add_action( 'save_post', 'wporg_custom', 10, 2 );
```

<!-- 
In order to actually receive those parameters in your callback function, modify the parameters your callback function will accept, like this:
 -->
コールバック関数でこれらのパラメータを実際に受け取るには、コールバック関数が受け取るパラメータを次のように修正します:

```
function wporg_custom( $post_id, $post ) {
  // do something
}
```

<!-- 
[tip]]It's good practice to give your callback function parameters the same name as the passed parameters, or as close as you can.[/tip]
 -->
[tip]コールバック関数のパラメータには、渡されたパラメータと同じ名前か、できるだけ近い名前をつけるのがよいプラクティスです。[/tip]