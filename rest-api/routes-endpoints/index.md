<!-- 
# Routes & Endpoints
 -->
# ルートとエンドポイント

<!-- 
The REST API provides us a way to match URIs to various resources in our WordPress install. By default, if you have pretty permalinks enabled, the WordPress REST API “lives” at `/wp-json/`. At our WordPress site `https://ourawesomesite.com`, we can access the REST API’s index by making a `GET` request to `https://ourawesomesite.com/wp-json/`. The index provides information regarding what routes are available for that particular WordPress install, along with what HTTP methods are supported and what endpoints are registered.
 -->
REST API は、WordPress の様々なリソースに URI を対応させる方法を提供してくれます。デフォルトでは、きれいなパーマリンクを有効にしている場合、WordPress REST API は `/wp-json/` に「存在」します。私たちの WordPress サイト `https://ourawesomesite.com` では、`https://ourawesomesite.com/wp-json/` に `GET` リクエストを行うことで、REST API のインデックスにアクセスできます。インデックスは、どの HTTP メソッドがサポートされ、どのエンドポイントが登録されているかとともに、その特定の WordPress インストールでどのルートが利用可能かに関する情報を提供します。

<!-- 
If we wanted to create an endpoint that would return the phrase “Hello World, this is the WordPress REST API”, we would first need to register the route for that endpoint. To register routes you should use the `register_rest_route()` function. It needs to be called on the `rest_api_init` action hook. `register_rest_route()` handles all of the mapping for routes to endpoints. Let’s try to create a “Hello World, this is the WordPress REST API” route.
 -->
「Hello World, this is the WordPress REST API」というフレーズを返すエンドポイントを作りたかったら、まずそのエンドポイント用のルートを登録する必要があります。ルートを登録するには、関数 `register_rest_route()` を使用する必要があります。この関数は、アクションフック `rest_api_init` で呼び出す必要があります。`register_rest_route()` は、ルートとエンドポイントのマッピングをすべて処理します。ルート「Hello World, this is the WordPress REST API」を作ってみましょう。

```
/**
 * This is our callback function that embeds our phrase in a WP_REST_Response
 */
function prefix_get_endpoint_phrase() {
    // rest_ensure_response() wraps the data we want to return into a WP_REST_Response, and ensures it will be properly returned.
    return rest_ensure_response( 'Hello World, this is the WordPress REST API' );
}

/**
 * This function is where we register our routes for our example endpoint.
 */
function prefix_register_example_routes() {
    // register_rest_route() handles more arguments but we are going to stick to the basics for now.
    register_rest_route( 'hello-world/v1', '/phrase', array(
        // By using this constant we ensure that when the WP_REST_Server changes our readable endpoints will work as intended.
        'methods'  => WP_REST_Server::READABLE,
        // Here we register our callback. The callback is fired when this endpoint is matched by the WP_REST_Server class.
        'callback' => 'prefix_get_endpoint_phrase',
    ) );
}

add_action( 'rest_api_init', 'prefix_register_example_routes' );
```

<!-- 
The first argument passed into `register_rest_route()` is the namespace, which provides us a way to group our routes. The second argument passed in is the resource path, or resource base. For our example, the resource we are retrieving is the “Hello World, this is the WordPress REST API” phrase. The third argument is an array of options. We specify what methods the endpoint can use and what callback should happen when the endpoint is matched (more things can be done but these are the fundamentals).
 -->
`register_rest_route()` に渡される第1引数は、名前空間で、ルートをグループ化する方法を提供します。第2引数は、リソース・パス、またはリソース・ベースです。この例では、取得するリソースは、フレーズ「Hello World, this is the WordPress REST API」です。第3引数は、オプションの配列です。エンドポイントが使用できるメソッドと、エンドポイントが一致したときに発生するコールバックを指定します (もっといろいろなことができますが、これらが基本です)。

<!-- 
The third argument also allows us to provide a permissions callback, which can restrict access for the endpoint to only certain users. The third argument also offers a way to register arguments for the endpoint so that requests can modify the response of our endpoint. We will get into those concepts in the endpoints section of this guide.
 -->
第3引数では、エンドポイントへのアクセスを特定のユーザーだけに制限できる「パーミッション・コールバック」も提供できます。第3引数はまた、エンドポイントに引数を登録する方法を提供し、リクエストがエンドポイントのレスポンスを変更できるようにします。これらのコンセプトについては、このガイドのエンドポイントのセクションで説明します。

<!-- 
When we go to `https://ourawesomesite.com/wp-json/hello-world/v1/phrase` we can now see our REST API greeting us kindly. Let’s take a look at routes a bit more in depth.
 -->
`https://ourawesomesite.com/wp-json/hello-world/v1/phrase` にアクセスすると、REST API が親切に迎えてくれます。ルートをもう少し詳しく見てみましょう。

<!-- 
## Routes
 -->
## ルート

<!-- 
Routes in the REST API are represented by URIs. The route itself is what is tacked onto the end of `https://ourawesomesite.com/wp-json`. The index route for the API is `'/'` which is why `https://ourawesomesite.com/wp-json/` returns all of the available information for the API. All routes should be built onto this route, the `wp-json` portion can be changed, but in general, it is advised to keep it the same.
 -->
