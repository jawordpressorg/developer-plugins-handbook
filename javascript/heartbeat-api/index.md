<!--
# Heartbeat API
-->

# ハートビート API

<!--
The Heartbeat API is a simple server polling API built in to WordPress, allowing near-real-time frontend updates.
-->

ハートビート API は、WordPress に組み込まれたシンプルなサーバーポーリング API で、フロントエンドの更新をほぼリアルタイムで行うことができます。

<!--
## How it works
-->

## しくみ

<!--
When the page loads, the client-side heartbeat code sets up an interval (called the "tick") to run every 15-120 seconds. When it runs, heartbeat gathers data to send via a jQuery event, then sends this to the server and waits for a response. On the server, an admin-ajax handler takes the passed data, prepares a response, filters the response, then returns the data in JSON format. The client receives this data and fires a final jQuery event to indicate the data has been received.
-->

ページがロードされると、15～120秒ごとに、クライアント側のハートビート・コードは、(「ティック」と呼ばれる) 実行間隔を設定します。実行されると、ハートビートは、jQuery イベントで送信するデータを収集し、これをサーバーに送信してレスポンスを待ちます。サーバーでは、admin-ajax ハンドラーが渡されたデータを受け取り、レスポンスを準備し、レスポンスをフィルタリングして、JSON フォーマットでデータを返します。クライアントは、このデータを受け取り、データを受け取ったことを示す最後の jQuery イベントを発生させます。

<!--
The basic process for custom Heartbeat events is:
-->

カスタム・ハートビート・イベントの基本的なプロセスは、以下の通りです:

<!--
1. Add additional fields to the data to be sent (JS `heartbeat-send` event).
2. Detect sent fields in PHP, and add additional response fields (`heartbeat_received` filter).
3. Process returned data in JS (JS `heartbeat-tick`).
-->

1. 送信するデータに、フィールドを追加します (JS `heartbeat-send` イベント)。
2. PHP で送信済みフィールドを検出し、レスポンスフィールドを追加します (`heartbeat_received` フィルター)。
3. 返されたデータを JS で処理します (JS `heartbeat-tick`)。

<!--
(You can choose to use only one or two of these events, depending on what functionality you need.)
-->

(必要な機能に応じて、これらのイベントのうち、1つまたは2つだけを使用できます)

<!--
## Using the API
-->

## API の使用

<!--
Using the heartbeat API requires two separate pieces of functionality: send and receive callbacks in JavaScript, and a server-side filter to process passed data in PHP.
-->

ハートビート API を使用するには、2つの別々な機能が必要です: JavaScript での送受信コールバック、そして、PHP で渡されたデータを処理するサーバー側フィルターです。

<!--
### Sending Data to the Server
-->

### サーバーへのデータ送信

<!--
When Heartbeat sends data to the server, you can include custom data. This can be any data you want to send to the server, or a simple true value to indicate you are expecting data.
-->

ハートビートがサーバーにデータを送信する際に、カスタムデータを含めることができます。これは、サーバーに送信したい任意のデータでも、データを期待していることを示す単純な true 値でもかまいません。

```
jQuery( document ).on( 'heartbeat-send', function ( event, data ) {
  // Add additional data to Heartbeat data.
  data.myplugin_customfield = 'some_data';
});
```

<!--
### Receiving and Responding on the Server
-->

### サーバーでの受信と応答

<!--
On the server side, you can then detect this data, and add additional data to the response.
-->

サーバー側では、このデータを検出し、レスポンスに追加データを加えることができます。

```
/**
 * Receive Heartbeat data and respond.
 *
 * Processes data received via a Heartbeat request, and returns additional data to pass back to the front end.
 *
 * @param array $response Heartbeat response data to pass back to front end.
 * @param array $data     Data received from the front end (unslashed).
 *
 * @return array
 */
function myplugin_receive_heartbeat( array $response, array $data ) {
  // If we didn't receive our data, don't send any back.
  if ( empty( $data['myplugin_customfield'] ) ) {
    return $response;
  }

  // Calculate our data and pass it back. For this example, we'll hash it.
  $received_data = $data['myplugin_customfield'];

  $response['myplugin_customfield_hashed'] = sha1( $received_data );
  return $response;
}
add_filter( 'heartbeat_received', 'myplugin_receive_heartbeat', 10, 2 );
```

<!--
Back on the frontend, you can then handle receiving this data back.
-->

フロントエンドに戻れば、このデータを受け取ることができます。

```
jQuery( document ).on( 'heartbeat-tick', function ( event, data ) {
  // Check for our data, and use it.
  if ( ! data.myplugin_customfield_hashed ) {
    return;
  }

  alert( 'The hash is ' + data.myplugin_customfield_hashed );
});
```

<!--
Not every feature will need all three of these steps. For example, if you don’t need to send any data to the server, you can use just the latter two steps.
-->

すべての機能が、これら3つのステップすべてを必要とするわけではありません。たとえば、サーバーにデータを送信する必要がない場合は、後の2つのステップだけを使用できます。
