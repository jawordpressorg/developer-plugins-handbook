<!--
# Requests
-->

# リクエスト

<!--
## Overview
-->

## 概要

<!--
The REST API is very simple in many ways. There is input, known as the request. The input is interpreted by the server and output is created. The output, is known as the response. In some ways, you can think of a request to the WordPress REST API as a set of directions or instructions that should be carried out and interpreted by the API. By default, the WordPress REST API is intended to use HTTP requests as its request medium. HTTP is the foundation for communication of data over the internet, which makes the WordPress REST API a very far reaching API. Requests in the API utilize a lot of the different aspects present in HTTP requests like URIs, HTTP methods, headers, and parameters. The data structure of a request is conveniently handled by the `WP_REST_Request` class.
-->

REST API は、多くの点で非常にシンプルです。リクエストと呼ばれる入力があります。入力は、サーバーによって解釈され、出力が作成されます。出力は、レスポンスとして知られています。ある意味では、WordPress REST API へのリクエストは、API が実行し解釈すべき、一連の指示や命令と考えることができます。デフォルトでは、WordPress REST API は、リクエスト媒体として HTTP リクエストを使用するようになっています。HTTP は、インターネット上でのデータ通信の基盤であり、WordPress REST API を非常に広範囲に及ぶ API にしています。API におけるリクエストは、URI、HTTP メソッド、ヘッダー、パラメータなど、HTTP リクエストに存在するさまざまな側面を多く利用しています。リクエストのデータ構造は、クラス `WP_REST_Request` によって便利に処理されます。

<!--
## WP_REST_Request
-->

## WP_REST_Request

<!--
This class is one of the three main infrastructure classes introduced in WordPress 4.4. When an HTTP request is made to an endpoint of the API, the API will automatically create an instance of the `WP_REST_Request` class, matching the provided data. The response object is auto-generated in `WP_REST_Server`‘s `serve_request()` method. Once the request is created and authentication is checked, the request is dispatched and our endpoint callbacks begin to be fired. All of the data stored up in the `WP_REST_Request` object is passed into our callbacks for our registered endpoints. So both our `permissions_callback` and `callback` are called with the request object being passed in. This enables us to access the various request properties in our callbacks, so that we can tailor our responses to match the desired output.
-->

このクラスは WordPress 4.4で導入された3つの主要な基盤クラスのひとつです。API のエンドポイントに HTTP リクエストが送信されると、API は自動的にクラス `WP_REST_Request` のインスタンスを生成し、提供されたデータと一致させます。レスポンス・オブジェクトは `WP_REST_Server` のメソッド `serve_request()` で自動生成されます。リクエストが作成され、認証がチェックされると、リクエストがディスパッチされ、エンドポイントのコールバックが開始されます。オブジェクト `WP_REST_Request` に格納されたデータはすべて、登録したエンドポイントのためのコールバックに渡されます。そのため、`permissions_callback` と `callback` の両方がリクエスト・オブジェクトが渡された状態で呼び出されます。これにより、コールバック内でさまざまなリクエスト・プロパティにアクセスできるようになるため、希望する出力に合わせてレスポンスを調整可能になります。

<!--
## Request Properties
-->

## リクエスト・プロパティ

<!--
Request objects have many different properties, each of which can be used in various ways. The main properties are the request method, route, headers, parameters and attributes. Let’s break each of these down into their role in a request. If you were to create a request object yourself it would look like this:
-->

リクエスト・オブジェクトにはさまざまなプロパティがあり、それぞれをさまざまな方法で使用できます。主なプロパティは、リクエスト・メソッド、ルート、ヘッダー、パラメータ、属性です。それぞれをリクエストにおける役割に分解してみましょう。リクエスト・オブジェクトを自分で作るとしたら、次のようになります:

```
$request = new WP_REST_Request( 'GET', '/my-namespace/v1/examples' );
```

<!--
In the above code sample we are only specifying that the request object method is `GET` and we should be matching the route `/my-namespace/v1/examples` which in the context of an entire URL would look like this: `https://ourawesomesite.com/wp-json/my-namepsace/v1/examples`. The method and route arguments for the `WP_REST_Request` constructor are used to map the request to the desired endpoint. If the request is made to an endpoint that is not registered then a helpful 404 error message is returned in the response. Let’s look at the various properties in more depth.
-->

