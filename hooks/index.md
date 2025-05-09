<!--
# Hooks
-->

# フック

<!--
Hooks are a way for one piece of code to interact/modify another piece of code at specific, pre-defined spots. They make up the foundation for how plugins and themes interact with WordPress Core, but they’re also used extensively by Core itself.
-->

フックとは、あるコード片が、あらかじめ定義された特定の場所で、別のコード片と相互作用したり修正したりするための方法です。プラグインやテーマが WordPress Core と相互作用するための基盤となっていますが、Core 自体でも広く使われています。

<!--
There are two types of hooks: [Actions](https://developer.wordpress.org/plugins/hooks/actions/) and [Filters](https://developer.wordpress.org/plugins/hooks/filters/). To use either, you need to write a custom function known as a `Callback`, and then register it with a WordPress hook for a specific action or filter.
-->

フックには2種類あります: [アクション](https://ja.wordpress.org/team/handbook/plugin-development/hooks/actions/)と[フィルター](https://ja.wordpress.org/team/handbook/plugin-development/hooks/filters/)です。どちらも使用するには、`Callback` と呼ばれるカスタム関数を記述し、特定のアクションまたはフィルター用の WordPress フックに登録する必要があります。

<!--
[Actions](https://developer.wordpress.org/plugins/hooks/actions/) allow you to add data or change how WordPress operates. Actions will run at a specific point in the execution of WordPress Core, plugins, and themes. Callback functions for Actions can perform some kind of a task, like echoing output to the user or inserting something into the database. Callback functions for an Action do not return anything back to the calling Action hook.
-->

[アクション](https://ja.wordpress.org/team/handbook/plugin-development/hooks/actions/)は、データを追加したり、WordPress の操作方法を変更したりできます。アクションは WordPress Core、プラグイン、テーマの実行の特定の時点で作動します。アクション用のコールバック関数は、ユーザーへのエコー出力やデータベースへの挿入など、何らかのタスクを実行できます。アクション用のコールバック関数は、呼び出したアクションフックに何も返しません。

<!--
[Filters](https://developer.wordpress.org/plugins/hooks/filters/) give you the ability to change data during the execution of WordPress Core, plugins, and themes. Callback functions for Filters will accept a variable, modify it, and return it. They are meant to work in an isolated manner, and should never have [side effects](https://en.wikipedia.org/wiki/Side_effect_(computer_science)) such as affecting global variables and output. Filters expect to have something returned back to them.
-->

[フィルター](https://ja.wordpress.org/team/handbook/plugin-development/hooks/filters/)は WordPress Core、プラグイン、テーマの実行中にデータを変更する機能を提供します。フィルター用コールバック関数は、変数を受け取り、修正し、返します。フィルターは単独で動作するものであり、グローバル変数や出力に影響を与えるような[副作用](https://en.wikipedia.org/wiki/Side_effect_(computer_science))があってはなりません。フィルターは、何かが返ってくることを期待します。

<!--
WordPress provides many hooks that you can use, but you can also [create your own](https://developer.wordpress.org/plugins/hooks/custom-hooks/) so that other developers can extend and modify your plugin or theme.
-->

WordPress は、あなたが使用できる多くのフックを提供していますが、他の開発者があなたのプラグインやテーマを拡張したり変更したりできるように、[自分で作成する](https://ja.wordpress.org/team/handbook/plugin-development/hooks/custom-hooks/)こともできます。

<!--
## Actions vs. Filters
-->

## アクション対フィルター

<!--
The main difference between an action and a filter can be summed up like this:
-->

アクションとフィルターの主な違いは、次のようにまとめられます:

<!--
- An action takes the info it receives, does something with it, and returns nothing. In other words: it _acts_ on something and then exits, returning nothing back to the calling hook.
- A filter takes the info it receives, modifies it somehow, and returns it. In other words: it _filters_ something and passes it back to the hook for further use.
-->

- アクションは、情報を受け取り、それを使って何かを行い、何も返しません。言い換えれば: アクションは何かに _作用_ して終了し、呼び出し元のフックには何も返しません。
- フィルターは、情報を受け取り、それを何らかの方法で修正し、それを返します。言い換えれば: 何かを _フィルター_ して、それをフックに戻し、さらに使えるようにします。

<!--
Said another way:
-->

別の言い方をしましょう:

<!--
- An action interrupts the code flow to do something, and then returns back to the normal flow without modifying anything;
- A filter is used to modify something in a specific way so that the modification is then used by code later on.
-->

- アクションは、コードフローに割り込んで「何か」を行い、何も変更せずに通常のフローに戻ります。
- フィルターは、特定の方法で「何か」を修正するために使用され、その修正は後のコードで使用されます。

<!--
The _something_ referred to is the parameter list sent via the hook definition. More on this in later sections.
-->

ここでいう _何か_ とは、フック定義を通じて送られるパラメータ・リストのことです。これについては後のセクションで詳しく説明します。

<!--
## More Resources
-->

## その他の情報源

<!--
- [Filter Reference](https://codex.wordpress.org/Plugin_API/Filter_Reference)
- [Action Reference](https://codex.wordpress.org/Plugin_API/Action_Reference)
-->

- [フィルター・リファレンス](https://codex.wordpress.org/Plugin_API/Filter_Reference)
- [アクション・リファレンス](https://codex.wordpress.org/Plugin_API/Action_Reference)
