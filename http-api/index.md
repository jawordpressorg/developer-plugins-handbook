# HTTP API

<!-- 
## Introduction
 -->
## はじめに

<!-- 
HTTP stands for Hypertext Transfer Protocol and is the foundational communication protocol for the entire Internet. Even if this is your first experience with HTTP it's likely that you probably understand more than you realize. At its most basic level, HTTP works like this:
 -->
HTTP は Hypertext Transfer Protocol の頭文字をとったもので、インターネット全体の基礎となる通信プロトコルです。これが HTTP を使う初めての経験であっても、おそらく自分が思っている以上に理解している可能性が高いことでしょう。最も基本的なレベルでは、HTTP は次のように動作します:

<!-- 
- "Hello server XYZ, may I please have file abc.html"
- "Well hello there little client, yes you may, here it is"
 -->
- 「こんにちはサーバー XYZ、ファイル abc.html をいただけますか ?」
- 「こんにちは、クライアントさん、はい、どうぞ」

<!-- 
There are many different methods to send HTTP requests in PHP. The purpose of the WordPress HTTP API is to support as many of those methods as possible and use the one that is the most suitable for the particular request.
 -->
PHP で HTTP リクエストを送信するには、さまざまな方法があります。WordPress HTTP API の目的は、これらのメソッドをできるだけ多くサポートし、特定のリクエストに最も適したものを使用することです。

<!-- 
The WordPress HTTP API can also be used to communicate and interact with other APIs like the Twitter API or the Google Maps API.
 -->
WordPress HTTP API は、Twitter API や Google Maps API のような他の API との通信やインタラクションにも使用できます。

<!-- 
## HTTP methods
 -->
## HTTP メソッド

<!-- 
HTTP has several methods, or verbs, that describe particular types of actions. Though a couple more exist, WordPress has pre-built functions for three of the most common. Whenever an HTTP request is made a method is also passed with it to help the server determine what kind of action the client is requesting.
 -->
HTTP には、特定のタイプの操作を表すいくつかのメソッドがあります。他にもいくつかありますが、WordPress には最も一般的な3つのメソッドに対応する関数が、あらかじめ組み込まれています。クライアントがどのような操作を要求しているのかをサーバーが判断しやすくするために、HTTP リクエストが行われるたびに、メソッドも一緒に渡されます。

### GET

<!-- 
GET is used to retrieve data. This is by far the most commonly used verb. Every time you view a website or pull data from an API you are seeing the result of a GET request. In fact your browser sent a GET request to the server you are reading this on and requested the data used to build this very article.
 -->
GET は、データの取得に使われます。これは圧倒的によく使われる動詞です。Web サイトを見たり、API からデータを取り出したりするたびに、あなたは GET リクエストの結果を見ています。実際、あなたのブラウザーは、あなたがこれを読んでいるサーバーに GET リクエストを送り、まさにこの記事を作成するために使われたデータを要求したのです。

### POST

<!-- 
POST is used to send data to the server for the server to act upon in some way. For example, a contact form. When you enter data into the form fields and click the submit button the browser takes the data and sends a POST request to the server with the text you entered into the form. From there the server will process the contact request.
 -->
POST は、サーバーが何らかの処理をするために、サーバーにデータを送信するために使用されます。たとえば、お問い合わせフォーム。フォーム・フィールドにデータを入力し、送信ボタンをクリックすると、ブラウザーはデータを受け取り、フォームに入力したテキストを含む POST リクエストをサーバーに送信します。そこからサーバーは、コンタクトリクエストを処理します。

### HEAD

<!-- 
HEAD is much less well known than the other two. HEAD is essentially the same as a GET request except that it does not retrieve the data, only information about the data. This data describes such things as when the data was last updated, whether the client should cache the data, what type the data is, etc. Modern browsers often send HEAD requests to pages you have previously visited to determine if there are any updates. If not, you may actually be seeing a previously downloaded copy of the page instead of using bandwidth needlessly pulling in the same copy.
 -->
HEAD は、他の2つに比べてあまり知られていません。HEAD は基本的に GET リクエストと同じですが、データを取得するのではなく、データに関する情報のみを取得します。このデータは、データが最後に更新されたのはいつか、クライアントがデータをキャッシュすべきかどうか、データのタイプは何か、などを記述します。モダンなブラウザーは、更新があるかどうかを判断するために、以前に訪れたページに HEAD リクエストを送信することがよくあります。もしそうでなければ、帯域幅を無駄に使って同じコピーを取り込む代わりに、以前にダウンロードしたページのコピーを実際に見ている可能性があります。

