<!-- 
## Adding the Personal Data Exporter to Your Plugin
 -->
## プラグインに個人データ・エクスポーターの追加

<!-- 
In WordPress 4.9.6, new tools were added to make compliance easier with laws like the European Union's General Data Protection Regulation, or GDPR for short. Among the tools added is a Personal Data Export tool which supports exporting all the personal data for a given user in a ZIP file. In addition to the personal data stored in things like WordPress comments, plugins can also hook into the exporter feature to export the personal data they collect, whether it be in something like postmeta or even an entirely new Custom Post Type (CPT).
 -->
WordPress 4.9.6では、欧州連合 (EU) の一般データ保護規則 (General Data Protection Regulation、略して GDPR) のような法律への準拠を容易にするための新しいツールが追加されました。追加されたツールの中には、指定したユーザーのすべての個人データを ZIP ファイルに書き出すことをサポートする、個人データ書き出しツールがあります。WordPress のコメントなどに保存された個人データに加えて、プラグインもまたエクスポーター機能にフックして、自身が収集した個人データ - 投稿メタから、まったく新規のカスタム投稿タイプさえも - を書き出すことができます。

<!-- 
The "key" for all the exports is the user's email address – this was chosen because it supports exporting personal data for both full-fledged registered users and also unregistered users (e.g. like a logged out commenter).
 -->
すべての書き出しの「キー」は、ユーザーのメールアドレスです – これは、本格的な登録ユーザーだけでなく、未登録ユーザー (たとえば、ログアウトしたコメント投稿者など) の個人データの書き出しにも対応しているためです。

<!-- 
However, since assembling a personal data export could be an intensive process and will likely contain sensitive data, we don't want to just generate it and email it to the requestor without confirming the request, so the admin-facing user interface starts all requests by having the admin enter the username or email address making the request and then sends then a link to click to confirm their request.
 -->
しかし、個人データの書き出しを作成するのは集中的なプロセスであり、機密データを含む可能性が高いため、リクエストを確認することなく、ただデータを生成してリクエスト者にメールで送信することはしたくありません。そのため、管理者向けのユーザーインターフェイスでは、管理者がリクエストを行うユーザー名またはメールアドレスを入力し、リクエストを確認するためにクリックするリンクを送信することで、すべてのリクエストを開始します。

<!-- 
Once a request has been confirmed, the admin can generate and download or directly email the personal data export ZIP file for the user, or do the export anyways if the need arises. Inside the ZIP file the user receives, they will find a "mini website" with an index HTML page containing their personal data organized in groups (e.g. a group for comments, etc. )
 -->
リクエストが確認されると、管理者はユーザーの個人データ書き出し ZIP ファイルを生成してダウンロードするか、直接メールで送信するか、または、必要に応じて書き出しを行うことができます。ユーザーが受け取る ZIP ファイルの中には、個人データをグループ (たとえば、コメントのグループなど) に編成したインデックス HTML ページを含む「ミニ Web サイト」があります。

<!-- 
Whether the admin downloads the personal data export ZIP file or sends it directly to the requestor, the way the personal data export is assembled is identical – and relies on hooking "exporter" callbacks to do the dirty work of collecting all the data for the export. When the admin clicks on the download or email link, an AJAX loop begins that iterates over all the exporters registered in the system, one at a time. In addition to exporters built into core, plugins can register their own exporter callbacks.
 -->
管理者が個人データ書き出し ZIP ファイルをダウンロードしても、要求者に直接送信しても、個人データ書き出しの組み立て方は同じです – そして、書き出すためのすべてのデータを収集する汚れ仕事をするために、「exporter」コールバックをフックすることに依存しています。管理者がダウンロードまたは電子メールのリンクをクリックすると、AJAX ループが始まり、システムに登録されているすべてのエクスポーターを一度に1つずつ繰り返します。コアに内蔵されたエクスポーターに加えて、プラグインは独自のエクスポーター・コールバックを登録できます。

<!-- 
The exporter callback interface is designed to be as simple as possible. A exporter callback receives the email address we are working with and a page parameter as well. The page parameter (which starts at 1) is used to avoid plugins potentially causing timeouts by attempting to export all the personal data they've collected at once. A well behaved plugin will limit the amount of data it attempts to erase per page (e.g. 100 posts, 200 comments, etc.)
 -->
エクスポーター・コールバックのインターフェースはできるだけシンプルに設計されています。エクスポーター・コールバックは、扱うメールアドレスとページパラメータを受け取ります。(1から始まる) ページパラメータは、プラグインが収集したすべての個人データを一度に書き出そうとしてタイムアウトを引き起こす可能性を避けるために使用されます。お行儀の良いプラグインは、ページごとに消去しようとするデータ量を制限します (たとえば、100投稿、200コメントなど)。

<!-- 
The exporter callback replies with whatever data it has for that email address and page and whether it is done or not. If a exporter callback reports that it is not done, it will be called again (in a separate request) with the page parameter incremented by 1. Exporter callbacks are expected to return an array of items for the export. Each item contains an a group identifier for the group of which the item is a part (e.g. comments, posts, orders, etc.), an optional group label (translated), an item identifier (e.g. comment-133) and then an array of name, value pairs containing the data to be exported for that item.
 -->
エクスポーター・コールバックは、そのメールアドレスとページが完了したかどうかのデータを返します。エクスポーター・コールバックが完了していないことを報告した場合、ページパラメータを1増やして (別のリクエストで) 再度呼び出されます。エクスポーター・コールバックは、書き出されるアイテムの配列を返すことが期待されています。各項目には、そのアイテムが属するグループ (たとえば、コメント、投稿、注文など)、省略可能なグループラベル (翻訳済み)、アイテムの識別子 (たとえば、comment-133)、そしてそのアイテムの書き出されるデータを含む名前と値のペアの配列、のグループ識別子が含まれます。