REST API のルートは、URI で表現されます。ルートそのものは、`https://ourawesomesite.com/wp-json` の末尾に付加されるものです。API のインデックスルートは `'/'` であり、`https://ourawesomesite.com/wp-json/` は API で利用可能なすべての情報を返します。すべてのルートは、このルートの上に構築する必要があり、`wp-json` の部分は変更可能ですが、一般的には同じにしておくことをおすすめします。

<!-- 
We want to make sure that our routes are unique. For instance we could have a route for books like this: `/books`. Our books route would now live at `https://ourawesomesite.com/wp-json/books`. However, this is not a good practice as we would end up polluting potential routes for the API. What if another plugin we wanted to register a books route as well? We would be in big trouble in that case, as the two routes would conflict with each other and only one could be used. The fourth parameter to `register_rest_field()` is a boolean for whether the route should override an existing route.
 -->
ルートは、一意なものにしたいですね。たとえば、次のような書籍用のルートを持つことができます: `/books`。私たちのルート「books」は、`https://ourawesomesite.com/wp-json/books` に存在します。しかし、これは API の潜在的なルートを汚してしまうことになるので、良いやり方とは言えません。もし別のプラグインがルート「books」も登録したいと思った場合は、どうしたらいいでしょう ? この場合、2つのルートが衝突してしまい、1つのルートしか使えなくなってしまうので、大変なことになります。`register_rest_field()` の第4パラメータは、ルートが既存のルートをオーバーライドするかどうかを示すブール値です。

<!-- 
The override parameter does not really solve our problem either, as both routes could override or we would want to use both routes for different things. This is where using namespaces for our routes comes in.
 -->
パラメータ override は、両方のルートがオーバーライドされる可能性があるため、あるいは両方のルートを異なることに使いたいため、私たちの問題を解決するものではありません。そこで、ルートに名前空間を使うことになります。

<!-- 
### Namespaces
 -->
### 名前空間

<!-- 
It is extremely important to add namespaces to your routes. The “core” endpoints, which are awaiting to be merged into WordPress core, use the `/wp/v2` namespace.
 -->
ルートに名前空間を追加することは、非常に重要です。WordPress コアへの統合が待たれる「core」エンドポイントは、名前空間 `/wp/v2` を使用します。

<!-- 
[info]**DO NOT PLACE ANYTHING INTO THE `/wp` NAMESPACE UNLESS YOU ARE MAKING ENDPOINTS WITH THE INTENTION OF MERGING THEM INTO CORE.**[/info]
 -->
[info]**コアにマージするつもりでエンドポイントを作っているのでなければ、名前空間 `/wp` には何も置かないでください。**[/info]

<!-- 
There are some key things to take notice of in the core endpoint namespace. The first part of the namespace is `/wp`, which represents the vendor name; WordPress. For our plugins we will want to come up with unique names for what we call the vendor portion of the namespace. In the example above we used `hello-world`.
 -->
コアエンドポイントの名前空間には、注意すべき点がいくつかあります。名前空間の最初の部分は `/wp` で、これはベンダー名を表しています; WordPress。私たちのプラグインでは、名前空間のベンダーの部分に、ユニークな名前を付けたいと思います。上記の例では、`hello-world` を使用しました。

<!-- 
Following the vendor portion is the version portion of the namespace. The “core” endpoints utilize `v2` to represent version 2 of the WordPress REST API. If you are writing a plugin, you can maintain backwards compatibility of your REST API endpoints by simply creating new endpoints and bumping up the version number you provide. This way both the original `v1` and `v2` endpoints can be accessed.
 -->
「ベンダー」パートに続くのは、「名前空間のバージョン」パートです。「コア」エンドポイントは `v2` を使用して、「WordPress REST API のバージョン2」を表します。プラグインを書いている場合は、新しいエンドポイントを作成し、提供するバージョン番号を上げるだけで、REST API エンドポイントの後方互換性を保つことができます。こうすることで、元の `v1` と `v2` の両方のエンドポイントにアクセスできます。

<!-- 
The part of the route that follows the namespace is the resource path.
 -->
ルートの「名前空間」に続くパートは、「リソースパス」です。

<!-- 
### Resource Paths
 -->
### リソース・パス

<!-- 
The resource path should signify what resource the endpoint is associated with. In the example we used above, we used the word `phrase` to signify that the resource we are interacting with is a phrase. To avoid any collisions, each resource path we register should also be unique within a namespace. Resource paths should be used to define different resource routes within a given namespace.
 -->
リソース・パスは、エンドポイントがどのようなリソースに関連付けられているかを示す必要があります。上記の例では、扱うリソースがフレーズであることを示すために `phrase` という単語を使っています。衝突を避けるために、登録する各リソース・パスも名前空間内で一意でなければなりません。リソース・パスは、与えられた名前空間内で異なるリソースルートを定義するために使用されるべきです。

<!-- 
Let’s say we have a plugin that handles some basic eCommerce functionality. We will have two main resource types orders, and products. Orders are a request for product(s) but they are not the product themselves. The same concept applies to products. Although these resources are related they are not the same thing and each should live in a separate resource paths. Our routes will end up looking something like this for our eCommerce plugin: `/my-shop/v1/orders` and `/my-shop/v1/products`.
 -->
基本的な e コマース機能を処理するプラグインがあるとします。注文と商品という2つの主要なリソースタイプがあります。注文は商品のリクエストですが、商品そのものではありません。同じコンセプトが、商品にも当てはまります。これらのリソースは関連していますが、同じものではなく、それぞれ別のリソース・パスに存在する必要があります。e コマース・プラグインの場合、ルートは以下のようになります: `/my-shop/v1/orders` と `/my-shop/v1/products`。