上記のコード例では、リクエスト・オブジェクトのメソッドが `GET` であることだけを指定していて、ルート `/my-namespace/v1/examples` に一致させる必要があり、URL 全体のコンテキストでは次のようになります: `https://ourawesomesite.com/wp-json/my-namepsace/v1/examples`。コンストラクタ `WP_REST_Request` のメソッドとルートの引数は、リクエストを目的のエンドポイントにマップするために使われます。登録されていないエンドポイントに対して、リクエストが行われた場合は、レスポンスに役立つエラーメッセージ「404」が返されます。さまざまなプロパティを詳しく見ていきましょう。

<!--
### Method
-->

### メソッド

<!--
The method property of a request object by default matches the HTTP Request method. The method in most cases will be one of `GET`, `POST`, `PUT`, `DELETE`, `OPTIONS`, or `HEAD`. These methods will be used to match the various endpoints registered to a route. When the API finds a match for the method and route it will fire the callbacks for that endpoint.
-->

デフォルトでは、リクエスト・オブジェクトのプロパティ method は HTTP リクエスト・メソッドに一致します。ほとんどの場合、このメソッドは、`GET`、`POST`、`PUT`、`DELETE`、`OPTIONS`、`HEAD` のいずれかとなります。これらのメソッドは、ルートに登録されているさまざまなエンドポイントを一致させるために使用されます。API がメソッドとルートとの一致を見つけると、そのエンドポイント用のコールバックを起動します。

<!--
The following convention is a best practice for matching HTTP methods: `GET` for read only tasks, `POST` for creation, `PUT` for updating, and `DELETE` for deleting. The request method acts as an indicator for the expected functionality of your endpoints. When you make a `GET` request to a route, you should expect to be returned read only data.
-->

以下の規約は、HTTP メソッドのマッチングのベストプラクティスです: 読み取り専用には `GET`、作成には `POST`、更新には `PUT`、削除には `DELETE` です。リクエスト・メソッドは、エンドポイントに期待される機能の指標となります。ルートに対してリクエスト `GET` を行う場合、読み取り専用のデータが返されることを期待しなければなりません。

<!--
### Route
-->

### ルート

<!--
The route for a request, by default, will match the server environment variable for path info; `$_SERVER['PATH_INFO']`. When you make an HTTP request to a route of the WordPress REST API, the generated `WP_REST_Request` object will be made to match that path, which will hopefully then be matched to a valid endpoint. In short the route for a request is where you want to target your request in the API.
-->

リクエストに対するルートは、デフォルトでは、パス情報のサーバー環境変数 `$_SERVER['PATH_INFO']` に一致します。WordPress REST API のルートに HTTP リクエストを行うと、生成されたオブジェクト `WP_REST_Request` が (うまくいけば有効なエンドポイントに一致する) そのパスに一致します。要するに、リクエストに対するルートというのは、API の中でどこにリクエストを送りたいかということです。

<!--
If we had registered a books endpoint, using `GET`, it might live at `https://ourawesomesite.com/wp-json/my-namespace/v1/books`. If we went to that URL in our browser, we would see our collection of books represented in JSON. WordPress will automatically generate the request object for us and handle all of the routing to match endpoints. So since we don’t really have to worry about the routing ourselves understanding how to pass extra data we want in our requests is a much more important thing to understand.
-->

`GET` を使ってエンドポイント books を登録したとしたら、`https://ourawesomesite.com/wp-json/my-namespace/v1/books` にそれは存在するかもしれません。ブラウザでこの URL にアクセスすると、JSON で表現された books のコレクションが表示されます。WordPress は、自動的にリクエスト・オブジェクトを生成し、エンドポイントに一致するようにすべてのルーティングを処理します。したがって、ルーティングについて心配する必要はないので、リクエストに必要な追加のデータを渡す方法を理解することは、より重要なことなのです。

<!--
### Headers
-->

### ヘッダー

<!--
HTTP Request headers are simply just extra data about our HTTP request. Request headers can specify caching policy, what our request content is, where the request is coming from and many other things. Request headers do not necessarily interact with our endpoints directly, but the information in the headers helps WordPress know what to do. To pass in data that we want our endpoints to interact with we want to use parameters.
-->