<!-- 
All good API clients utilize HEAD before performing a GET request to potentially save on bandwidth. Though it will require two separate HTTP requests if HEAD says there is new data, the data size with a GET request can be very large. Only using GET when HEAD says the data is new or should not be cached will help save on expensive bandwidth and load times.
 -->
すべての優れた API クライアントは、帯域幅を節約できる可能性があるため、GET リクエストを実行する前に HEAD を利用します。HTTP リクエストを2回に分けて行う必要がありますが、HEAD に新しいデータがあると書かれている場合、GET リクエストのデータサイズは非常に大きくなる可能性があります。HEAD がデータが新しい、あるいはキャッシュすべきでないと言っているときだけ GET を使えば、高価な帯域幅とロード時間を節約できます。

<!-- 
### Custom Methods
 -->
### カスタム・メソッド

<!-- 
There are other HTTP methods, such as PUT, DELETE, TRACE, and CONNECT. These methods will not be covered in this article as there aren't pre-built methods to utilize them in WordPress, nor is it yet common for APIs to implement them.
 -->
HTTP メソッドには他にも PUT、DELETE、TRACE、CONNECT などがあります。WordPress にはこれらのメソッドを利用するためのメソッドが、あらかじめ用意されておらず、API に実装することもまだ一般的ではないため、この記事では取り上げません。

<!-- 
Depending upon how your server is configured you can also implement additional HTTP methods of your own. It is always a gamble to go outside of the standard methods, and places huge potential limitations on other developers creating clients to consume your site or API, however it is possible to utilize any method you wish with WordPress. We will briefly touch on how to do that in this article.
 -->
サーバーの設定によっては、独自の HTTP メソッドも追加実装できます。標準のメソッドから外れることは常にギャンブルであり、あなたのサイトや API を利用するクライアントを作成する他の開発者に大きな制限を与える可能性がありますが、WordPress ではどのようなメソッドでも利用できます。この記事では、その方法について簡単に触れます。

<!-- 
## Response codes
 -->
## レスポンスコード

<!-- 
HTTP utilizes both numeric and string response codes. Rather than go into a lengthy explanation of each, here are the standard response codes. You can define your own response codes when creating APIs, however unless you need to support specific types of responses it may be best to stick to the standard codes. Custom codes are usually in the 1xx ranges.
 -->
HTTP は、数値と文字列の両方のレスポンスコードを利用します。それぞれについて長々と説明するよりも、標準的なレスポンスコードを紹介しましょう。API を作成する際に独自のレスポンスコードも定義できますが、特定の種類のレスポンスをサポートする必要がない限り、標準のコードに従うのが最善でしょう。カスタムコードは、通常、1xx の範囲です。

<!-- 
### Code Classes
 -->
### コードクラス

<!-- 
The type of response can quickly be seen by the leftmost digit of the three digit codes.
 -->
レスポンスの種類は、3桁のコードの一番左の桁ですぐにわかります。

<!-- 
| Status Code | Description |
| --- | --- |
| 2xx | Request was successful |
| 3xx | Request was redirected to another URL |
| 4xx | Request failed due to client error. Usually invalid authentication or missing data |
| 5xx | Request failed due to a server error. Commonly missing or misconfigured configuration files |
 -->
| ステータスコード | 説明 |
| --- | --- |
| 2xx | リクエストは成功しました |
| 3xx | リクエストは別の URL にリダイレクトされました |
| 4xx | クライアント・エラーにより、リクエストは失敗しました。通常、認証が無効か、データが不足しています |
| 5xx | サーバー・エラーにより、リクエストは失敗しました。通常、コンフィギュレーションファイルが見つからないか、間違って設定されています |

<!-- 
**Common Codes**
 -->
**一般コード**

<!-- 
These are the most common codes you will encounter.
 -->
これらは、あなたが遭遇する最も一般的なコードです。

<!-- 
| Status Code | Description |
| --- | --- |
| 200 | OK – Request was successful |
| 301 | Resource was moved permanently |
| 302 | Resource was moved temporarily |
| 403 | Forbidden – Usually due to an invalid authentication |
| 404 | Resource not found |
| 500 | Internal server error |
| 503 | Service unavailable |
 -->
| ステータスコード | 説明 |
| --- | --- |
| 200 | OK – リクエストは、成功しました |
| 301 | リソースは、恒久的に移動されました |
| 302 | リソースは、一時的に移動されました |
| 403 | 禁止 – 通常は、無効な認証が原因です |
| 404 | リソースは、見つかりません |
| 500 | 内部サーバー・エラー |
| 503 | サービスは、利用できません |