<!-- 
Using routes like this, we would want each to return a collection of orders or products. What if we wanted to grab a specific product by ID, we would need to use path variables in our routes.
 -->
このようなルートを使って、それぞれが注文や商品のコレクションを返すようにしたいですね。ID で特定の商品を取得したい場合は、ルートでパス変数を使用する必要があります。

<!-- 
### Path Variables
 -->
### パス変数

<!-- 
Path variables enable us to add dynamic routes. To expand on our eCommerce routes, we could register a route to grab individual products.
 -->
パス変数によって、動的なルートを追加できます。e コマースのルートを拡張するために、個々の商品を取得するルートを登録できます。

```
/**
 * This is our callback function to return our products.
 *
 * @param WP_REST_Request $request This function accepts a rest request to process data.
 */
function prefix_get_products( $request ) {
    // In practice this function would fetch the desired data. Here we are just making stuff up.
    $products = array(
        '1' => 'I am product 1',
        '2' => 'I am product 2',
        '3' => 'I am product 3',
    );

    return rest_ensure_response( $products );
}

/**
 * This is our callback function to return a single product.
 *
 * @param WP_REST_Request $request This function accepts a rest request to process data.
 */
function prefix_get_product( $request ) {
    // In practice this function would fetch the desired data. Here we are just making stuff up.
    $products = array(
        '1' => 'I am product 1',
        '2' => 'I am product 2',
        '3' => 'I am product 3',
    );

    // Here we are grabbing the 'id' path variable from the $request object. WP_REST_Request implements ArrayAccess, which allows us to grab properties as though it is an array.
    $id = (string) $request['id'];

    if ( isset( $products[ $id ] ) ) {
        // Grab the product.
        $product = $products[ $id ];

        // Return the product as a response.
        return rest_ensure_response( $product );
    } else {
        // Return a WP_Error because the request product was not found. In this case we return a 404 because the main resource was not found.
        return new WP_Error( 'rest_product_invalid', esc_html__( 'The product does not exist.', 'my-text-domain' ), array( 'status' => 404 ) );
    }

    // If the code somehow executes to here something bad happened return a 500.
    return new WP_Error( 'rest_api_sad', esc_html__( 'Something went horribly wrong.', 'my-text-domain' ), array( 'status' => 500 ) );
}

/**
 * This function is where we register our routes for our example endpoint.
 */
function prefix_register_product_routes() {
    // Here we are registering our route for a collection of products.
    register_rest_route( 'my-shop/v1', '/products', array(
        // By using this constant we ensure that when the WP_REST_Server changes our readable endpoints will work as intended.
        'methods'  => WP_REST_Server::READABLE,
        // Here we register our callback. The callback is fired when this endpoint is matched by the WP_REST_Server class.
        'callback' => 'prefix_get_products',
    ) );
    // Here we are registering our route for single products. The (?P<id>[\d]+) is our path variable for the ID, which, in this example, can only be some form of positive number.
    register_rest_route( 'my-shop/v1', '/products/(?P<id>[\d]+)', array(
        // By using this constant we ensure that when the WP_REST_Server changes our readable endpoints will work as intended.
        'methods'  => WP_REST_Server::READABLE,
        // Here we register our callback. The callback is fired when this endpoint is matched by the WP_REST_Server class.
        'callback' => 'prefix_get_product',
    ) );
}

add_action( 'rest_api_init', 'prefix_register_product_routes' );
```

<!-- 
The above example covers a lot. The important part to note is that in the second route we register, we add on a path variable `/(?P[\d]+)` to our resource path `/products`. The path variable is a regular expression. In this case it uses `[\d]+` to signify that should be any numerical character at least once. If you are using numeric IDs for your resources, then this is a great example of how to use a path variable. When using path variables, we now have to be careful around what can be matched as it is user input.
 -->
上記の例では、多くのことをカバーしています。注意すべき重要な点は、2番目に登録したルートで、リソース・パス `/products` にパス変数 `/(?P[\d]+)` を追加していることです。パス変数は、正規表現です。このケースでは、`[\d]+` を使って、少なくとも1回は任意の数字が入るようにします。リソースに数値の ID を使っているのであれば、これはパス変数の使い方の良い例です。パス変数を使用する場合、ユーザー入力であるため、一致させることができるものに注意する必要があります。

<!-- 
The regex luckily will filter out anything that is not numerical. However, what if the product for the requested ID doesn’t exist. We need to do error handling. You can see the basic way we are handling errors in the code example above. When you return a `WP_Error` in your endpoint callbacks the API server will automatically handle serving the error to the client.
 -->
正規表現は、幸いにも数値以外のものを除外してくれます。しかし、要求された ID の商品が存在しない場合は、どうなるでしょうか。エラー処理が必要です。上のコード例でエラー処理の基本的な方法を見ることができます。エンドポイントコールバックで `WP_Error` を返すと、API サーバーは自動的にクライアントにエラーを提供する処理を行います。

<!-- 
Although this section is about routes, we have covered quite a bit about endpoints. Endpoints and routes are interrelated, but they definitely have distinctions.
 -->
このセクションはルートについてですが、エンドポイントについてもかなり取り上げました。エンドポイントとルートは相互に関連していますが、明確に区別されています。

<!-- 
## Endpoints
 -->
## エンドポイント