HTTP リクエスト・ヘッダーは、HTTP リクエストに関する単なる追加データです。リクエスト・ヘッダーには、キャッシュポリシー、リクエストの内容、リクエストの送信元、その他多くのことを指定できます。リクエスト・ヘッダーは、必ずしもエンドポイントと直接やりとりするわけではありませんが、ヘッダーの情報は、WordPress が何をすべきかを知るのに役立ちます。エンドポイントとやりとりさせたいデータを渡すには、パラメータを使います。

<!--
### Parameters
-->

### パラメータ

<!--
When making requests to the WordPress REST API, most of the additional data passed in will take on the form of parameters. What are parameters? There are four different types in the context of the API. There are route parameters, query parameters, body parameters, and file parameters. Let’s take a look at each one a bit more in depth.
-->

WordPress REST API に対してリクエストを行う際、追加で渡されるデータのほとんどはパラメータの形を取ります。パラメータとは、何でしょうか ? API のコンテキストには、4つの異なるタイプがあります。ルート・パラメータ、クエリー・パラメータ、ボディ・パラメータ、ファイル・パラメータです。それぞれをもう少し詳しく見てみましょう。

<!--
#### URL Params
-->

#### URL パラメータ

<!--
URL parameters are automatically generated in a `WP_REST_Request` from the path variables in the requested route. What does that mean? Let’s look at this route, which grabs individual books by id: `/my-namespace/v1/books/(?P\d+)`. The odd looking `(?P\d+)` is a path variable. The name of the path variable is ‘`id`‘.
-->

URL パラメータは、リクエストされたルートのパス変数から `WP_REST_Request` で自動的に生成されます。これは何を意味するのでしょうか ? 個々の books を id で取得する、このルートを見てみましょう: `/my-namespace/v1/books/(?P\d+)`。奇妙に見える `(?P\d+)` は、パス変数です。パス変数の名前は「`id`」です。

<!--
If we were to make a request like `GET https://ourawesomesite.com/wp-json/my-namespace/v1/books/5`, `5` will become the value for our `id` path variable. The `WP_REST_Request` object will automatically take that path variable and store it as a URL parameter. Now inside of our endpoint callbacks we can interact with that URL parameter really easily. Let’s look at an example.
-->

`GET https://ourawesomesite.com/wp-json/my-namespace/v1/books/5` のようなリクエストをすると、`5` がパス変数 `id` の値になります。オブジェクト `WP_REST_Request` は、自動的にそのパス変数を受け取り、URL パラメータとして格納します。これで、エンドポイント・コールバック内で、URL パラメータととても簡単にやりとりできます。例を見てみましょう。

```
// Register our individual books endpoint.
function prefix_register_book_route() {
    register_rest_route( 'my-namespace/v1', '/books/(?P<id>\d+)', array(
        // Supported methods for this endpoint. WP_REST_Server::READABLE translates to GET.
        'methods' => WP_REST_Server::READABLE,
        // Register the callback for the endpoint.
        'callback' => 'prefix_get_book',
    ) );
}

add_action( 'rest_api_init', 'prefix_register_book_route' ); 

/**
 * Our registered endpoint callback. Notice how we are passing in $request as an argument.
 * By default, the WP_REST_Server will pass in the matched request object to our callback.
 *
 * @param WP_REST_Request $request The current matched request object.
 */
function prefix_get_book( $request ) {
    // Here we are accessing the path variable 'id' from the $request.
    $book = prefix_get_the_book( $request['id'] );
    return rest_ensure_response( $book );
}

// A simple function that grabs a book title from our books by ID.
function prefix_get_the_book( $id ) {
    $books = array(
        'Design Patterns',
        'Clean Code',
        'Refactoring',
        'Structure and Interpretation of Computer Programs',
    );

    $book = '';
    if ( isset( $books[ $id ] ) ) {
        // Grab the matching book.
        $book = $books[ $id ];
    } else {
        // Error handling.
        return new WP_Error( 'rest_not_found', esc_html__( 'The book does not exist', 'my-text-domain' ), array( 'status' => 404 ) );
    }

    return $book;
}
```

<!--
In the example above we see how path variables are stored as URL parameters in the request object. We can then access those parameters in our endpoint callbacks. The above example is a pretty common use case for using URL params. Adding too many path variables to a route can slow down the matching of routes and it can also over complicate registering endpoints, it is advised to use URL parameters sparingly. If we aren’t supposed to use parameters directly in our URL path, then we need another way to pass in extra information to our request. This is where query and body parameters come in, they will typically do most of the heavy lifting in your API.
-->