<!-- 
## GETting data from an API
 -->
## API からデータの GET

<!-- 
[GitHub](https://github.com/) provides an excellent API that does not require app registration for many public aspects, so to demonstrate some of these methods, examples will target the GitHub API.
 -->
[GitHub](https://github.com/) は、多くのパブリックな側面に対してアプリケーションの登録を必要としない優れた API を提供している。そこで、これらのメソッドのいくつかを示すために、例では GitHub API をターゲットにします。

<!-- 
GETting data is made incredibly simple in WordPress through the [`wp_remote_get()`](https://developer.wordpress.org/reference/functions/wp_remote_get/) function. This function takes the following two arguments:
 -->
WordPress では、[`wp_remote_get()`](https://developer.wordpress.org/reference/functions/wp_remote_get/) 関数によってデータの GET が驚くほど簡単になります。この関数は、以下の2つの引数を取ります:

<!-- 
1. `$url` – Resource to retrieve data from. This must be in a standard HTTP format.
2. `$args` – OPTIONAL – You may pass an array of arguments in here to alter behavior and headers, such as cookies, follow redirects, etc.
 -->
1. `$url` – データを取得するリソースです。これは標準的な HTTP フォーマットでなければなりません。
2. `$args` – 任意 – ここに引数の配列を渡して、Cookie やフォローリダイレクトなどの動作やヘッダーを変更できます。

<!-- 
The following defaults are assumed, though they can be changed via the $args parameter:
 -->
以下のデフォルトが想定されていますが、$args パラメータで変更できます:

<!-- 
- `method` – GET
- `timeout` – 5 – How long to wait before giving up
- `redirection` – 5 – How many times to follow redirects.
- `httpversion` – 1.0
- `blocking` – true – Should the rest of the page wait to finish loading until this operation is complete?
- `headers` – array()
- `body` – null
- `cookies` – array()

 -->
- `method` – GET
- `timeout` – 5 – ギブアップするまでの待ち時間
- `redirection` – 5 – リダイレクトを何回実行するか
- `httpversion` – 1.0
- `blocking` – true – この操作が完了するまで、ページの残りの部分の読み込みを待つべきか ?
- `headers` – array()
- `body` – null
- `cookies` – array()

<!-- 
Let's use the URL to a GitHub user account and see what sort of information we can get.
 -->
GitHub のユーザーアカウントの URL を使って、どんな情報が得られるか見てみましょう。

```
$response = wp_remote_get( 'https://api.github.com/users/blobaugh' );
```

<!-- 
`$response` will contain all the headers, content, and other meta data about our request.
 -->
`$response` は、リクエストに関するすべてのヘッダー、コンテンツ、その他のメタデータを含みます。

```
Array(
  [headers] => Array(
    [server] => nginx
    [date] => Fri, 05 Oct 2012 04:43:50 GMT
    [content-type] => application/json; charset=utf-8
    [connection] => close
    [status] => 200 OK
    [vary] => Accept
    [x-ratelimit-remaining] => 4988
    [content-length] => 594
    [last-modified] => Fri, 05 Oct 2012 04:39:58 GMT
    [etag] => "5d5e6f7a09462d6a2b473fb616a26d2a"
    [x-github-media-type] => github.beta
    [cache-control] => public, s-maxage=60, max-age=60
    [x-content-type-options] => nosniff
    [x-ratelimit-limit] => 5000
  )
  [body] => {"type":"User","login":"blobaugh","gravatar_id":"f25f324a47a1efdf7a745e0b2e3c878f","public_gists":1,"followers":22,"created_at":"2011-05-23T21:38:50Z","public_repos":31,"email":"ben@lobaugh.net","hireable":true,"blog":"http://ben.lobaugh.net","bio":null,"following":30,"name":"Ben Lobaugh","company":null,"avatar_url":"https://secure.gravatar.com/avatar/f25f324a47a1efdf7a745e0b2e3c878f?d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-user-420.png","id":806179,"html_url":"https://github.com/blobaugh","location":null,"url":"https://api.github.com/users/blobaugh"}
  [response] => Array(
    [preserved_text 5237511b45884ac6db1ff9d7e407f225 /] => 200
    [message] => OK
  )
  [cookies] => Array()
  [filename] =>
)
```

<!-- 
All of the same helper functions can be used on this function as with the previous two. The exception here being that HEAD never returns a body, so that element will always be empty.
 -->
この関数では、前の2つの関数と同じヘルパー関数を使うことができます。ここでの例外は、HEAD はボディを返さないので、その要素は常に空になるということです。

<!-- 
### GET the body you always wanted
 -->
### 望むボディの GET

<!-- 
Just the body can be retrieved using [`wp_remote_retrieve_body()`](https://developer.wordpress.org/reference/functions/wp_remote_retrieve_body/). This function takes just one parameter, the response from any of the other [`wp_remote_X`](https://developer.wordpress.org/?s=wp_remote_&post_type%5B%5D=wp-parser-function) functions where retrieve is not the next value.
 -->
ボディだけを取得するには、[`wp_remote_retrieve_body()`](https://developer.wordpress.org/reference/functions/wp_remote_retrieve_body/) を使用します。この関数はパラメータを1つだけ受け取ります。他の [`wp_remote_X`](https://developer.wordpress.org/?s=wp_remote_&post_type%5B%5D=wp-parser-function) 関数のうち、retrieve が次の値ではない関数からのレスポンスです。

```
$response = wp_remote_get( 'https://api.github.com/users/blobaugh' );
$body     = wp_remote_retrieve_body( $response );
```

<!-- 
Still using the GitHub resource from the previous example, `$body` will be.
 -->
先ほどの例の GitHub リソースをそのまま使って、`$body` はこうなります。

```
{"type":"User","login":"blobaugh","public_repos":31,"gravatar_id":"f25f324a47a1efdf7a745e0b2e3c878f","followers":22,"avatar_url":"https://secure.gravatar.com/avatar/f25f324a47a1efdf7a745e0b2e3c878f?d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-user-420.png","public_gists":1,"created_at":"2011-05-23T21:38:50Z","email":"ben@lobaugh.net","following":30,"name":"Ben Lobaugh","company":null,"hireable":true,"id":806179,"html_url":"https://github.com/blobaugh","blog":"http://ben.lobaugh.net","location":null,"bio":null,"url":"https://api.github.com/users/blobaugh"}
```

<!-- 
If you do not have any other operations to perform on the response other than getting the body you can reduce the code to one line with.
 -->
ボディを取得する以外にレスポンスに対して実行する操作がなければ、コードを1行に減らすことができます。

```
$body = wp_remote_retrieve_body( wp_remote_get( 'https://api.github.com/users/blobaugh' ) );
```

<!-- 
Many of these helper functions can be used on one line similarly.
 -->
これらのヘルパー関数の多くは、同様に1行で使うことができます。

<!-- 
### GET the response code
 -->
### レスポンスコードの GET

<!-- 
You may want to check the response code to ensure your retrieval was successful. This can be done via the [`wp_remote_retrieve_response_code()`](https://developer.wordpress.org/reference/functions/wp_remote_retrieve_response_code/) function:
 -->
検索が成功したことを確認するために、レスポンスコードをチェックしたくなるかもしれません。これは [`wp_remote_retrieve_response_code()`](https://developer.wordpress.org/reference/functions/wp_remote_retrieve_response_code/) 関数を介して行うことができます:

```
$response = wp_remote_get( 'https://api.github.com/users/blobaugh' );
$http_code = wp_remote_retrieve_response_code( $response );
```

<!-- 
If successful `$http_code` will contain `200`.
 -->
成功した場合、`$http_code` には `200` が格納されます。

<!-- 
### GET a specific header
 -->
### 特定ヘッダーの GET

<!-- 
If your desire is to retrieve a specific header, say last-modified, you can do so with [`wp_remote_retrieve_header()`](https://developer.wordpress.org/reference/functions/wp_remote_retrieve_header). This function takes two parameters.
 -->
特定のヘッダー、たとえば last-modified を取得したい場合は、[`wp_remote_retrieve_header()`](https://developer.wordpress.org/reference/functions/wp_remote_retrieve_header) を使用します。この関数は、2つのパラメータを受け取ります。

<!-- 
1. `$response` – The response from the get call.
2. `$header` – Name of the header to retrieve.
 -->
1. `$response` – get コールからのレスポンス。
2. `$header` – 取得するヘッダーの名前。

<!-- 
To retrieve the last-modified header.
 -->
last-modified ヘッダーを取得するには。

```
$response      = wp_remote_get( 'https://api.github.com/users/blobaugh' );
$last_modified = wp_remote_retrieve_header( $response, 'last-modified' );
```

<!-- 
`$last_modified` will contain `[last-modified] => Fri, 05 Oct 2012 04:39:58 GMT`
 -->
`$last_modified` には `[last-modified] => Fri, 05 Oct 2012 04:39:58 GMT` が格納されます。

<!-- 
You can also retrieve all of the headers in an array with `wp_remote_retrieve_headers( $response )`.
 -->
また、`wp_remote_retrieve_headers( $response )` を使って、すべてのヘッダーを配列で取得できます。

<!-- 
### GET using basic authentication
 -->
### ベーシック認証を使用した GET

<!-- 
APIs that are secured more provide one or more of many different types of authentication. A common, though not highly secure, authentication method is HTTP Basic Authentication. It can be used in WordPress by passing ‘Authorization' to the second parameter of the [`wp_remote_get()`](https://developer.wordpress.org/reference/functions/wp_remote_get/) function, as well as the other HTTP method functions.
 -->
セキュアな API は、異なるタイプの認証を1つ以上提供します。安全性は高くありませんが、一般的な認証方法は HTTP ベーシック認証です。WordPress では、他の HTTP メソッド関数と同様に、[`wp_remote_get()`](https://developer.wordpress.org/reference/functions/wp_remote_get/) 関数の第2パラメータに「Authorization」を渡すことで使用できます。

```
$args = array(
  'headers' => array(
    'Authorization' => 'Basic ' . base64_encode( YOUR_USERNAME . ':' . YOUR_PASSWORD )
  )
);
wp_remote_get( $url, $args );
```

<!-- 
## POSTing data to an API
 -->
## API にデータを POST

<!-- 
The same helper methods ([`wp_remote_retrieve_body()`](https://developer.wordpress.org/reference/functions/wp_remote_retrieve_body/), etc.) are available for all of the HTTP method calls, and utilized in the same fashion.
 -->
同じヘルパーメソッド ([`wp_remote_retrieve_body()`](https://developer.wordpress.org/reference/functions/wp_remote_retrieve_body/) など) がすべての HTTP メソッド呼び出しで利用可能で、同じように利用します。

<!-- 
POSTing data is done using the [`wp_remote_post()`](https://developer.wordpress.org/reference/functions/wp_remote_post/) function, and takes exactly the same parameters as [`wp_remote_get()`](https://developer.wordpress.org/reference/functions/wp_remote_get/). It should be noted here that you are required to pass in ALL of the elements in the array for the second parameter. The Codex provides the default acceptable values. You only need to care right now about the data you are sending so the other values will be defaulted.
 -->
データの POST は [`wp_remote_post()`](https://developer.wordpress.org/reference/functions/wp_remote_post/) 関数を使って行われ、[`wp_remote_get()`](https://developer.wordpress.org/reference/functions/wp_remote_get/) とまったく同じパラメータを取ります。ここで注意しなければならないのは、2番目のパラメータには配列のすべての要素を渡す必要があるということです。Codex にはデフォルトの許容値が記載されています。今は送信するデータにだけ気を付ければいいので、他の値はデフォルトに設定します。

<!-- 
To send data to the server you will need to build an associative array of data. This data will be assigned to the `'body'` value. From the server side of things the value will appear in the `$_POST` variable as you would expect. i.e. if `body => array( 'myvar' => 5 )` on the server `$_POST['myvar'] = 5`.
 -->
サーバーにデータを送信するには、データの連想配列を作成する必要があります。このデータは `'body'` 値に割り当てられます。サーバーサイドから見ると、値は期待通りに変数 `$_POST` に表示されます。つまり、サーバーで `body => array( 'myvar' => 5 )` の場合、`$_POST['myvar'] = 5` となります。

<!-- 
Because GitHub does not allow POSTing to the API used in the previous example, this example will pretend that it does. Typically if you want to POST data to an API you will need to contact the maintainers of the API and get an API key or some other form of authentication token. This simply proves that your application is allowed to manipulate data on the API the same way logging into a website as a user does to the website.
 -->
GitHub では先の例で使用した API への POST は許可されていないので、この例では許可されていることにします。通常、API にデータを POST したい場合は API のメンテナーに連絡して API キーや何らかの認証トークンを取得する必要があります。これはただ、あなたのアプリケーションが API 上でデータを操作することを許可されていることを証明するだけであり、ユーザーとして Web サイトにログインするのと同じことです。

<!-- 
Lets assume we are submitting a contact form with the following fields: name, email, subject, comment. To setup the body we do the following:
 -->
名前、E メール、主題、コメントというフィールドを持つコンタクトフォームを送信すると仮定しましょう。ボディを構築するには、次のようにします:

```
$body = array(
  'name'    => 'Jane Smith',
  'email'   => 'some@email.com',
  'subject' => 'Checkout this API stuff',
  'comment' => 'I just read a great tutorial. You gotta check it out!',
);
```

<!-- 
Now we need to set up the rest of the values that will be passed to the second parameter of [`wp_remote_post()`](https://developer.wordpress.org/reference/functions/wp_remote_post/).
 -->
次に、[`wp_remote_post()`](https://developer.wordpress.org/reference/functions/wp_remote_post/) の2番目のパラメータに渡す残りの値を設定する必要があります。

```
$args = array(
  'body'        => $body,
  'timeout'     => '5',
  'redirection' => '5',
  'httpversion' => '1.0',
  'blocking'    => true,
  'headers'     => array(),
  'cookies'     => array(),
);
```

<!-- 
Then of course to make the call.
 -->
そして、もちろん、コールします。

```
$response = wp_remote_post( 'https://example.com', $args );
```

<!-- 
## HEADing off bandwidth usage
 -->
## HEAD で帯域幅の使用量削減 

<!-- 
It can be pretty important, and sometimes required by the API, to check a resource status using HEAD before retrieving it. On high traffic APIs, GET is often limited to a number of requests per minute or hour. There is no need to even attempt a GET request unless the HEAD request shows that the data on the API has been updated.
 -->
リソースを取得する前に HEAD でリソースのステータスをチェックすることは非常に重要であり、API によって要求されることもあります。トラフィックの多い API では、GET は1分または1時間あたりのリクエスト回数を制限されることが多いです。HEAD リクエストが、API 上のデータが更新されたことを示さない限り、GET リクエストを試みる必要さえありません。

<!-- 
As mentioned previously, HEAD contains data on whether or not the data has been updated, if the data should be cached, when to expire the cached copy, and sometimes a rate limit on requests to the API.
 -->
前述したように、HEAD にはデータが更新されたかどうか、データをキャッシュすべきかどうか、キャッシュされたコピーをいつ失効させるか、時には API へのリクエストのレート制限などのデータが含まれています。

<!-- 
Going back to the GitHub example, here are few headers to watch out for. Most of these headers are standard, but you should always check the API docs to ensure you understand which headers are named what, and their purpose.
 -->
GitHub の例に戻って、気を付けなければならないヘッダーをいくつか挙げてみましょう。これらのヘッダーのほとんどは標準的なものですが、どのヘッダーがどのような名前なのか、またその目的は何なのかを理解するために API のドキュメントを常にチェックするようにしましょう。

<!-- 
- `x-ratelimit-limit` – Number of requests allowed in a time period.
- `x-ratelimit-remaining` – Number of remaining available requests in time period.
- `content-length` – How large the content is in bytes. Can be useful to warn the user if the content is fairly large.
- `last-modified` – When the resource was last modified. Highly useful to caching tools.
- `cache-control` – How should the client handle caching.
 -->
- `x-ratelimit-limit` – 時間内に許可されるリクエスト数。
- `x-ratelimit-remaining` – 時間内に利用可能な残りのリクエスト数。
- `content-length` – コンテンツのバイト数。コンテンツがかなり大きい場合、ユーザーに警告するのに便利。
- `last-modified` – リソースの最終更新の日時。キャッシュツールに非常に有用。
- `cache-control` – クライアントは、どのようにキャッシュを扱うべきか。

<!-- 
The following will check the HEAD value of my GitHub user account:
 -->
以下は、自分の GitHub ユーザーアカウントの HEAD 値をチェックするものです:

```
$response = wp_remote_head( 'https://api.github.com/users/blobaugh' );
```

<!-- 
`$response` should look similar to
 -->
`$response` は、次のようになるはずです。

```
Array(
  [headers] => Array(
    [server] => nginx
    [date] => Fri, 05 Oct 2012 05:21:26 GMT
    [content-type] => application/json; charset=utf-8
    [connection] => close
    [status] => 200 OK
    [vary] => Accept
    [x-ratelimit-remaining] => 4982
    [content-length] => 594
    [last-modified] => Fri, 05 Oct 2012 04:39:58 GMT
    [etag] => "5d5e6f7a09462d6a2b473fb616a26d2a"
    [x-github-media-type] => github.beta
    [cache-control] => public, s-maxage=60, max-age=60
    [x-content-type-options] => nosniff
    [x-ratelimit-limit] => 5000
  )
  [body] =>
  [response] => Array(
    [preserved_text 39a8515bd2dce2aa06ee8a2a6656b1de /] => 200
    [message] => OK
  )
  [cookies] => Array(
  )
  [filename] =>
)
```

<!-- 
All of the same helper functions can be used on this function as with the previous two. The exception here being that HEAD never returns a body, so that element will always be empty.
 -->
この関数では、前の2つの関数と同じヘルパー関数を使うことができます。ここでの例外は、HEAD はボディを返さないので、その要素は常に空になるということです。

<!-- 
## Make any sort of request
 -->
## あらゆる要求をする

<!-- 
If you need to make a request using an HTTP method that is not supported by any of the above functions do not panic. The great people developing WordPress already thought of that and lovingly provided [`wp_remote_request()`](https://developer.wordpress.org/reference/functions/wp_remote_request/). This function takes the same two parameters as [`wp_remote_get()`](https://developer.wordpress.org/reference/functions/wp_remote_get/), and allows you to specify the HTTP method as well. What data you need to pass along is up to your method.
 -->
上記のどの関数でもサポートされていない HTTP メソッドを使用してリクエストを行う必要がある場合でも、パニックになる必要はありません。WordPress を開発している偉大な人々はすでにそのことを考え、愛情を持って [`wp_remote_request()`](https://developer.wordpress.org/reference/functions/wp_remote_request/) を提供してくれました。この関数は [`wp_remote_get()`](https://developer.wordpress.org/reference/functions/wp_remote_get/) と同じ2つのパラメータを受け取り、HTTP メソッドも指定できます。どのようなデータを渡すかはメソッド次第です。

<!-- 
To send a DELETE method example you may have something similar to the following:
 -->
DELETE メソッドを送信する例としては、以下のようなものがあります:

```
$args     = array(
  'method' => 'DELETE',
);
$response = wp_remote_request( 'http://some-api.com/object/to/delete', $args );
```

<!-- 
## Introduction to caching
 -->
## キャッシング概要

<!-- 
Caching is a practice whereby commonly used objects or objects requiring significant time to build are saved into a fast object store for quick retrieval on later requests. This prevents the need to spend the time fetching and building the object again. Caching is a vast subject that is part of website optimization and could go into an entire series of articles by itself. What follows is just an introduction to caching and a simple yet effective way to quickly setup a cache for API responses.
 -->
キャッシングとは、よく使われるオブジェクトや、構築に時間がかかるオブジェクトを、高速なオブジェクト・ストアに保存し、後のリクエストですばやく取り出せるようにする手法です。これにより、オブジェクトの取得と構築に再度時間を費やす必要がなくなります。キャッシングは、Web サイトの最適化の一部であり、それだけで一連の記事を書くことができるほど膨大なテーマです。以下は、キャッシュの概要と、API レスポンスのキャッシュをすばやく構築するシンプルかつ効果的な方法です。

<!-- 
Why should you cache API responses? Well, the big elephant in the room is because external APIs slow down your site. Many consultants will tell you tapping into external APIs will improve the performance of your website by reducing the amount of connections and processing it performs, as well as costly bandwidth, but sometimes this is simply not true.
 -->
なぜ API のレスポンスをキャッシュする必要があるのでしょう ? そう、部屋の中の大きな象は、外部 API があなたのサイトを遅くするからです。多くのコンサルタントは、外部 API を利用することで、接続や処理の量を減らし、コストのかかる帯域幅を削減することで、Web サイトのパフォーマンスを向上させることができると言うだろうが、時には真ではありません。

<!-- 
It is a fine balancing act between the speed your server can send data and the amount of time it takes for the remote server to process a request, build the data, and send it back. The second glaring aspect is that many APIs have a limited number of requests in a time period, and possibly a limit to the number of connections by an application at once. Caching helps solve these dilemmas by placing a copy of the data on your server until it needs to be refreshed.
 -->
あなたのサーバーがデータを送信できる速度と、リモートサーバーがリクエストを処理し、データを構築し、それを送り返すのにかかる時間との間で、絶妙なバランスをとる必要があります。2つ目の顕著な側面は、多くの API には一定期間内のリクエスト数に制限があり、場合によっては一度に接続できるアプリケーションの数に制限があることです。キャッシングは、リフレッシュが必要になるまでサーバーにデータのコピーを置くことで、これらのジレンマを解決するのに役立ちます。

<!-- 
## When should you cache?
 -->
## いつキャッシュすべきか ?

<!-- 
The snap answer to this is **always**, but again there are times when you should not. If you are dealing with real time data or the API specifically says not to cache in the headers you may not want to cache, but for all other situations it is generally a good idea to cache any resources retrieved from an API.
 -->
これに対する簡単な答えは**常に**だが、やはりキャッシュすべきではない場合もあります。リアルタイムデータを扱っている場合や、API がヘッダーにキャッシュするなと明記している場合は、キャッシュしたくないかもしれませんが、それ以外の状況では、API から取得したリソースをキャッシュするのが一般的には良い考えです。

## WordPress Transients

<!-- 
WordPress Transients provide a convenient way to store and use cached objects. Transients live for a specified amount of time, or until you need them to expire when a resource from the API has been updated. Using the transient functionality in WordPress may be the easiest to use caching system you ever encounter. There are only three functions to do all the heavy lifting for you.
 -->
WordPress Transients は、キャッシュされたオブジェクトを保存して使用する便利な方法です。Transient は、指定された時間、または API からのリソースが更新されたときに失効させる必要があるまで有効です。WordPress の Transient 機能を使えば、今まで出会ったキャッシュシステムの中で最も簡単に使えるかもしれません。たった3つの関数が、あなたのために力仕事をしてくれるのです。

<!-- 
### Cache an object ( Set a transient )
 -->
### オブジェクトのキャッシュ (Transient の設定)

<!-- 
Caching an object is done with the [`set_transient()`](https://developer.wordpress.org/reference/functions/set_transient/) function. This function takes the following three parameters:
 -->
オブジェクトのキャッシングは、[`set_transient()`](https://developer.wordpress.org/reference/functions/set_transient/) 関数で行います。この関数は以下の3つのパラメータを取ります:

<!-- 
1. `$transient` – Name of the transient for future reference.
2. `$value` – Value of the transient.
3. `$expiration` – How many seconds from saving the transient until it expires.
 -->
1. `$transient` – 今後の参照のための Transient の名前。
2. `$value` – Transient の値。
3. `$expiration` – Transient を保存してから有効期限が切れるまでの秒数。

<!-- 
An example of caching the GitHub user information response from above for one hour would be
 -->
GitHub のユーザー情報のレスポンスを一時間キャッシングする例は次のようになります。

```
$response = wp_remote_get( 'https://api.github.com/users/blobaugh' );
set_transient( 'prefix_github_userinfo', $response, 60 * 60 );
```

<!-- 
### Get a cached object ( Get a transient )
 -->
### キャッシュされたオブジェクトの取得 (Transient の取得)

<!-- 
Getting a cached object is quite a bit more complex than setting a transient. You need to request the transient, but then you also need to check to see if that transient has expired and if so fetch updated data. Usually the `set_transient()` call is made inside of the `get_transient()` call. Here is an example of getting the transient data for the GitHub user profile:
 -->
キャッシュされたオブジェクトを取得するのは、Transient を設定するよりもかなり複雑です。Transient をリクエストする必要がありますが、その Transient が期限切れかどうかをチェックし、期限切れであれば更新されたデータを取得する必要があります。通常、`set_transient()` コールは `get_transient()` コールの内部で行われます。ここでは、GitHub のユーザープロファイルの Transient データを取得する例を示します:

```
$github_userinfo = get_transient( 'prefix_github_userinfo' );
if ( false === $github_userinfo ) {
  // Transient expired, refresh the data
  $response = wp_remote_get( 'https://api.github.com/users/blobaugh' );
  set_transient( 'prefix_github_userinfo', $response, HOUR_IN_SECONDS );
}
// Use $github_userinfo as you will
```

<!-- 
## Delete a cached object (Delete a transient)
 -->
## キャッシュされたオブジェクトの削除 (Transient の削除)

<!-- 
Deleting a cached object is the easiest of all the transient functions, simply pass it a parameter of the name of the transient and you are done.
 -->
キャッシュされたオブジェクトの削除は、Transient 関数の中で最も簡単で、Transient 名のパラメータを渡すだけで完了します。

<!-- 
To remove the Github user info:
 -->
GitHub のユーザー情報を削除するには:

```
delete_transient( 'blobaugh_github_userinfo' );
```

<!-- 
More information on transients can be found [here](https://developer.wordpress.org/apis/transients/).
 -->
Transient についての詳細は、[こちら](https://developer.wordpress.org/apis/transients/) を参照してください。