<!-- 
Endpoints are the destination that a route needs to map to. For any given route, you could have a number of different endpoints registered to it. We will expand on our fictitious eCommerce plugin, to better show the distinction between routes and endpoints. We are going to create two endpoints that exist at the `/wp-json/my-shop/v1/products/` route. One endpoint uses the HTTP verb `GET` to get products, and the other endpoint uses the HTTP verb `POST` to create a new product.
 -->
エンドポイントは、ルートがマップする必要のある目的地です。任意のルートに対して、いくつかの異なるエンドポイントを登録できます。ルートとエンドポイントの区別を明確にするために、架空の e コマースプラグインを拡張します。ルート `/wp-json/my-shop/v1/products/` に存在する2つのエンドポイントを作成します。一方のエンドポイントは HTTP メソッド `GET` を使って商品を取得し、もう一方のエンドポイントは HTTP メソッド `POST` を使って新しい商品を作成します。

```
/**
 * This is our callback function to return our products.
 *
 * @param WP_REST_Request $request This function accepts a rest request to process data.
 */
function prefix_get_products( $request ) {
    // In practice this function would fetch the desired data. Here we are just making stuff up.
    $products = array(
        '1' =&gt; 'I am product 1',
        '2' =&gt; 'I am product 2',
        '3' =&gt; 'I am product 3',
    );

    return rest_ensure_response( $products );
}

/**
 * This is our callback function to return a single product.
 *
 * @param WP_REST_Request $request This function accepts a rest request to process data.
 */
function prefix_create_product( $request ) {
    // In practice this function would create a product. Here we are just making stuff up.
   return rest_ensure_response( 'Product has been created' );
}

/**
 * This function is where we register our routes for our example endpoint.
 */
function prefix_register_product_routes() {
    // Here we are registering our route for a collection of products and creation of products.
    register_rest_route( 'my-shop/v1', '/products', array(
        array(
            // By using this constant we ensure that when the WP_REST_Server changes, our readable endpoints will work as intended.
            'methods'  =&gt; WP_REST_Server::READABLE,
            // Here we register our callback. The callback is fired when this endpoint is matched by the WP_REST_Server class.
            'callback' =&gt; 'prefix_get_products',
        ),
        array(
            // By using this constant we ensure that when the WP_REST_Server changes, our create endpoints will work as intended.
            'methods'  =&gt; WP_REST_Server::CREATABLE,
            // Here we register our callback. The callback is fired when this endpoint is matched by the WP_REST_Server class.
            'callback' =&gt; 'prefix_create_product',
        ),
    ) );
}

add_action( 'rest_api_init', 'prefix_register_product_routes' );
```

<!-- 
Depending on what HTTP Method we use for the route `/wp-json/my-shop/v1/products`, we are matched to a different endpoint and a different callback is fired. When we use `POST` we trigger the `prefix_create_product()` callback, and when we use `GET` we trigger the `prefix_get_products()` callback.
 -->
どの HTTP メソッドをルート `/wp-json/my-shop/v1/products` に使用するかによって、異なるエンドポイントに一致し、異なるコールバックが発生します。`POST` を使うとコールバック `prefix_create_product()` がトリガーされ、`GET` を使うとコールバック `prefix_get_products()` がトリガーされます。

<!-- 
There are a number of different HTTP methods and the REST API can make use of any of them.
 -->
HTTP メソッドにはいくつもの種類があり、REST API はそのどれでも利用できます。

<!-- 
### HTTP Methods
 -->
### HTTP メソッド

<!-- 
HTTP methods are sometimes referred to as HTTP verbs. They are simply just different ways to communicate via HTTP. The main ones used by the WordPress REST API are:
 -->
HTTP メソッドは、HTTP 動詞と呼ばれることもあります。これらは単に、HTTP を介して通信するためのいろいろな方法です。WordPress REST API で使用される主なものは次のとおりです:

<!-- 
- `GET` should be used for retrieving data from the API.
- `POST` should be used for creating new resources (i.e users, posts, taxonomies).
- `PUT` should be used for updating resources.
- `DELETE` should be used for deleting resources.
- `OPTIONS` should be used to provide context about our resources.
 -->
- `GET` は API からデータを取得するために使用します。
- `POST` は、新しいリソース (ユーザー、投稿、タクソノミー、など) を作成する際に使用します。
- `PUT` は、リソースの更新に使用します。
- `DELETE` は、リソースの削除に使用します。
- `OPTIONS` は、リソースに関するコンテキストを提供するために使用します。

<!-- 
It is important to note that these methods are not supported by every client, as they were introduced in HTTP 1.1. Luckily, the API provides a workaround for these unfortunate cases. If you want to delete a resource but can’t send a `DELETE` request, then you can use the `_method` parameter or the `X-HTTP-Method-Override` header in your request. How this works is you will send a `POST` request to `https://ourawesomesite.com/wp-json/my-shop/v1/products/1?_method=DELETE`. Now you will have deleted product number 1, even though your client could not send the proper HTTP method in the request, or maybe there was a firewall in place that blocks out DELETE requests.
 -->