上の例では、パス変数が URL パラメータとしてリクエスト・オブジェクトに格納されていることが分かります。そして、エンドポイント・コールバックでそれらのパラメータにアクセスできます。上記の例は、URL パラメータを使用するためのかなり一般的なユースケースです。ルートにパス変数を追加しすぎると、ルートのマッチングが遅くなったり、エンドポイントの登録が複雑になりすぎたりするので、URL パラメータは控えめに使うことをおすすめします。URL パスで直接パラメータを使うことが想定されていないのであれば、リクエストに追加情報を渡す別の方法が必要です。ここがクエリー・パラメータとボディ・パラメータの出番で、これらは一般的に、API で重要な作業のほとんどを行います。

<!--
#### Query Params
-->

#### クエリー・パラメータ

<!--
Query parameters exist in the query string portion of a URI. The query string portion of a URI in `https://ourawesomesite.com/wp-json/my-namespace/v1/books?per_page=2&genre=fiction` is `?per_page=2&genre=fiction`. The query string is started by the ‘`?`‘ character, the different values within the query string are separated by the ‘`&`‘ character. We specified two parameters in our query string; `per_page` and `fiction`. In our endpoint we would want to grab only two books from the fiction genre. We could access those values in a callback like this: `$request['per_page']`, and `$request['genre']` ( assuming $request is the name of the argument we are using ). If you are familiar with PHP you have probably used query parameters in your web applications.
-->

クエリー・パラメータは、URI のクエリー文字列部分に存在します。`https://ourawesomesite.com/wp-json/my-namespace/v1/books?per_page=2&genre=fiction` における URI のクエリー文字列部分は `?per_page=2&genre=fiction` です。クエリー文字列は、文字「`?`」で始まり、クエリー文字列内の異なる値は、文字「`&`」で区切られます。クエリー文字列には、`per_page` と `fiction` の2つのパラメータを指定しました。私たちのエンドポイントでは、フィクション・ジャンルから2冊の本だけを取得したいと思います。このようなコールバックでこれらの値にアクセスできます: `$request['per_page']` と `$request['genre']` ($request が、使用する引数の名前であると仮定)。PHP に慣れている人なら、おそらく Web アプリケーションでクエリー・パラメータを使ったことがあるでしょう。

<!--
In PHP, the query parameters get stored in the superglobal `$_GET`. It is important to note that you should never directly access any superglobals or server variables in your endpoints. It is always best to work with what is provided by the `WP_REST_Request` class. Another common method for passing in variables to an endpoint is to use body parameters.
-->

PHP では、クエリー・パラメータは、スーパーグローバル `$_GET` に格納されます。注意すべき点は、エンドポイント内でスーパーグローバルやサーバー変数に、直接アクセスしてはいけないということです。クラス `WP_REST_Request` が提供するものを使用するのが常にベストです。エンドポイントに変数を渡すもうひとつの一般的な方法は、ボディ・パラメータを使用することです。

<!--
#### Body Params
-->

#### ボディ・パラメータ

<!--
Body parameters are key value pairs that are stored in the request body. If you have ever sent a `POST` request via a , through cURL, or some other method, then you have used body parameters. With body parameters you can pass them as different content types as well. The default `Content-Type` header for a `POST` request is `x-www-form-urlencoded`. When using `x-www-form-urlencoded`, the parameters are sent like a query string; `per_page=2&genre=fiction`. An HTML form, by default, will bundle up the various inputs and send a `POST` request matching the `x-www-form-urlencoded` pattern.
-->

ボディ・パラメータは、リクエスト・ボディに格納される KVP (キーと値のペア) です。これまでに cURL やその他の方法を使用して `POST` リクエストを送信したことがあれば、ボディ・パラメータを使ったことがあるはずです。ボディ・パラメータでは、異なるコンテンツタイプとして渡すこともできます。リクエスト `POST` に対するデフォルトのヘッダー `Content-Type` は、`x-www-form-urlencoded` です。`x-www-form-urlencoded` を使用する場合、パラメータはクエリー文字列のように送信されます; `per_page=2&genre=fiction`。デフォルトでは、HTML フォームは、さまざまな入力を束ね、パターン `x-www-form-urlencoded` に一致するリクエスト `POST` を送信します。

<!--
It is important to note that although the HTTP specification does not prohibit the use of sending body parameters in `GET` requests, it is encouraged that you do not use body parameters in a `GET` request. Body parameters can and should be used for `POST`, `PUT`, and `DELETE` requests.
-->

