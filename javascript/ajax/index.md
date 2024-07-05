# AJAX

<!-- 
## What is AJAX?
 -->
## AJAX とは ?

<!-- 
AJAX is the acronym for Asynchronous JavaScript And XML. XML is a data exchange format and UX is software developer shorthand for User Experience. Ajax is an Internet communications technique that allows a web page displayed in a user's browser to request specific information from a server and display this new information on the same page without the need to reload the entire page. You can already imagine how this improves the user experience.
 -->
AJAX とは、Asynchronous JavaScript And XML の頭文字をとったものです。XML はデータ交換フォーマットであり、UX はユーザー・エクスペリエンスを意味するソフトウェア開発者の略語です。Ajax とは、インターネット通信技術のひとつで、ユーザーのブラウザに表示された Web ページがサーバーに特定の情報を要求し、ページ全体を再読み込みすることなく、同じページに新しい情報を表示することを可能にするものです。これによってユーザー体験がどのように向上するか、すでに想像がつくことでしょう。

<!-- 
While XML is the traditional data exchange format used, the exchange can actually be any convenient format. When working with PHP code, many developers favor JSON because the internal data structure created from the transmitted data stream is easier to interface with.
 -->
XML は伝統的なデータ交換フォーマットを使用していますが、実際には便利なフォーマットであれば何でもかまいません。PHP のコードで作業する場合、多くの開発者は JSON を好みます。なぜなら、送信されたデータストリームから作成される内部データ構造は、取り扱う事が簡単だからです。

<!-- 
To see AJAX in action, go to your WordPress administration area and add a category or tag. Pay close attention when you click the Add New button, notice the page changes but does not actually reload. Not convinced? Check your browser's back history, if the page had reloaded, you would see two entries for the page.
 -->
AJAX の動作を確認するには、WordPress の管理エリアに行き、カテゴリーやタグを追加します。新規追加ボタンをクリックすると、ページが変わりますが、実際にはリロードされないことに注意してください。納得いかないですか ? ブラウザの履歴を確認すると、ページがリロードされた際、そのページに対して2つのエントリーが表示されているはずです。

<!-- 
AJAX does not even require a user action to work. Google Docs automatically saves your document every few minutes with AJAX without you needing to initiate a save action.
 -->
AJAX は、ユーザーの操作を必要としません。Google ドキュメントは、AJAX を使って数分ごとに自動的にドキュメントを保存し、保存のためのアクションを起こす必要はありません。

<!-- 
## Why use AJAX?
 -->
## なぜ AJAX を使うのか ?

<!-- 
Obviously, it improves the user experience. Instead of presenting a boring, static page, AJAX allows you to present a dynamic, responsive, user friendly experience. Users can get immediate feedback that some action they took was right or wrong. No need to submit an entire form before finding out there is a mistake in one field. Important fields can be validated as soon as the data is entered. Or suggestions could be made as the user types.
 -->
明らかに、ユーザー体験が向上します。退屈な静的ページを表示する代わりに、AJAX を使えば、ダイナミックで、レスポンシブで、ユーザーフレンドリーな体験を提供できます。ユーザーは、自分が取った操作が正しかったか間違っていたかのフィードバックを、即座に得ることができます。1つのフィールドに間違いがあることに気付く前に、フォーム全体を送信する必要はありません。重要なフィールドは、データが入力されるとすぐに検証できます。あるいは、ユーザーが入力する際に提案もできます。

<!-- 
AJAX can dramatically decrease the amount of data flowing back and forth. Only the pertinent data needs to be exchanged instead of all of the page content, which is what happens when the page reloads.
 -->
AJAX は、前後に流れるデータ量を劇的に減らすことができます。すべてのページ・コンテンツを交換するのではなく、適切なデータだけを交換する必要があります。ページがリロードされると、そのようなことが起こります。

<!-- 
Specifically related to WordPress plugins, AJAX is by far the best way to initiate a process independent of WordPress content. If you've programmed PHP before, you would likely do this by simply linking to a new PHP page. The user following the link initiates the process. The problem with this is that you cannot access any WordPress functions when you link to a new external PHP page. In the past, developers accessed WordPress functions by including the core file `wp-load.php` on their new PHP page. The problem with doing that is you cannot possibly know the correct path to this file anymore. The WordPress architecture is now flexible enough that the `/wp-content/` and your plugin files can be moved from its usual location to one level from the installation root. You cannot know where `wp-load.php` is relative to your plugin files, and you cannot know the absolute path to the installation folder either.
 -->