これらのメソッドは HTTP 1.1で導入されたため、すべてのクライアントでサポートされているわけではないことに注意することが重要です。幸いなことに、API はこのような不運なケースを回避する手段を提供しています。リソースを削除したいが、リクエスト `DELETE` を送ることができない場合は、パラメータ `_method` またはヘッダー `X-HTTP-Method-Override` をリクエストに使用できます。これがどのように動作するかというと、リクエスト `POST` を `https://ourawesomesite.com/wp-json/my-shop/v1/products/1?_method=DELETE` に送信します。クライアントがリクエストに適切な HTTP メソッドを送信できなかったにもかかわらず、あるいは DELETE リクエストをブロックするファイアウォールがあったにもかかわらず、あなたは製品番号1を削除したことになります。

<!-- 
The HTTP method, in combination with the route and callbacks, are what make up the core of an endpoint.
 -->
HTTP メソッドと、ルート、コールバックの組み合わせが、エンドポイントの核となるものです。

<!-- 
### Callbacks
 -->
### コールバック

<!-- 
There are currently only two types of callbacks for endpoints supported by the REST API; `callback` and `permissions_callback`. The main callback should handle the interaction with the resource. The permissions callback should handle what users have access to the endpoint. You can add additional callbacks by adding additional information when registering an endpoint. You can then hook into `rest_pre_dispatch`, `rest_dispatch_request`, or `rest_post_dispatch` hooks to fire your new custom callbacks.
 -->
現在のところ、REST API でサポートされているエンドポイントのコールバックは2種類しかありません; `callback` と `permissions_callback` です。メインのコールバックは、リソースとのやりとりを処理します。パーミッション・コールバックは、どのユーザーがエンドポイントにアクセスできるかを処理します。エンドポイントを登録する際に情報を追加することで、コールバックを追加できます。その後、フック `rest_pre_dispatch`、フック `rest_dispatch_request`、または フック `rest_post_dispatch` にフックして、新しいカスタム・コールバックを呼び出すことができます。

<!-- 
#### Endpoint Callback
 -->
#### エンドポイント・コールバック

<!-- 
The main callback for a delete endpoint should only delete the resource and return a copy of it in the response. The main callback for a creation endpoint should only create the resource and return a response matching the newly created data. An update callback should only modify resources that actually exist. A reading callback should only retrieve data that already exists. It is important to take into account the concept of idempotence.
 -->
エンドポイント delete のメイン・コールバックは、リソースを削除し、そのコピーをレスポンスに返すだけであるべきです。エンドポイント creation のメイン・コールバックは、リソースを作成し、新しく作成されたデータと一致するレスポンスを返すだけであるべきです。コールバック update は、実際に存在するリソースのみを変更するべきです。コールバック reading は、既に存在するデータのみを取得するべきです。「巾等 (べきとう) 性のコンセプト (ある操作を1回行っても、複数回行っても、結果が同じであること)」を考慮することが重要です。

<!-- 
Idempotence, in the context of a REST API, means that if you make the same request to an endpoint the server will process the request the same way. Imagine if our read endpoint was not idempotent. Whenever we made a request to it the state of our server would be modified by the request, even though we were only trying to get data. This could be catastrophic. Any time someone fetched data from your server something would change internally. It is important to make sure that read, update, and delete endpoints do not have nasty side effects and just stick to what they are intended to do.
 -->
REST API でいうところの巾等性とは、エンドポイントに同じリクエストをした場合、サーバーは同じようにリクエストを処理することを意味します。エンドポイント read が巾等でなかったらと想像してみてください。データを取得しようとしているだけなのに、リクエストをするたびに、サーバーの状態はリクエストによって変更されてしまうのです。これでは、大惨事になりかねません。誰かがサーバーからデータを取得するたびに、内部で何かが変わってしまうのです。read、update、delete の各エンドポイントに厄介な副作用がないことを確認し、本来の目的に忠実であることが重要です。

<!-- 
In a REST API, the concept of idempotence is tied to HTTP methods instead of endpoint callbacks. Any callback using `GET`, `HEAD`, `TRACE`, `OPTIONS`, `PUT`, or `DELETE`, should not produce any side effects. `POST` requests are not idempotent, and are typically used for creating resources. If you created an idempotent creation method then you would only ever create one resource because when you make the same request there would be no more side effects to the server. For creating, if you make the same request over and over the server should generate new resources each time.
 -->
REST API では、巾等性のコンセプトは、エンドポイント・コールバックではなく HTTP メソッドと結び付いています。`GET`、`HEAD`、`TRACE`、`OPTIONS`、`PUT`、`DELETE` を使用したコールバックは、副作用を発生させるべきではありません。リクエスト `POST` は巾等ではなく、通常はリソースを作成するために使用されます。巾等なメソッド creation を作れば、同じリクエストをしたときにサーバーへの副作用がなくなるので、作成するリソースは1つだけになるでしょう。同じリクエストを何度も繰り返すと、サーバーはそのたびに新しいリソースを生成しなければなりません。

<!-- 
To restrict usage of endpoints we need to register a permissions callback.
 -->
エンドポイントの利用を制限するには、パーミッション・コールバックを登録する必要があります。

<!-- 
#### Permissions Callback
 -->
#### パーミッション・コールバック

<!-- 
Permissions callbacks are extremely important for security with the WordPress REST API. If you have any private data that should not be displayed publicly, then you need to have permissions callbacks registered for your endpoints. Below is an example of how to register permissions callbacks.
 -->
パーミッション・コールバックは、WordPress REST API のセキュリティにとって非常に重要です。一般に公開すべきでないプライベートなデータがある場合は、エンドポイントにパーミッション・コールバックを登録する必要があります。以下は、パーミッション・コールバックの登録方法の例です。