HTTP の仕様では `GET` リクエストでボディ・パラメータを送ることを禁止しているわけではありませんが、`GET` リクエストでボディ・パラメータを使わないことが推奨されています。ボディ・パラメータは `POST`、`PUT`、`DELETE` リクエストで使うことができますし、使うべきです。

<!--
#### File Params
-->

#### ファイル・パラメータ

<!--
File parameters in a `WP_REST_Request` object are stored when the request uses a special content type header; `multipart/form-data`. The file data can then be accessed from the request object using `$request->get_file_params()`. The file parameters are equivalent to the PHP superglobal: `$_FILES`. Remember, do not access the superglobals directly only use what the `WP_REST_Request` object provides.
-->

オブジェクト `WP_REST_Request` のファイル・パラメータは、リクエストが特別なコンテンツタイプ・ヘッダー `multipart/form-data` を使用する場合に格納されます。ファイルデータは、リクエストオブジェクトから `$request->get_file_params()` を使ってアクセスできます。ファイル・パラメータは PHP のスーパーグローバル `$_FILES` と同じです。スーパーグローバルに直接アクセスせず、オブジェクト `WP_REST_Request` が提供するものだけを使用することを忘れないでください。

<!--
In the endpoint callback we could use `wp_handle_upload()` to then add in the desired files to WordPress’s media uploads directory. The file parameters are only useful for dealing with file data and you should never use them for any other purpose.
-->

エンドポイント・コールバックでは、`wp_handle_upload()` を使用して、WordPress のメディアアップロード・ディレクトリに必要なファイルを追加できます。ファイル・パラメータは、ファイルデータを扱うときにのみ有効で、それ以外の目的では決して使ってはいけません。

<!--
### Attributes
-->

### 属性

<!--
`WP_REST_Request` also supports request attributes. The attributes of a request are the attributes registered to the match route. If we made a `GET` request to `my-namespace/v1/books`, and then we called `$request->get_attributes()` inside of our endpoint callback, we would be returned all of the registration options for the `my-namespace/v1/books` endpoint. If we made a `POST` request to the same route and our endpoint callback also returned `$request->get_attributes()`, we would receive a different set of endpoint options registered to the `POST` endpoint callback.
-->

`WP_REST_Request` は、リクエスト属性もサポートします。リクエストの属性は、一致ルートに登録されている属性です。`my-namespace/v1/books` に対して `GET` リクエストを行い、エンドポイント・コールバック内で `$request->get_attributes()` を呼び出すと、エンドポイント `my-namespace/v1/books` 用のすべての登録オプションが返されます。同じルートに対して `POST` リクエストを行い、エンドポイント・コールバックも `$request->get_attributes()` を返したとすると、エンドポイント・コールバック `POST` に登録されたエンドポイント・オプションの異なるセットを受け取ることになります。

<!--
In the attributes we will get a response containing supported methods, options, whether to show this endpoint in the index, a list of registered arguments for the endpoint, and our registered callbacks. It might look something like this:  
-->

属性には、サポートされているメソッド、オプション、このエンドポイントをインデックスに表示する否か、エンドポイント用に登録されている引数のリスト、そして登録されているコールバックが含まれるレスポンスを取得します。以下のようになります:  