WordPress プラグインに特に関連することですが、AJAX は WordPress のコンテンツとは無関係に処理を開始する方法として圧倒的に優れています。PHP をプログラミングしたことがある人なら、新しい PHP ページにリンクするだけで、このようなことができるでしょう。ユーザーがリンクをたどると、処理が開始されます。この場合の問題は、新しい外部 PHP ページにリンクしたときに WordPress の関数にアクセスできないことです。以前は、開発者は新しい PHP ページにコアファイル `wp-load.php` を含めることで、WordPress の関数にアクセスしていました。そうすることの問題点は、このファイルへの正しいパスを知ることができなくなったことです。WordPress のアーキテクチャーは柔軟になり、`/wp-content/` やプラグインファイルはインストールルートから1階層下に移動できるようになりました。プラグインファイルからの相対パスで `wp-load.php` の場所を知ることはできませんし、インストールフォルダーへの絶対パスもわかりません。

<!-- 
What you can know is where to send an AJAX request, because it is defined in a global JavaScript variable. Your PHP AJAX handler script is actually an action hook, so all WordPress functions are automatically available to it, unlike an external PHP file.
 -->
AJAX リクエストを送信する場所は、JavaScript のグローバル変数に定義されているため、知ることができます。PHP の AJAX ハンドラスクリプトは、実際にはアクションフックですので、外部の PHP ファイルとは異なり、WordPress のすべての機能が自動的に利用できます。

<!-- 
## How Do I Use AJAX?
 -->
## AJAX はどのように使うのか ?

<!-- 
If you are new to WordPress but have experience using AJAX in other environments, you will need to relearn a few things. The way WordPress implements AJAX is most likely different than what you are used to. If everything is new to you, no problem. You will learn the basics here. Once you've developed a basic AJAX exchange, it's a cinch to expand on that base and develop that killer app with an awesome user interface!
 -->
WordPress は初めてだが、他の環境で AJAX を使用した経験がある場合、いくつかのことを学び直す必要があります。WordPress が AJAX を実装する方法は、ほとんどの場合、あなたが慣れているものとは異なります。すべてが初めての人は、問題ありません。ここで基本を学びましょう。一度基本的な AJAX 交換を開発すれば、そのベースを拡張して、すばらしいユーザーインターフェイスを持つキラーアプリを開発することは簡単ですよ !

<!-- 
There are two major components of any AJAX exchange in WordPress. The client side JavaScript or jQuery and the server side PHP. All AJAX exchanges follow the following sequence of events.
 -->
WordPress での AJAX 交換には、2つの主要なコンポーネントがあります。クライアントサイドの JavaScript または jQuery と、サーバーサイドの PHP です。すべての AJAX 交換は、以下のイベントのシーケンスに従って行われます。

<!-- 
1. Some sort of page event initiates a JavaScript or jQuery function. That function gathers some data from the page and sends it via a HTTP request to the server. Because handling HTTP requests with JavaScript is awkward and jQuery is bundled into WordPress anyway, we are going to focus only on jQuery code from here on out. AJAX with straight JavaScript is possible, but it's not worth doing it when jQuery is available.
2. The server receives the request and does something with the data. It may assemble related data and send it back to the client browser in the form of an HTTP response. This is not a requirement, but since keeping the user informed about what's going on is desirable, it's very rare not to send some kind of response.
3. The jQuery function that sent the initial AJAX request receives the server response and does something with it. It may update something on the page and/or present a message to the user by some means.
 -->