```
/**
 * This is our callback function that embeds our resource in a WP_REST_Response
 */
function prefix_get_private_data() {
    // rest_ensure_response() wraps the data we want to return into a WP_REST_Response, and ensures it will be properly returned.
    return rest_ensure_response( 'This is private data.' );
}

/**
 * This is our callback function that embeds our resource in a WP_REST_Response
 */
function prefix_get_private_data_permissions_check() {
    // Restrict endpoint to only users who have the edit_posts capability.
    if ( ! current_user_can( 'edit_posts' ) ) {
        return new WP_Error( 'rest_forbidden', esc_html__( 'OMG you can not view private data.', 'my-text-domain' ), array( 'status' => 401 ) );
    }

    // This is a black-listing approach. You could alternatively do this via white-listing, by returning false here and changing the permissions check.
    return true;
}

/**
 * This function is where we register our routes for our example endpoint.
 */
function prefix_register_example_routes() {
    // register_rest_route() handles more arguments but we are going to stick to the basics for now.
    register_rest_route( 'my-plugin/v1', '/private-data', array(
        // By using this constant we ensure that when the WP_REST_Server changes our readable endpoints will work as intended.
        'methods'  => WP_REST_Server::READABLE,
        // Here we register our callback. The callback is fired when this endpoint is matched by the WP_REST_Server class.
        'callback' => 'prefix_get_private_data',
        // Here we register our permissions callback. The callback is fired before the main callback to check if the current user can access the endpoint.
        'permissions_callback' => 'prefix_get_private_data_permissions_check',
    ) );
}

add_action( 'rest_api_init', 'prefix_register_example_routes' );
```

<!-- 
If you try out this endpoint without any Authentication enabled then you will also be returned the error response, preventing you from seeing the data. Authentication is a huge topic and eventually a portion of this chapter will be created to show you how to create your own authentication processes.
 -->
認証が有効になっていない状態でこのエンドポイントを試すと、エラー・レスポンスが返され、データを見ることができません。認証は大きなトピックですので、最終的には本章の一部で、独自の認証プロセスを作成する方法を紹介することになるでしょう。

<!-- 
### Arguments
 -->
### 引数

<!-- 
When making requests to an endpoint you might need to specify extra parameters to change the response. These extra parameters can be added while registering endpoints. Let’s look at an example of how to use arguments with an endpoint.
 -->
エンドポイントへのリクエストを行う際に、レスポンスを変更するための追加パラメータを指定する必要があるかもしれません。これらの追加パラメータは、エンドポイントを登録する際に追加できます。エンドポイントで引数を使う例を見てみましょう。

```
/**
 * This is our callback function that embeds our resource in a WP_REST_Response
 */
function prefix_get_colors( $request ) {
    // In practice this function would fetch the desired data. Here we are just making stuff up.
    $colors = array(
        'blue',
        'blue',
        'red',
        'red',
        'green',
        'green',
    );

    if ( isset( $request['filter'] ) ) {
       $filtered_colors = array();
       foreach ( $colors as $color ) {
           if ( $request['filter'] === $color ) {
               $filtered_colors[] = $color;
           }
       }
       return rest_ensure_response( $filtered_colors );
    }
    return rest_ensure_response( $colors );
}

/**
 * We can use this function to contain our arguments for the example product endpoint.
 */
function prefix_get_color_arguments() {
    $args = array();
    // Here we are registering the schema for the filter argument.
    $args['filter'] = array(
        // description should be a human readable description of the argument.
        'description' => esc_html__( 'The filter parameter is used to filter the collection of colors', 'my-text-domain' ),
        // type specifies the type of data that the argument should be.
        'type'        => 'string',
        // enum specified what values filter can take on.
        'enum'        => array( 'red', 'green', 'blue' ),
    );
    return $args;
}

/**
 * This function is where we register our routes for our example endpoint.
 */
function prefix_register_example_routes() {
    // register_rest_route() handles more arguments but we are going to stick to the basics for now.
    register_rest_route( 'my-colors/v1', '/colors', array(
        // By using this constant we ensure that when the WP_REST_Server changes our readable endpoints will work as intended.
        'methods'  => WP_REST_Server::READABLE,
        // Here we register our callback. The callback is fired when this endpoint is matched by the WP_REST_Server class.
        'callback' => 'prefix_get_colors',
        // Here we register our permissions callback. The callback is fired before the main callback to check if the current user can access the endpoint.
        'args' => prefix_get_color_arguments(),
    ) );
}

add_action( 'rest_api_init', 'prefix_register_example_routes' );
```

<!-- 
We have now specified a `filter` argument for this example. We can specify the argument as a query parameter when we request the endpoint. If we make a `GET` request to `https://ourawesomesitem.com/my-colors/v1/colors?filter=blue`, we will be returned only the blue colors in our collection. You could also pass these as body parameters in the request body, instead of in the query string. To understand the distinction between query parameters and body parameters you should read about the HTTP spec. Query parameters live in the query string tacked onto the URL and body parameters are directly embedded in the body of an HTTP request.
 -->
この例では、引数 `filter` を指定しました。この引数は、エンドポイントをリクエストするときの、クエリーパラメータとして指定できます。`https://ourawesomesitem.com/my-colors/v1/colors?filter=blue` にリクエスト `GET` をすると、コレクション内の青い色だけが返されます。クエリー文字列の代わりに、リクエストボディのボディパラメータとしてこれらを渡すこともできます。クエリーパラメータとボディパラメータの違いを理解するには、HTTP 仕様書を読む必要があります。クエリーパラメータは、URL に付加されたクエリー文字列の中にあり、ボディパラメータは、HTTP リクエストのボディに直接埋め込まれます。

