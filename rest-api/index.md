<!-- 
# REST API
 -->
# REST API

<!-- 
WordPress 4.4 introduced the infrastructure for a REST API.  The REST API provides an easy way to get data into and out of WordPress.  Data can be retrieved and stored by sending HTTP requests to the REST API server.  The REST API takes advantage of different HTTP methods.
 -->
WordPress 4.4では、REST API の基盤が導入されました。REST API は、WordPress にデータを出し入れする簡単な方法を提供します。REST API サーバーに HTTP リクエストを送信することで、データを取得したり格納したりできます。REST API は、さまざまな HTTP メソッドを活用します。

<!-- 
- `GET` should be used for retrieving data from the API.
- `POST` should be used for creating new resources (i.e users, posts, taxonomies).
- `PUT` should be used for updating resources.
- `DELETE` should be used for deleting resources.
- `OPTIONS` should be used to provide context about our resources.
 -->
- `GET` は、API からデータを取得するために使用します。
- `POST` は、新しいリソース (ユーザー、投稿、タクソノミー、など) を作成するために使用されます。
- `PUT` は、リソースを更新するために使用されます。
- `DELETE` は、リソースを削除するために使用されます。
- `OPTIONS` は、リソースに関するコンテキストを提供するために使用されます。

<!-- 
A resource is any single entity or object.  A good example of a resource for WordPress would be a post. A post has different properties like its title and content.  A response from the API could show us title and content as fields in the response.  The REST API enables us to interact with posts and other WordPress resources  in a new way.  The REST API makes sharing our content with the rest of the web easier, and it provides us a structured way to handle complex interactions within WordPress.
 -->
リソースとは、単一のエンティティやオブジェクトのことです。WordPress のリソースの良い例は、投稿です。投稿には、タイトルや内容といったさまざまなプロパティがあります。API からのレスポンスでは、タイトルや内容が、フィールドとして表示されます。REST API は、投稿や他の WordPress リソースと、新しい方法でやりとりすることを可能にします。REST API は、私たちのコンテンツを他の Web と共有することを容易にし、WordPress 内で複雑なインタラクションを扱うための構造化された方法を提供してくれます。

<!-- 
In this chapter of the Plugin Handbook, we will explore how the API works and how we can leverage its power to do great things with WordPress!
 -->
プラグインハンドブックの本章では、API がどのように機能し、WordPress ですばらしいことをするために、API の力をどのように活用できるかを探ります !