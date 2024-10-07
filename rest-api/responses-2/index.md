<!-- 
# Responses
 -->
# レスポンス

<!-- 
## Overview
 -->
## 概要

<!-- 
Responses in the API are what holds all of the data we want. If we made a mistake in our request, our response’s data should also inform us that an error occurred. Responses in the WordPress REST API should return the data we requested or an error message. Responses in the API are handled by the `WP_REST_Response` class, one of the three infrastructural classes for the API.
 -->
API に於けるレスポンスとは、我々が欲しい全てのデータを保持しているものです。リクエストにミスがあった場合、レスポンスのデータもエラーが発生したことを知らせてくれるものです。WordPress REST API のレスポンスは、リクエストしたデータかエラーメッセージを返します。API に於けるレスポンスは、API のための3つの基盤クラスの1つであるクラス `WP_REST_Response` によって処理されます。

<!-- 
## WP_REST_Response
 -->
## WP_REST_Response

<!-- 
The `WP_REST_Response` extends WordPress’s `WP_HTTP_Response` class, allowing us access to response headers, response status code, and response data.
 -->
`WP_REST_Response` は、WordPress のクラス `WP_HTTP_Response` を継承しており、レスポンス・ヘッダー、レスポンス・ステータスコード、レスポンス・データにアクセスできるようになっています。

```
// The following code will not do anything and just serves as a demonstration.
$response = new WP_REST_Response( 'This is some data' );

// To get the response data we can use this method. It should equal 'This is some data'.
$our_data = $response->get_data();

// To access the HTTP status code we can use this method. The most common status code is probably 200, which means OK!
$our_status = $response->get_status();

// To access the HTTP response headers we can use this method.
$our_headers = $response->get_headers();
```

<!-- 
The above is pretty straightforward and shows you how to get what you need out of a response. The `WP_REST_Response` takes things a bit further. You can access the matched route for the response to backtrack which endpoint the response came from with `$response->get_matched_route()`. `$response->get_matched_handler()` will return the options registered for the endpoint that produced our response. These could be useful for logging the API among other things. The response class also helps us with error handling.
 -->
上記は非常にわかりやすく、レスポンスから必要なものを得る方法を示しています。`WP_REST_Response` は、もう少し踏み込んで説明しています。`$response->get_matched_route()` を使うと、レスポンスの一致したルートにアクセスして、レスポンスがどのエンドポイントから来たのかを追跡できます。`$response->get_matched_handler()` は、レスポンスを生成したエンドポイントに登録されているオプションを返します。これらはとりわけ API のロギングに役立つでしょう。レスポンスクラスは、エラー処理にも役に立つでしょう。

<!-- 
### Error Handling
 -->
### エラー処理

<!-- 
If something went terribly wrong in our request, we can return `WP_Error` objects in our endpoint callbacks explaining what went wrong, like this:
 -->
リクエストの中で何かが大きく間違っていた場合、この様に、何が間違っていたのかを説明するために、エンドポイント・コールバックで `WP_Error` オブジェクトを返すことがでます:

```
// Register our mock batch endpoint.
function prefix_register_broken_route() {
    register_rest_route( 'my-namespace/v1', '/broken', array(
        // Supported methods for this endpoint. WP_REST_Server::READABLE translates to GET.
        'methods' => WP_REST_Server::READABLE,
        // Register the callback for the endpoint.
        'callback' => 'prefix_get_an_error',
    ) );
}

add_action( 'rest_api_init', 'prefix_register_broken_route' );

/**
 * Our registered endpoint callback. Notice how we are passing in $request as an argument.
 * By default, the WP_REST_Server will pass in the matched request object to our callback.
 *
 * @param WP_REST_Request $request The current matched request object.
 */
function prefix_get_an_error( $request ) {
    return new WP_Error( 'oops', esc_html__( 'This endpoint is currently broken, try another endpoint, I promise the API is cool! EEEK!!!!', 'my-textdomain' ), array( 'status' => 400 ) );
}
```