1. ある何らかのページ・イベントが、JavaScript または jQuery 関数を起動させます。その関数は、ページからデータを収集し、HTTP リクエストでサーバーに送信します。JavaScript で HTTP リクエストを処理するのはやっかいだし、jQuery は WordPress にバンドルされているから、ここから先は、jQuery のコードだけに集中することにします。JavaScript をそのまま使った AJAX も可能だが、jQuery が使えるのにやる価値はありません。
2. サーバーは、リクエストを受信し、そのデータで何かをします。関連するデータを組み立て、HTTP レスポンスの形でクライアント・ブラウザに送り返すかもしれません。これは必須条件ではありませんが、何が起こっているかをユーザーに知らせ続けることは望ましいことですので、何らかのレスポンスを送らないことは非常にまれです。
3. 最初の AJAX リクエストを送信した jQuery 関数は、サーバーレスポンスを受信し、それを使って何かします。ページ上の何かを更新したり、何らかの方法でユーザーにメッセージを表示したりします。

<!-- 
## Using AJAX with jQuery
 -->
## jQuery で AJAX を使用する

<!-- 
Now we will define the "do stuff" portion from the [snippet in the article on jQuery](https://developer.wordpress.org/plugins/javascript/jquery/#selector-and-event). We will use the [`$.post()`](https://api.jquery.com/jQuery.post/ "jQuery Reference") method, which takes 3 parameters: the URL to send the POST request to, the data to send, and a callback function to handle the server response. Before we do that though, we have a bit of advance planning to get out of the way. We do the following assignment for use later in the callback function. The purpose will be more evident in the [Callback section](https://developer.wordpress.org/plugins/javascript/ajax/#callback "Page section").
 -->
ここで、[jQuery の記事のスニペット](https://developer.wordpress.org/plugins/javascript/jquery/#selector-and-event)にある「do stuff」部分を定義します。ここでは、[`$.post()`](https://api.jquery.com/jQuery.post/ "jQuery Reference") メソッドを使用し、そのパラメータは、POST リクエストを送信する URL、送信するデータ、そしてサーバーのレスポンスを処理するコールバック関数、の3つになります。でも、その前に、ちょっとした下準備があります。後でコールバック関数で使うために、次のように割り当てします。目的は[コールバック項](https://developer.wordpress.org/plugins/javascript/ajax/#callback "Page section")で詳しく説明します。

### URL

<!-- 
All WordPress AJAX requests must be sent to `wp-admin/admin-ajax.php`. The correct, complete URL needs to come from PHP, jQuery cannot determine this value on its own, and you cannot hardcode the URL in your jQuery code and expect anyone else to use your plugin on their site. If the page is from the administration area, WordPress sets the correct URL in the global JavaScript variable ajaxurl. For a page from the public area, you will need to establish the correct URL yourself and pass it to jQuery using [`wp_localize_script()`](https://developer.wordpress.org/reference/functions/wp_localize_script/). This will be covered in more detail in the [PHP section](https://developer.wordpress.org/plugins/javascript/enqueuing/ "Server Side PHP and Enqueuing"). For now just know that the URL that will work for both the front and back end is available as a property of a global object that you will define in the PHP segment. In jQuery it is referenced like so:
 -->
WordPress の AJAX リクエストはすべて `wp-admin/admin-ajax.php` に送られなければなりません。正しい完全な URL は PHP から取得する必要があります。jQuery は、この値を独自に決定できませんし、jQuery のコードに URL をハードコーディングして他の人がそのプラグインを自分のサイトで使えるようにもできません。ページが管理エリアのものであれば、WordPress は、グローバル JavaScript 変数 ajaxurl に正しい URL を設定します。公開エリアのページの場合は、正しい URL を自分で設定し、[`wp_localize_script()`](https://developer.wordpress.org/reference/functions/wp_localize_script/) を使って jQuery に渡す必要があります。これについては [PHP 項](https://developer.wordpress.org/plugins/javascript/enqueuing/ "Server Side PHP and Enqueuing") で詳しく説明します。今のところ、フロントエンドとバックエンドの両方で動作する URL は、PHP セグメントで定義するグローバルオブジェクトのプロパティとして利用可能であることだけ知っておいてください。jQuery では、このように参照します:

```
my_ajax_obj.ajax_url
```

<!-- 
### Data
 -->
### データ

<!-- 
All data that needs to be sent to the server is included in the data array. Besides any data needed by your app, you must send an action parameter. For requests that could result in a change to the database you need to send a nonce so the server knows the request came from a legitimate source. Our example data array provided to the `.post()` method looks like this:
 -->
サーバーに送信する必要のあるデータは、すべてデータ配列に含まれます。アプリが必要とするデータのほかに、アクションパラメータを送信する必要があります。データベースの変更になり得るリクエストに対しては、リクエストが正当なソースからのものであることをサーバーに知らせるため、nonce を送る必要があります。`.post()` メソッドに渡すデータ配列の例は次のようになります:

```
{
  _ajax_nonce: my_ajax_obj.nonce, // nonce
  action: "my_tag_count", // action
  title: this.value // data
}
```

<!-- 
Each component is explained below.
 -->
各コンポーネントの説明は、以下の通りです。

### Nonce

<!-- 
[Nonce](https://developer.wordpress.org/apis/security/nonces/) is a portmanteau of "Number used ONCE". It is essentially a unique serial number assigned to each instance of any form served. The nonce is established with PHP script and passed to jQuery the same way the URL was, as a property in a global object. In this case it is referenced as my\_ajax\_obj.nonce.
 -->
[Nonce](https://developer.wordpress.org/apis/security/nonces/) は、「Number used ONCE」の造語です。基本的には、提供されるフォームの各インスタンスに割り当てられる、一意のシリアル番号です。nonce は、PHP スクリプトで確立され、URL と同じようにグローバルオブジェクトのプロパティとして、jQuery に渡されます。このケースでは、my\_ajax\_obj.nonce として参照されます。

<!-- 
[info]A true nonce needs to be refreshed every time it is used so the next AJAX call has a new, unused nonce to send as verification. As it happens, the WordPress nonce implementation is not a true nonce. The same nonce can be used as many times as necessary in a 24 hour period, unless you logout. Generating a nonce with the same seed phrase will always yield the same number for a 12 hour period after which a new number will finally be generated.
 -->
[info]真の nonce は、それが使用されるたびにリフレッシュされる必要があるので、次の AJAX 呼び出しは、検証として送信する新しい、未使用の nonce を持っています。たまたま、WordPress の nonce 実装は真の nonce ではありません。同じ nonce は、ログアウトしない限り、24時間以内に何度でも使用できます。同じシードフレーズで nonce を生成すると、12時間の間は常に同じ番号が生成され、その後、最終的に新しい番号が生成されます。

<!-- 
If your app needs serious security, implement a true nonce system where the server sends a new, fresh nonce in response to an Ajax request for the script to use to verify the next request.[/info]
 -->
もしあなたのアプリが強固なセキュリティを必要とするのであれば、サーバーが Ajax リクエストに応答して新しい nonce を送信し、スクリプトが次のリクエストを検証するために使用する、真の nonce システムを実装してください。[/info]

<!-- 
It's easiest if you key this nonce value to \_ajax\_nonce. You can use a different key if it's coordinated with the PHP code verifying the nonce, but it's easier to just use the default value and not worry about coordination. Here is the way the declaration of this key-value pair appears:
 -->
一番簡単なのは、この nonce の値を \_ajax\_nonce にキー設定することです。nonce を検証する PHP のコードと調整すれば、別のキーを使うこともできますが、デフォルト値を使用するほうが簡単で、調整の心配をする必要はありません。以下は、このキー・値ペアの宣言の表示方法です:

```
_ajax_nonce: my_ajax_obj.nonce
```
<!-- 
### Action
 -->
### 動作

<!-- 
All WordPress AJAX requests must include an action argument in the data. This value is an arbitrary string that is used in part to construct an action tag you use to hook your AJAX handler code. It's useful for this value to be a very brief description of the AJAX call's purpose. Unsurprisingly, the key for this value is _‘action'_. In this example, we will use `my_tag_count` as our action value. The declaration of this key-value pair looks like this:
 -->
WordPress のすべての AJAX リクエストは、データに action 引数を含める必要があります。この値は任意の文字列で、AJAX ハンドラコードをフックするために使用する、アクションタグの構築に使用されます。この値は、AJAX コールの目的を非常に簡潔に記述するのに便利です。当然、この値のキーは _‘action'_ です。この例では、`my_tag_count` をアクションの値として使います。このキー・値ペアの宣言は、次のようになります:

```
action: "my_tag_count"
```

<!-- 
Any other data the server needs to do its task is also included in this array. If there are a lot of fields to transmit, there are two common formats to combine data fields into a single string for more convenient transmission, XML and JSON. Using these formats is optional, but whatever you do does need to be coordinated with the PHP script on the server side. More information on these formats is available in the following Callback section. It is more common to receive data in this format than to send it, but it can work both ways.
 -->
サーバーがタスクを実行するために必要なその他のデータも、この配列に含まれます。送信するフィールドの数が多い場合は、データフィールドをひとつの文字列にまとめて、送信しやすくするためのフォーマットとして、XML および JSON の2つが一般的です。これらのフォーマットを使用するかどうかは任意ですが、使用する場合はサーバーサイドの PHP スクリプトと調整する必要があります。これらのフォーマットについての詳細は、以降のコールバック項を参照ください。このフォーマットでデータを送信するよりも受信するほうが一般的ですが、どちらでも使用できます。

<!-- 
In our example, the server only needs one value, a single string for the selected book title, so we will use the key _‘title'_. In jQuery, the object that fired the event is always contained in the variable this. Accordingly, the value of the selected element is this.value. Our declaration of this key-value pair appears like so:
 -->
この例では、サーバーは1つの値、つまり選択された本のタイトルを表す1つの文字列だけが必要ですので、キー _‘title'_ を使います。jQuery では、イベントを発生させたオブジェクトは、常に変数 this に含まれます。よって、選択された要素の値は this.value となります。このキー・値ペアの宣言は次のようになります:

```
title: this.value
```

<!-- 
### Callback
 -->
### コールバック

<!-- 
The callback handler is the function to execute when a response comes back from the server after the request is made. Once again, we usually see an anonymous function here. The function is passed one parameter, the server response. The response could be anything from a yes or no to a huge XML database. JSON formatted data is also a useful format for data. The response is not even required. If there is none, then no callback need be specified. In the interest of UX, it's always a good idea to let the user know what happened to any request, so it is recommended to always respond and provide some indication that something happened.
 -->
コールバックハンドラは、リクエスト後にサーバーからレスポンスが返ってきたときに実行する関数です。繰り返しますが、通常はここで無名関数を使用します。この関数には1つのパラメータ、サーバー・レスポンス、が渡されます。レスポンスは、YES か NO かといったものから、巨大な XML データベースまで何でもあり得ます。JSON フォーマットのデータも、データのフォーマットとしては便利です。レスポンスは必須ではありません。もし何もなければ、コールバックを指定する必要はありません。UX の観点からは、どのようなリクエストに対しても、何が起こったかをユーザーに知らせることは常に良いことですので、常にレスポンスを返し、何かが起こったことを示す何らかの表示をすることを推奨します。

<!-- 
In our example, we replace the current text following the radio input with the server response, which includes the number of posts tagged by the book title. Here is our anonymous callback function:
 -->
この例では、ラジオボタン横の現在のテキストを、本のタイトルでタグ付けされた投稿の数を含むサーバーレスポンスで置き換えています。これが匿名コールバック関数です:

```
function( data ) {
  this2.nextSibling.remove();
  $( this2 ).after( data );
}
```

<!-- 
`data` contains the entire server response. Earlier we assigned to `this2` the object that triggered the change event (referenced as `this`) with the line var `this2` = `this;`. This is because variable scope in closures only extends one level. By assigning `this2` in the event handler (the part that initially just contained `/* do stuff */`), we are able to use it in the callback where this would be out of scope.
 -->
`data` は、サーバーのレスポンス全体を含みます。先程、行 var `this2` = `this;` で、変更イベントをトリガーしたオブジェクト (`this` として参照) を `this2` に代入しました。なぜなら、クロージャの変数スコープは、一段階しか拡張されないからです。イベント・ハンドラ (最初は `/* do stuff */` が入っていた部分) に `this2` を割り当てることで、これがスコープ外になるコールバックで使うことができます。

<!-- 
The server response can take on any form. Significant quantities of data should be encoded into a data stream for easier handling. XML and JSON are two common encoding schemes.
 -->
サーバーのレスポンスは、どのような形でもかまいません。大量のデータは、扱いやすいようにデータストリームにエンコードすべきです。XML と JSON が一般的なエンコード方式です。

#### XML

<!-- 
XML is the old data exchange format for AJAX. It is after all the ‘X' in AJAX. It continues to be a viable exchange format even though it can be difficult to work with using native PHP functions. Many PHP programmers prefer the JSON exchange format for that reason. If you do use XML, the parsing method depends on the browser being used. Use Microsoft.XMLDOM ActiveX for Internet Explorer and use DOMParser for everything else. Note that [Internet Explorer is no longer supported by WordPress](https://make.wordpress.org/core/2021/04/22/ie-11-support-phase-out-plan/) since 5.8 release.
 -->
XML は、AJAX のための古いデータ交換フォーマットです。つまり、AJAX の「X」です。PHP のネイティブ関数を使うのは難しいかもしれませんが、JSON は今でも有効な交換フォーマットです。そのため、多くの PHP プログラマーは JSON 交換フォーマットを好んでいます。XML を使用する場合、パース方法は使用するブラウザに依存します。Internet Explorer には Microsoft.XMLDOM ActiveX を使い、それ以外には DOMParser を使います。5.8リリース以降、[Internet Explorer は、WordPress では、最早サポートされていない](https://make.wordpress.org/core/2021/04/22/ie-11-support-phase-out-plan/)ことに注意してください。

#### JSON

<!-- 
JSON is often favored for its light weight and ease of use. You can actually parse JSON using `eval()`, but don't do that! The use of `eval()` carries significant security risks. Instead, use a dedicated parser, which is also faster. Use the global instance of the parser object `JSON`. To ensure that it is available, be sure it is enqueued with other scripts on the page. More information about enqueuing is included later in the [PHP section](https://developer.wordpress.org/plugins/javascript/ajax/#json "Page section").
 -->
JSON は軽量で使いやすいため、よく好まれています。`eval()` を使って JSON をパースもできるが、それはやめておきましょう ! `eval()` の使用は重大なセキュリティリスクを伴います。代わりに、より高速な専用のパーサーを使用します。パーサーオブジェクトのグローバルインスタンス `JSON` を使用します。JSON オブジェクトを確実に利用できるようにするには、ページ上の他のスクリプトと一緒にエンキューされていることを確認してください。エンキューに関する詳細は、[PHP 項](https://developer.wordpress.org/plugins/javascript/ajax/#json "Page section")の後半に記載されています。

<!-- 
#### Other
 -->
#### その他

<!-- 
As long as the data format is coordinated with the PHP handler, it can be any format you like, such as comma delimited, tab delimited, or any kind of structure that works for you.
 -->
データフォーマットが PHP ハンドラで調整されている限り、カンマ区切りやタブ区切りなど、どのようなフォーマットでもかまいません。

<!-- 
#### Client Side Summary
 -->
#### クライアント・サイドの概要

<!-- 
Now that we've added our callback as the final parameter for the $.post() function, we've completed our sample jQuery Ajax script. All the pieces put together look like this:
 -->
$.post() 関数の最後のパラメータにコールバックを追加して、jQuery Ajax スクリプトのサンプルは完成です。すべてのピースをまとめると、このようになります:

```
jQuery(document).ready(function($) {         //wrapper
  $(".pref").change(function() {          //event
    var this2 = this;                  //use in callback
    $.post(my_ajax_obj.ajax_url, {      //POST request
      _ajax_nonce: my_ajax_obj.nonce, //nonce
      action: "my_tag_count",         //action
      title: this.value               //data
      }, function(data) {            //callback
        this2.nextSibling.remove(); //remove current title
        $(this2).after(data);       //insert server response
      }
    );
  } );
} );
```

<!-- 
This script can either be output into a `block` on the web page or contained in its own file. This file can reside anywhere on the Internet, but most plugin developers place it in a `/js/` subfolder of the plugin's main folder. Unless you have reason to do otherwise, you may as well follow convention. For this example we will name our file `myjquery.js`.
 -->
このスクリプトは、Web ページの `block` に出力するか、独自のファイルに含めることができます。このファイルは、インターネット上のどこにでも置くことができますが、ほとんどのプラグイン開発者はプラグインのメインフォルダーのサブフォルダー `/js/` に置きます。そうしなければならない理由がない限り、慣例に従ったほうがよいでしょう。この例では、ファイル名 `myjquery.js` とします。