<!-- 
We have created an argument for our endpoint, but how do we verify that the argument is a string and tell whether it matches the value red, green, or blue. To do this we need to specify a validation callback for our argument.
 -->
エンドポイント用の引数を作成しましたが、引数が文字列であることを確認し、それが値 red、green、blue に一致するかどうかを判断するにはどうすればよいでしょうか。そのためには、引数の検証コールバックを指定する必要があります。

<!-- 
#### Validation
 -->
#### バリデーション (検証)

<!-- 
Validation and sanitization are extremely important for security in the API. The validate callback (in WP 4.6+), fires before the sanitize callback. You should use the `validate_callback` for your arguments to verify whether the input you are receiving is valid. The `sanitize_callback` should be used to transform the argument input or clean out unwanted parts out of the argument, before the argument is processed by the main callback.
 -->
バリデーション (検証) とサニタイズは、API のセキュリティにとって非常に重要です。コールバック validate (WordPress 4.6以降の場合) は、コールバック sanitize の前に実行されます。引数に対して `validate_callback` を使用して、受け取る入力が有効かどうかを確認する必要があります。`sanitize_callback` は、引数がメイン・コールバックで処理される前に、引数の入力を変換したり、引数から不要な部分を削除したりするために使用する必要があります。

<!-- 
In the example above, we need to verify that the `filter` parameter is a string, and it matches the value red, green, or blue. Let’s look at what the code looks like after adding in a `validate_callback`.
 -->
上の例では、パラメータ `filter` が文字列であり、red, green, blue のいずれかに一致することを確認する必要があります。`validate_callback` を追加した後のコードを見てみましょう。

```
/**
 * This is our callback function that embeds our resource in a WP_REST_Response
 */
function prefix_get_colors( $request ) {
    // In practice this function would fetch more practical data. Here we are just making stuff up.
    $colors = array(
        'blue',
        'blue',
        'red',
        'red',
        'green',
        'green',
    );

    if ( isset( $request['filter'] ) ) {
       $filtered_colors = array();
       foreach ( $colors as $color ) {
           if ( $request['filter'] === $color ) {
               $filtered_colors[] = $color;
           }
       }
       return rest_ensure_response( $filtered_colors );
    }
    return rest_ensure_response( $colors );
}
/**
 * Validate a request argument based on details registered to the route.
 *
 * @param  mixed            $value   Value of the 'filter' argument.
 * @param  WP_REST_Request  $request The current request object.
 * @param  string           $param   Key of the parameter. In this case it is 'filter'.
 * @return WP_Error|boolean
 */
function prefix_filter_arg_validate_callback( $value, $request, $param ) {
    // If the 'filter' argument is not a string return an error.
    if ( ! is_string( $value ) ) {
        return new WP_Error( 'rest_invalid_param', esc_html__( 'The filter argument must be a string.', 'my-text-domain' ), array( 'status' => 400 ) );
    }

    // Get the registered attributes for this endpoint request.
    $attributes = $request->get_attributes();

    // Grab the filter param schema.
    $args = $attributes['args'][ $param ];

    // If the filter param is not a value in our enum then we should return an error as well.
    if ( ! in_array( $value, $args['enum'], true ) ) {
        return new WP_Error( 'rest_invalid_param', sprintf( __( '%s is not one of %s' ), $param, implode( ', ', $args['enum'] ) ), array( 'status' => 400 ) );
    }
}

/**
 * We can use this function to contain our arguments for the example product endpoint.
 */
function prefix_get_color_arguments() {
    $args = array();
    // Here we are registering the schema for the filter argument.
    $args['filter'] = array(
        // description should be a human readable description of the argument.
        'description' => esc_html__( 'The filter parameter is used to filter the collection of colors', 'my-text-domain' ),
        // type specifies the type of data that the argument should be.
        'type'        => 'string',
        // enum specified what values filter can take on.
        'enum'        => array( 'red', 'green', 'blue' ),
        // Here we register the validation callback for the filter argument.
        'validate_callback' => 'prefix_filter_arg_validate_callback',
    );
    return $args;
}

/**
 * This function is where we register our routes for our example endpoint.
 */
function prefix_register_example_routes() {
    // register_rest_route() handles more arguments but we are going to stick to the basics for now.
    register_rest_route( 'my-colors/v1', '/colors', array(
        // By using this constant we ensure that when the WP_REST_Server changes our readable endpoints will work as intended.
        'methods'  => WP_REST_Server::READABLE,
        // Here we register our callback. The callback is fired when this endpoint is matched by the WP_REST_Server class.
        'callback' => 'prefix_get_colors',
        // Here we register our permissions callback. The callback is fired before the main callback to check if the current user can access the endpoint.
        'args' => prefix_get_color_arguments(),
    ) );
}

add_action( 'rest_api_init', 'prefix_register_example_routes' );
```

<!-- 
#### Sanitizing
 -->
#### サニタイズ