<!-- 
That is kind of a silly example but it touches on some key things. The most important thing to understand is that the WordPress REST API will automatically handle changing the [WP\_Error](https://developer.wordpress.org/reference/classes/wp_error/) object into an HTTP Response containing your data. When you set the status code in the `WP_Error` object your HTTP response status code will take on that value. This comes in really handy when you need to use different error codes like 404 for content that wasn’t found, or 403 for forbidden access. All we have to do is have our endpoint callbacks return a request and the `WP_REST_Server` class will handle a lot of really important things for us.
 -->
これは馬鹿げた例だが、いくつかの重要なことに触れておきたい。理解すべき最も重要なことは、WordPress REST API は自動的に [WP\_Error](https://developer.wordpress.org/reference/classes/wp_error/) オブジェクトを、あなたのデータを含む HTTP レスポンスに変更する処理を行うということです。`WP_Error` オブジェクトにステータスコードを設定すると、HTTP レスポンスのステータスコードがその値になります。これは、コンテンツが見つからなかった際の404や、アクセスが禁止されている際の403など、様々なエラーコードを使い分ける必要がある場合にとても便利です。エンドポイント・コールバックがリクエストを返すようにするだけで、クラス `WP_REST_Server` が本当に重要なことをたくさん処理してくれます。

<!-- 
There are other cool things the response class can help us with, like Linking.
 -->
レスポンス・クラスが助けてくれるクールなことは、リンクとか、まだ他にもあります。

<!-- 
## Linking
 -->
## リンク

<!-- 
What if we wanted to get a post and the first comment for that post? Would we write a separate endpoint to handle this use case? If we did that, we would need to start adding a lot of endpoints to handle various small use cases and our API index would get bloated really fast. Response Linking provides us a way to form relations between our resources that the API can understand. The API implements a standard known as HAL for resource linking. Let’s look at our post and comment example, it would be better to have routes for each resource.
 -->
投稿とその投稿に対する最初のコメントを取得したい場合はどうすればいいでしょうか ? このユースケースを扱うために別のエンドポイントを書くでしょうか ? そんなことをしたら、様々な小さなユースケースを処理するために、たくさんのエンドポイントを追加し始めなければならなくなり、API インデックスはあっという間に肥大化していくことになるでしょう。レスポンス・リンクは、API が理解できるリソース間の関係を形成する方法を提供してくれます。API はリソースリンク用に HAL として知られる標準を実装しています。投稿とコメントの例を見てみましょう。各リソースに対してルートを持つほうがよいでしょう。

<!-- 
Let’s say we have post with ID = 1 and comment ID = 3. The comment is assigned to post 1, so realistically the two resources could live at the routes `/my-namespace/v1/posts/1` and `/my-namespace/v1/comments/3`. We would add links to the responses to create the relationships between them. Let’s look at this from the comment perspective first.
 -->
例えば、`ID = 1` と `comment ID = 3` の投稿があったとしましょう。コメントは `post 1` に割り当てられているので、現実的には2つのリソースは `/my-namespace/v1/posts/1` と `/my-namespace/v1/comments/3` のルートに存在することになります。レスポンスにリンクを追加して、レスポンス間のリレーションを作成します。まずはコメントの観点から見てみましょう。

```
// Register our mock endpoints.
function prefix_register_my_routes() {
    register_rest_route( 'my-namespace/v1', '/posts/(?P<id>[\d]+)', array(
        // Supported methods for this endpoint. WP_REST_Server::READABLE translates to GET.
        'methods' => WP_REST_Server::READABLE,
        // Register the callback for the endpoint.
        'callback' => 'prefix_get_rest_post',
    ) );
    register_rest_route( 'my-namespace/v1', '/comments', array(
        // Supported methods for this endpoint. WP_REST_Server::READABLE translates to GET.
        'methods' => WP_REST_Server::READABLE,
        // Register the callback for the endpoint.
        'callback' => 'prefix_get_rest_comments',
        // Register the post argument to limit results to a specific post parent.
        'args' => array(
            'post' => array(
                'description' => esc_html__( 'The post ID that the comment is assigned to.', 'my-textdomain' ),
                'type'        => 'integer',
                'required'    => true,
            ),
        ),
    ) );
    register_rest_route( 'my-namespace/v1', '/comments/(?P<id>[\d]+)', array(
        // Supported methods for this endpoint. WP_REST_Server::READABLE translates to GET.
        'methods' => WP_REST_Server::READABLE,
        // Register the callback for the endpoint.
        'callback' => 'prefix_get_rest_comment',
    ) );
}

add_action( 'rest_api_init', 'prefix_register_my_routes' );

// Grab a post.
function prefix_get_rest_post( $request ) {
    $id = (int) $request['id'];
    $post = get_post( $id );

    $response = rest_ensure_response( array( $post ) );

    $response->add_links( prefix_prepare_post_links( $post ) );

    return $response;
}

// Prepare post links.
function prefix_prepare_post_links( $post ) {
    $links = array();

    $replies_url = rest_url( 'my-namespace/v1/comments' );
    $replies_url = add_query_arg( 'post', $post->ID, $replies_url );
    $links['replies'] = array(
		'href'         => $replies_url,
		'embeddable'   => true,
    );

    return $links;
}

// Grab a comments.
function prefix_get_rest_comments( $request ) {
    if ( ! isset( $request['post'] ) ) {
        return new WP_Error( 'rest_bad_request', esc_html__( 'You must specify the post parameter for this request.', 'my-text-domain' ), array( 'status' => 400 ) );
    }

    $data = array();

    $comments = get_comments( array( 'post__in' => $request['post'] ) );

    if ( empty( $comments ) ) {
        return array();
    }

    foreach( $comments as $comment ) {
        $response = rest_ensure_response( $comment );
        $response->add_links( prefix_prepare_comment_links( $comment ) );
        $data[] = prefix_prepare_for_collection( $response );
    }

    $response = rest_ensure_response( $data );
    return $response;
}

// Grab a comment.
function prefix_get_rest_comment( $request ) {
    $id = (int) $request['id'];
    $post = get_comment( $id );

    $response = rest_ensure_response( $comment );

    $response->add_links( prefix_prepare_comment_links( $comment ) );

    return $response;
}

// Prepare comment links.
function prefix_prepare_comment_links( $comment ) {
    $links = array();
    if ( 0 !== (int) $comment->comment_post_ID ) {
        $post = get_post( $comment->comment_post_ID );
        if ( ! empty( $post->ID ) ) {
        $links['up'] = array(
                'href'       => rest_url( 'my-namespace/v1/posts/' . $comment->comment_post_ID ),
                'embeddable' => true,
                'post_type'  => $post->post_type,
            );
        }
    }
    return $links;
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
```

<!-- 
As you can see in the example above we are using links to create the relations between our resources. If the post has comments, our endpoint callback will add a link to the comments route specifying the \`post\` parameter to match our current post ID. So if you were to follow that route you would now get the comments that have that assigned post ID. If you search for comments then each comment will have a link point \`up\` to the post. \`up\` has special meaning in links using the HAL spec. If we follow an up link for a comment then we will be returned the post that is the comment parent. Linking is pretty awesome, but it gets better.
 -->
上の例でわかるように、リンクを使ってリソース間のリレーションを作成しています。投稿にコメントがある場合、エンドポイント・コールバックは、現在の投稿 ID に合わせてパラメータ「\`post\`」を指定してコメントルートにリンクを追加します。つまり、そのルートを辿れば、その割り当てられた投稿 ID を持つコメントを得ることができるのです。コメントを検索すると、それぞれのコメントに投稿へのリンクポイント「\`up\`」が表示されます。「\`up\`」は、HAL スペックを使用するリンクに於いては、特別な意味を持ちます。コメントのアップリンクを辿れば、コメントの親である投稿が返されるのです。リンクはとても素晴らしいが、さらに良いことがあります。

<!-- 
The WordPress REST API also supports what is referred to as embedding. If you notice in both of the links we added, we specified that `embeddable => true`. This enables us to embed our linked data in our responses. So if we wanted to grab comment 3 and its assigned post we could make this request `https://ourawesomesite.com/wp-json/my-namespace/v1/comments/3?_embed`. The `_embed` parameter tells the API we want all of the embeddable resource links for our request to also be added to the API. Using embed is a performance gain as the multiple resources are all handled in one HTTP Request.
 -->
WordPress REST API は、いわゆる埋め込みにも対応しています。追加したリンクの両方で、`embeddable => true` と指定していることにお気付きでしょうか。これにより、リンク先のデータをレスポンスに埋め込むことができます。これにより、リンク先のデータをレスポンスに埋め込むことができます。つまり、`comment 3` とその割り当てられた投稿を取得したい場合、`https://ourawesomesite.com/wp-json/my-namespace/v1/comments/3?_embed` とリクエストできるのです。パラメータ `_embed` は、リクエストに対する埋め込み可能なリソースリンクがすべて欲しいということも、API に追加する様、API に指示します。embed を使用すると、複数のリソースが1つの HTTP リクエストで処理されるため、パフォーマンスが向上します。

<!-- 
Smart use of embedding and links make the WordPress REST API incredibly flexible and powerful for interacting with WordPress.
 -->
埋め込みとリンクを賢く使うことで、WordPress REST API は WordPress とやりとりするための信じられないほど柔軟で強力なものになります。