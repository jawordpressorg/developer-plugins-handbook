<!-- 
# jQuery
 -->
# jQuery

<!-- 
## Using jQuery
 -->
## jQuery の使用

<!-- 
Your jQuery script runs on the user's browser after your WordPress webpage is received. A basic jQuery statement has two parts: a selector that determines which HTML elements the code applies to, and an action or event, which determines what the code does or what it reacts to. The basic event statement looks like this:
 -->
jQuery スクリプトは、WordPress の Web ページを受信した後、ユーザーのブラウザー上で実行されます。基本的な jQuery ステートメントには2つの部分があります: コードが適用される HTML 要素を決定するセレクタ、そして、コードが何をするか、何に反応するかを決定するアクションまたはイベントです。基本的なイベントステートメントは、次のようになります:

```
jQuery.(selector).event(function);
```

<!-- 
When an event, such as a mouse click, occurs in an HTML element selected by the selector, the function that is defined inside the final set of parentheses is executed.
 -->
セレクターで選択された HTML 要素で、マウスクリックなど、イベントが発生した際、最後の括弧の中で定義された関数が実行されます。

<!-- 
All the following code examples are based on this HTML page content. Assume it appears on your plugin's admin settings screen, defined by the file `myplugin_settings.php`. It is a simple table with radio buttons next to each title.
 -->
以下のコード例はすべて、この HTML ページの内容にもとづいています。ファイル `myplugin_settings.php` で定義されたプラグインの管理画面上に表示されると仮定します。各タイトルの横にラジオボタンがある、シンプルなテーブルです。

```
<form id="radioform">
  <table>
    <tbody>
    <tr>
      <td><input class="pref" checked="checked" name="book" type="radio" value="Sycamore Row" />Sycamore Row</td>
      <td>John Grisham</td>
    </tr>
    <tr>
      <td><input class="pref" name="book" type="radio" value="Dark Witch" />Dark Witch</td>
      <td>Nora Roberts</td>
    </tr>
    </tbody>
  </table>
</form>
```

<!-- 
The output could look something like this on your settings page.
 -->
出力は、設定ページで次のように表示されます。

<!-- 
![Sample Table](https://i3.wp.com/make.wordpress.org/docs/files/2013/11/pdh-ajax-example.png)
 -->
![サンプル・テーブル](https://i3.wp.com/make.wordpress.org/docs/files/2013/11/pdh-ajax-example.png)

<!-- 
In the [article on AJAX](https://developer.wordpress.org/plugins/javascript/ajax/), we will build an AJAX exchange that saves the user selection in usermeta and adds the number of posts tagged with the selected title. Not a very practical application, but it illustrates all the important steps. jQuery code can either reside in an external file or be output to the page inside a `<script>` block. We will focus on the external file variation because passing values from PHP requires special attention. The same code can be output to the page if that seems more expedient to you.
 -->
[AJAX の記事](https://developer.wordpress.org/plugins/javascript/ajax/)で、ユーザーの選択を usermeta に保存し、選択されたタイトルでタグ付けされた投稿の数を追加する AJAX 交換を構築します。あまり実用的なアプリケーションではありませんが、すべての重要なステップを説明しています。jQuery のコードは、外部ファイルに置くか、`<script>` ブロックの中でページに出力できます。PHP から値を渡すには特別な注意が必要ですので、ここでは外部ファイルのバリエーションに焦点を当てます。その方が便利だと思われる場合は、同じコードをページに出力できます。

<!-- 
### Selector and Event
 -->
### セレクターとイベント

<!-- 
The selector is the same form as CSS selectors: `.class` or `#id`. There's many [more forms](https://api.jquery.com/category/selectors/ "jQuery Reference"), but these are the two you will frequently use. In our example, we will use class `.pref`. There's also a slew of possible [events](https://api.jquery.com/category/events/ "jQuery Reference"), one you will likely use a lot is _‘click'_. In our example we will use _‘change'_ to capture a radio button selection. Be aware that jQuery events are often named somewhat differently than those with JavaScript. So far, after we add in an empty anonymous function, our example statement looks like this:
 -->
セレクターは CSS セレクタと同じ形式です: `.class` または `#id`。もっと[多くの形式](https://api.jquery.com/category/selectors/ "jQuery Reference")がありますが、よく使うのはこの2つです。この例では、クラス `.pref` を使用します。また、[イベント](https://api.jquery.com/category/events/ "jQuery Reference")はたくさんありますが、その中でもよく使うのは _‘click'_ でしょう。この例では、_‘change'_ を使ってラジオボタンの選択を捕捉します。jQuery のイベントの名前は、JavaScript のイベントとは多少異なることが多いので、注意してください。ここまでで、空の無名関数を追加すると、例のステートメントは次のようになります:

```
$.(".pref").change(function(){
  /*do stuff*/
});
```

<!-- 
This code will "do stuff" when any element of the "pref" class changes.
 -->
このコードは、"pref" クラスの要素が変更されたときに「何かをします」。

<!-- 
[info]This code snippet, and all examples on this page, are for illustrating the use of AJAX. The code is not suitable for production environments because related operations such as [sanitization](https://developer.wordpress.org/plugins/security/securing-input/), [security](https://developer.wordpress.org/apis/security/nonces/), [error handling](https://www.sitepoint.com/error-handling-in-php/), and [internationalization](https://developer.wordpress.org/plugins/internationalization/) have been intentionally omitted. Be sure to always address these important operations in your production code.[/info]
 -->
[info]このコードスニペット、そしてこのページのすべての例は、AJAX の使用を説明するためのものです。[サニタイズ](https://developer.wordpress.org/plugins/security/securing-input/)、[セキュリティ](https://developer.wordpress.org/apis/security/nonces/)、[エラー処理](https://www.sitepoint.com/error-handling-in-php/)、そして[国際化](https://developer.wordpress.org/plugins/internationalization/)などの関連処理が意図的に省略されているため、コードは本番環境には適していません。本番環境のコードでは、必ずこれらの重要な操作に対処してください。[/info]