```
{
  "methods": {
    "GET": true
  },
  "accept_json": false,
  "accept_raw": false,
  "show_in_index": true,
  "args": {
    "context": {
      "description": "Scope under which the request is made; determines fields present in response.",
      "type": "string",
      "sanitize_callback": "sanitize_key",
      "validate_callback": "rest_validate_request_arg",
      "enum": [
        "view",
        "embed",
        "edit"
      ],
      "default": "view"
    },
    "page": {
      "description": "Current page of the collection.",
      "type": "integer",
      "default": 1,
      "sanitize_callback": "absint",
      "validate_callback": "rest_validate_request_arg",
      "minimum": 1
    },
    "per_page": {
      "description": "Maximum number of items to be returned in result set.",
      "type": "integer",
      "default": 10,
      "minimum": 1,
      "maximum": 100,
      "sanitize_callback": "absint",
      "validate_callback": "rest_validate_request_arg"
    },
    "search": {
      "description": "Limit results to those matching a string.",
      "type": "string",
      "sanitize_callback": "sanitize_text_field",
      "validate_callback": "rest_validate_request_arg"
    },
    "after": {
      "description": "Limit response to resources published after a given ISO8601 compliant date.",
      "type": "string",
      "format": "date-time",
      "validate_callback": "rest_validate_request_arg"
    },
    "author": {
      "description": "Limit result set to posts assigned to specific authors.",
      "type": "array",
      "default": [],
      "sanitize_callback": "wp_parse_id_list",
      "validate_callback": "rest_validate_request_arg"
    },
    "author_exclude": {
      "description": "Ensure result set excludes posts assigned to specific authors.",
      "type": "array",
      "default": [],
      "sanitize_callback": "wp_parse_id_list",
      "validate_callback": "rest_validate_request_arg"
    },
    "before": {
      "description": "Limit response to resources published before a given ISO8601 compliant date.",
      "type": "string",
      "format": "date-time",
      "validate_callback": "rest_validate_request_arg"
    },
    "exclude": {
      "description": "Ensure result set excludes specific ids.",
      "type": "array",
      "default": [],
      "sanitize_callback": "wp_parse_id_list"
    },
    "include": {
      "description": "Limit result set to specific ids.",
      "type": "array",
      "default": [],
      "sanitize_callback": "wp_parse_id_list"
    },
    "offset": {
      "description": "Offset the result set by a specific number of items.",
      "type": "integer",
      "sanitize_callback": "absint",
      "validate_callback": "rest_validate_request_arg"
    },
    "order": {
      "description": "Order sort attribute ascending or descending.",
      "type": "string",
      "default": "desc",
      "enum": [
        "asc",
        "desc"
      ],
      "validate_callback": "rest_validate_request_arg"
    },
    "orderby": {
      "description": "Sort collection by object attribute.",
      "type": "string",
      "default": "date",
      "enum": [
        "date",
        "relevance",
        "id",
        "include",
        "title",
        "slug"
      ],
      "validate_callback": "rest_validate_request_arg"
    },
    "slug": {
      "description": "Limit result set to posts with a specific slug.",
      "type": "string",
      "validate_callback": "rest_validate_request_arg"
    },
    "status": {
      "default": "publish",
      "description": "Limit result set to posts assigned a specific status; can be comma-delimited list of status types.",
      "enum": [
        "publish",
        "future",
        "draft",
        "pending",
        "private",
        "trash",
        "auto-draft",
        "inherit",
        "any"
      ],
      "sanitize_callback": "sanitize_key",
      "type": "string",
      "validate_callback": [
        {},
        "validate_user_can_query_private_statuses"
      ]
    },
    "filter": {
      "description": "Use WP Query arguments to modify the response; private query vars require appropriate authorization."
    },
    "categories": {
      "description": "Limit result set to all items that have the specified term assigned in the categories taxonomy.",
      "type": "array",
      "sanitize_callback": "wp_parse_id_list",
      "default": []
    },
    "tags": {
      "description": "Limit result set to all items that have the specified term assigned in the tags taxonomy.",
      "type": "array",
      "sanitize_callback": "wp_parse_id_list",
      "default": []
    }
  },
  "callback": [
    {},
    "get_items"
  ],
  "permission_callback": [
    {},
    "get_items_permissions_check"
  ]
}
```

<!--
As you can see we have all of the information we have registered to our endpoint already there, ready to go! The request attributes are typically used at a lower level and are handled by the `WP_REST_Server` class, however there are cool things that can be done inside of endpoint callbacks, like restricting accepted parameters to match registered arguments.
-->

ご覧の通り、エンドポイントに登録した情報はすべてそろっており、準備万端です ! リクエスト属性は通常、より低いレベルで使用され、クラス `WP_REST_Server` によって処理されますが、エンドポイント・コールバック内部でできるクールなことがあります。たとえば、受け付けたパラメータを登録された引数と一致するように制限するようなことです。

<!--
The WP REST API is designed for you so that you do not have to mess around with any internals, so some of these more advanced methods of interacting with `WP_REST_Request` are not going to be commonly practiced. The core of using the WP REST API is linked to registering routes and endpoints. Requests are the tool we use to tell the API which endpoint we want to hit. This is most commonly done over HTTP, however we can also use `WP_REST_Request`s internally.
-->