<!-- 
It is noteworthy that the value could be a media path, in which case a link to the media file will be added to the index HTML page in the export.
 -->
注目すべきは、この値がメディア・パスである可能性があることで、この場合、メディアファイルへのリンクが書き出しのインデックス HTML ページに追加されます。

<!-- 
When all the exporters have been called to completion, WordPress first assembles an "index" HTML document that serves as the heart of the export report. If a plugin reports additional data for an item that WordPress or another plugin has already added, all the data for that item will be presented together.
 -->
すべてのエクスポーターが完了するまで呼び出されると、WordPress はまず、書き出しレポートの中心となる「インデックス」HTML ドキュメントを作成します。WordPress や他のプラグインがすでに追加したアイテムについて、プラグインが追加データを報告する場合、そのアイテムについてのすべてのデータが一緒に表示されます。

<!-- 
Exports are cached on the server for 3 days and then deleted.
 -->
書き出しは3日間サーバーにキャッシュされ、その後削除されます。

<!-- 
A plugin can register one or more exporters, but most plugins will only need one. Let's work on a hypothetical plugin which adds location data for the commenter to comments.
 -->
プラグインは1つ以上のエクスポーターを登録できますが、ほとんどのプラグインは1つだけでよいでしょう。コメント投稿者の位置情報をコメントに追加するプラグインを想定してみましょう。

<!-- 
First, let's assume the plugin has used [`add_comment_meta`](https://developer.wordpress.org/reference/functions/add_comment_meta/) to add location data using `meta_key`'s of `latitude` and `longitude`.
 -->
まず、プラグインが [`add_comment_meta`](https://developer.wordpress.org/reference/functions/add_comment_meta/) を使って `meta_key` の `latitude` と `longitude` を用いて位置情報を追加したとします。

<!-- 
The first thing the plugin needs to do is to create an exporter function that accepts an email address and a page, e.g.:
 -->
プラグインが最初に行う必要があるのは、メールアドレスとページを受け付けるエクスポーター関数を作成することです:

```
/**
 * Export user meta for a user using the supplied email.
 *
 * @param string $email_address   email address to manipulate
 * @param int    $page            pagination
 *
 * @return array
 */
function wporg_export_user_data_by_email( $email_address, $page = 1 ) {
  $number = 500; // Limit us to avoid timing out
  $page   = (int) $page;

  $export_items = array();

  $comments = get_comments(
    array(
      'author_email' => $email_address,
      'number'       => $number,
      'paged'        => $page,
      'order_by'     => 'comment_ID',
      'order'        => 'ASC',
    )
  );

  foreach ( (array) $comments as $comment ) {
    $latitude  = get_comment_meta( $comment->comment_ID, 'latitude', true );
    $longitude = get_comment_meta( $comment->comment_ID, 'longitude', true );

    // Only add location data to the export if it is not empty.
    if ( ! empty( $latitude ) ) {
      // Most item IDs should look like postType-postID. If you don't have a post, comment or other ID to work with,
      // use a unique value to avoid having this item's export combined in the final report with other items
      // of the same id.
      $item_id = "comment-{$comment->comment_ID}";

      // Core group IDs include 'comments', 'posts', etc. But you can add your own group IDs as needed
      $group_id = 'comments';

      // Optional group label. Core provides these for core groups. If you define your own group, the first
      // exporter to include a label will be used as the group label in the final exported report.
      $group_label = __( 'Comments', 'text-domain' );

      // Plugins can add as many items in the item data array as they want.
      $data = array(
        array(
          'name'  => __( 'Commenter Latitude', 'text-domain' ),
          'value' => $latitude,
        ),
        array(
          'name'  => __( 'Commenter Longitude', 'text-domain' ),
          'value' => $longitude,
        ),
      );

      $export_items[] = array(
        'group_id'    => $group_id,
        'group_label' => $group_label,
        'item_id'     => $item_id,
        'data'        => $data,
      );
    }
  }

  // Tell core if we have more comments to work on still.
  $done = count( $comments ) > $number;
  return array(
    'data' => $export_items,
    'done' => $done,
  );
}
```

<!-- 
The next thing the plugin needs to do is to register the callback by filtering the exporter array using the [`wp_privacy_personal_data_exporters`](https://developer.wordpress.org/reference/hooks/wp_privacy_personal_data_exporters/) filter.
 -->
次にプラグインが行うべきことは、フィルター [`wp_privacy_personal_data_exporters`](https://developer.wordpress.org/reference/hooks/wp_privacy_personal_data_exporters/) を使用してエクスポーター配列をフィルタリングしてコールバックを登録することです。

<!-- 
When registering you provide a friendly name for the export (to aid in debugging – this friendly name is not shown to anyone at this time) and the callback, e.g.
 -->
登録の際には、書き出しのためのフレンドリーな名前 (デバッグを助けるため - このフレンドリーな名前は、現時点では誰にも表示されません) とコールバックを指定します。

```
/**
 * Registers all data exporters.
 *
 * @param array $exporters
 *
 * @return mixed
 */
function wporg_register_user_data_exporters( $exporters ) {
  $exporters['my-plugin-slug'] = array(
    'exporter_friendly_name' => __( 'Comment Location Plugin', 'text-domain' ),
    'callback'               => 'my_plugin_exporter',
  );
  return $exporters;
}

add_filter( 'wp_privacy_personal_data_exporters', 'wporg_register_user_data_exporters' );
```

<!-- 
And that's all there is to it! Your plugin will now provide data for the export!
 -->
以上で完了です ! これで、プラグインが書き出し用のデータを提供します !