<!-- 
In the above example, we do not need to use a `sanitize_callback`, because we are restricting input to only values in our enum. If we did not have strict validation and accepted any string as a parameter, we would definitely need to register a `sanitize_callback`. What if we wanted to update a content field and the user entered something like `alert('ZOMG Hacking you');`. The field value could potentially be a executable script. To strip out unwanted data or to transform data into a desired format we need to register a `sanitize_callback` for our arguments. Here is an example of how to use WordPress’s `sanitize_text_field()` for a sanitize callback:
 -->
上記の例では、入力を列挙型の値だけに制限しているため、`sanitize_callback` を使用する必要はありません。厳密なバリデーションを行わず、任意の文字列をパラメータとして受け付けるのであれば、間違いなく `sanitize_callback` を登録する必要があるでしょう。コンテンツ・フィールドを更新したいときに、ユーザーが `alert('ZOMG Hacking you');` のように入力したとしたらどうでしょう。フィールドの値は、実行可能なスクリプトである可能性があります。不要なデータを取り除いたり、データを希望するフォーマットに変換したりするには、引数に `sanitize_callback` を登録する必要があります。WordPress の `sanitize_text_field()` をサニタイズ・コールバックに使う例を示します:

```
/**
 * This is our callback function that embeds our resource in a WP_REST_Response.
 *
 * The parameter is already sanitized by this point so we can use it without any worries.
 */
function prefix_get_item( $request ) {
    if ( isset( $request['data'] ) ) {
        return rest_ensure_response( $request['data'] );
    }

    return new WP_Error( 'rest_invalid', esc_html__( 'The data parameter is required.', 'my-text-domain' ), array( 'status' => 400 ) );
}

/**
 * Validate a request argument based on details registered to the route.
 *
 * @param  mixed            $value   Value of the 'filter' argument.
 * @param  WP_REST_Request  $request The current request object.
 * @param  string           $param   Key of the parameter. In this case it is 'filter'.
 * @return WP_Error|boolean
 */
function prefix_data_arg_validate_callback( $value, $request, $param ) {
    // If the 'data' argument is not a string return an error.
    if ( ! is_string( $value ) ) {
        return new WP_Error( 'rest_invalid_param', esc_html__( 'The filter argument must be a string.', 'my-text-domain' ), array( 'status' => 400 ) );
    }
}

/**
 * Sanitize a request argument based on details registered to the route.
 *
 * @param  mixed            $value   Value of the 'filter' argument.
 * @param  WP_REST_Request  $request The current request object.
 * @param  string           $param   Key of the parameter. In this case it is 'filter'.
 * @return WP_Error|boolean
 */
function prefix_data_arg_sanitize_callback( $value, $request, $param ) {
    // It is as simple as returning the sanitized value.
    return sanitize_text_field( $value );
}

/**
 * We can use this function to contain our arguments for the example product endpoint.
 */
function prefix_get_data_arguments() {
    $args = array();
    // Here we are registering the schema for the filter argument.
    $args['data'] = array(
        // description should be a human readable description of the argument.
        'description' => esc_html__( 'The data parameter is used to be sanitized and returned in the response.', 'my-text-domain' ),
        // type specifies the type of data that the argument should be.
        'type'        => 'string',
        // Set the argument to be required for the endpoint.
        'required'    => true,
        // We are registering a basic validation callback for the data argument.
        'validate_callback' => 'prefix_data_arg_validate_callback',
        // Here we register the validation callback for the filter argument.
        'sanitize_callback' => 'prefix_data_arg_sanitize_callback',
    );
    return $args;
}

/**
 * This function is where we register our routes for our example endpoint.
 */
function prefix_register_example_routes() {
    // register_rest_route() handles more arguments but we are going to stick to the basics for now.
    register_rest_route( 'my-plugin/v1', '/sanitized-data', array(
        // By using this constant we ensure that when the WP_REST_Server changes our readable endpoints will work as intended.
        'methods'  => WP_REST_Server::READABLE,
        // Here we register our callback. The callback is fired when this endpoint is matched by the WP_REST_Server class.
        'callback' => 'prefix_get_item',
        // Here we register our permissions callback. The callback is fired before the main callback to check if the current user can access the endpoint.
        'args' => prefix_get_data_arguments(),
    ) );
}

add_action( 'rest_api_init', 'prefix_register_example_routes' );
```

<!-- 
## Summary
 -->
## 総括

<!-- 
We have covered the basics of registering endpoints for the WordPress REST API. Routes are the URIs that our endpoints live at. Endpoints are a collection of callbacks, methods, args, and other options. Each endpoint is mapped to a route when using `register_rest_route()`. An endpoint by default can support various HTTP methods, a main callback, a permissions callback, and registered arguments. We can register endpoints to cover any of our use cases for interacting with WordPress. The endpoints serve as the core interaction point with the REST API, but there are many other topics to explore and understand, to fully utilize this powerful API.
 -->
WordPress REST API のエンドポイント登録の基本を説明しました。ルートとは、エンドポイントが存在する URI のことです。エンドポイントは、コールバック、メソッド、引数、その他のオプションの集まりです。`register_rest_route()` を使用する場合、各エンドポイントは、ルートにマッピングされます。デフォルトのエンドポイントは、様々な HTTP メソッド、メイン・コールバック、パーミッション・コールバック、登録された引数をサポートできます。WordPress とやりとりするあらゆるユースケースをカバーするために、エンドポイントを登録できます。エンドポイントは、REST API とのやりとりの核となるものですが、この強力な API を十分に活用するためには、他にも探求し理解すべきトピックがたくさんあります。