WP REST API は、内部をいじくり回さなくてもいいように設計されているので、`WP_REST_Request` とやりとりするためのこれらの高度な方法のいくつかは、一般的に実践されることはないでしょう。WP REST API を利用するための核心は、ルートとエンドポイントを登録することに関わっています。リクエストは、API に対してどのエンドポイントにアクセスしたいかを伝えるためのツールです。これは最も一般的には HTTP で行われますが、`WP_REST_Request` を内部的に使うこともできます。

<!--
## Internal Requests
-->

## 内部リクエスト

<!--
The key to making internal requests is using `rest_do_request()`. All you need to do is pass in a request object and you will be returned a response. Because the request is never served by the `WP_REST_Server`, the response data is never encoded into json, meaning we have our response object as a PHP object. This is pretty awesome and enables us to do a lot of interesting things. For one, we can create efficient batch endpoints. From a performance perspective, one of the hurdles is minimizing HTTP requests. We can create batch endpoints that will use `rest_do_request()` to serve all of our requests internally all in one HTTP request. Here is a very simplistic batch endpoint for read only data, so you can see `rest_do_request()` in action.
-->

内部リクエストの鍵は、`rest_do_request()` を使うことに尽きます。リクエスト・オブジェクトを渡すだけで、レスポンスが返ってきます。リクエストが `WP_REST_Server` によって送信されることはないので、レスポンスデータは json にエンコードされることは決してありません。つまり、レスポンス・オブジェクトは PHP オブジェクトとなります。これはとてもすばらしいことで、多くのおもしろいことができます。ひとつは、効率的なバッチ・エンドポイントを作成できることです。パフォーマンスの観点からすると、ハードルのひとつは HTTP リクエストを最小限に抑えることです。`rest_do_request()` を使用して、内部的にすべてのリクエストを1つの HTTP リクエストで送信するバッチ・エンドポイントを作成できます。以下は、読み取り専用データ用の非常に単純なバッチ・エンドポイントで、`rest_do_request()` が動作している様子を見ることができます。

```
// Register our mock batch endpoint.
function prefix_register_batch_route() {
    register_rest_route( 'my-namespace/v1', '/batch', array(
        // Supported methods for this endpoint. WP_REST_Server::READABLE translates to GET.
        'methods' => WP_REST_Server::READABLE,
        // Register the callback for the endpoint.
        'callback' => 'prefix_do_batch_request',
        // Register args for the batch endpoint.
        'args' => prefix_batch_request_parameters(),
    ) );
}

add_action( 'rest_api_init', 'prefix_register_batch_route' );

/**
 * Our registered endpoint callback. Notice how we are passing in $request as an argument.
 * By default, the WP_REST_Server will pass in the matched request object to our callback.
 *
 * @param WP_REST_Request $request The current matched request object.
 */
function prefix_do_batch_request( $request ) {
    // Here we initialize the array that will hold our response data.
    $data = array();
	$data = prefix_handle_batch_requests( $request['requests'] );
	return $data;
}

/**
 * This handles the building of the response for the batch requests we make.
 *
 * @param array $requests An array of data to build WP_REST_Request objects from.
 * @return WP_REST_Response A collection of response data for batch endpoints.
 */
function prefix_handle_batch_requests( $requests ) {
	$data = array();

	// Foreach request specified in the requests param run the endpoint.
	foreach ( $requests as $request_params ) {
		$response = prefix_handle_request( $request_params );
		$key = $request_params['method'] . ' ' . $request_params['route'];
		$data[ $key ] = prefix_prepare_for_collection( $response );
	}

	return rest_ensure_response( $data );
}

/**
 * This handles the building of the response for the batch requests we make.
 *
 * @param array $request_params Data to build a WP_REST_Request object from.
 * @return WP_REST_Response Response data for the request.
 */
function prefix_handle_request( $request_params ) {
	$request = new WP_REST_Request( $request_params['method'], $request_params['route'] );

	// Add specified request parameters into the request.
	if ( isset( $request_params['params'] ) ) {
		foreach ( $request_params['params'] as $param_name => $param_value ) {
			$request->set_param( $param_name, $param_value );
		}
	}
	$response = rest_do_request( $request );
	return $response;
}

/**
 * Prepare a response for inserting into a collection of responses.
 *
 * This is lifted from WP_REST_Controller class in the WP REST API v2 plugin.
 *
 * @param WP_REST_Response $response Response object.
 * @return array Response data, ready for insertion into collection data.
 */
function prefix_prepare_for_collection( $response ) {
	if ( ! ( $response instanceof WP_REST_Response ) ) {
		return $response;
	}

	$data = (array) $response->get_data();
	$server = rest_get_server();

	if ( method_exists( $server, 'get_compact_response_links' ) ) {
		$links = call_user_func( array( $server, 'get_compact_response_links' ), $response );
	} else {
		$links = call_user_func( array( $server, 'get_response_links' ), $response );
	}

	if ( ! empty( $links ) ) {
		$data['_links'] = $links;
	}

	return $data;
}

/**
 * Returns the JSON schema data for our registered parameters.
 *
 * @return array $params A PHP representation of JSON Schema data.
 */
function prefix_batch_request_parameters() {
    $params = array();

    $params['requests'] = array(
		'description'        => esc_html__( 'An array of request objects arguments that can be built into WP_REST_Request instances.', 'my-text-domain' ),
		'type'               => 'array',
		'required'           => true,
		'validate_callback'  => 'prefix_validate_requests',
		'items'              => array(
			array(
				'type' => 'object',
				'properties' => array(
					'method' => array(
						'description' => esc_html__( 'HTTP Method of the desired request.', 'my-text-domain' ),
						'type'        => 'string',
						'required'    => true,
						'enum'        => array(
							'GET',
							'POST',
							'PUT',
							'DELETE',
							'OPTIONS',
						),
					),
					'route' => array(
						'description' => esc_html__( 'Desired route for the request.', 'my-text-domain' ),
						'required'    => true,
						'type'        => 'string',
						'format'      => 'uri',
					),
					'params' => array(
						'description' => esc_html__( 'Key value pairs of desired request parameters.', 'my-text-domain' ),
						'type' => 'object',
					),
				),
			),
		),
	);

	return $params;
}

function prefix_validate_requests( $requests, $request, $param_key ) {
	// If requests isn't an array of requests then we don't process the batch.
	if ( ! is_array( $requests ) ) {
		return new WP_Error( 'rest_invald_param', esc_html__( 'The requests parameter must be an array of requests.' ), array( 'status' => 400 ) );
	}

	foreach ( $requests as $request ) {
		// If the method or route is not set then we do not run the requests.
		if ( ! isset( $request['method'] ) || ! isset( $request['route'] ) ) {
			return new WP_Error( 'rest_invald_param', esc_html__( 'You must specify the method and route for each request.' ), array( 'status' => 400 ) );
		}

		if ( isset( $request['params'] ) && ! is_array( $request['params'] ) ) {
			return new WP_Error( 'rest_invald_param', esc_html__( 'You must specify the params for each request as an array of named key value pairs.' ), array( 'status' => 400 ) );
		}
	}

	// This is a black listing approach to data validation.
	return true;
}
```

<!--
That is quite a decent chunk of code that covers a number of topics, but everything centers around what happens in `prefix_handle_request()`. Here we are passing in an array that tells us a HTTP method, a route, and a set of parameters we want to turn into a request. We then build the request object for the method and route. If any parameters were specified we use the `WP_REST_Request::set_param()` method to add in the desired parameters. Once our `WP_REST_Request` is ready to go we use `rest_do_request` to internally match that endpoint and the response is returned to our batch endpoint response collection. Using a batch endpoint like this can net you huge performance gains, as you will only make one HTTP request to get a response for multiple endpoints. The implementation of this is not necessarily the best and serves as an example; not the only way to do this.
-->

これは、多くのトピックをカバーする、かなりまとまったコードの塊だが、すべては `prefix_handle_request()` で起こることが中心となっています。ここでは、HTTP メソッド、ルート、そしてリクエストとしたいパラメータのセットを配列で渡しています。次に、メソッドとルートに対してリクエスト・オブジェクトを構築します。パラメータが指定されている場合は、メソッド `WP_REST_Request::set_param()` を使用して必要なパラメータを追加します。`WP_REST_Request` が準備できたら、`rest_do_request` を使って内部的にそのエンドポイントに一致させ、レスポンスをバッチ・エンドポイント・レスポンスコレクションに返します。このようにバッチ・エンドポイントを使えば、複数のエンドポイントに対するレスポンスを得るための HTTP リクエストは1回だけですので、パフォーマンスが大幅に向上します。この実装は必ずしもベストではなく、あくまで一例であり、これが唯一の方法という訳ではありません。
