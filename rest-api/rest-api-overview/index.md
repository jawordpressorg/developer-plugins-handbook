<!--
# REST API Overview
-->

# REST API 概要

<!--
The WordPress REST API brings many new features to WordPress. The REST API uses JSON (JavaScript Object Notation) as its data format.  JSON is an open standard data format that is becoming more widely used across the web as a whole, and software in general.  It is light-weight and human readable, and looks like Objects do in JavaScript; hence the name.  When you make a request to the API, the response will be returned in JSON. This enables developers to use WordPress in languages beyond PHP, which in turn allows WordPress to be used in new and exciting ways.
-->

WordPress REST API は、WordPress に多くの新機能をもたらします。REST API は、データフォーマットとして JSON (JavaScript Object Notation、JavaScript オブジェクト記法) を使用しています。JSON は、オープンスタンダードのデータフォーマットで、Web 全体やソフトウェア全般で広く使われるようになってきています。軽量で人間が読むことができ、JavaScript の Object のように見えます; これが名前の由来です。API にリクエストすると、レスポンスは JSON で返されます。これにより、開発者は PHP 以外の言語でも WordPress を使用できるようになり、WordPress を新しくエキサイティングな方法で使用できます。

<!--
## Why use the WordPress REST API
-->

## なぜ WordPress REST API を使用するのか

<!--
There are many use cases for the WordPress REST API.  One of the largest use cases is creating Single Page Applications on top of WordPress.  You could create an entirely new admin experience for WordPress, or you could create an entirely new front end experience for WordPress.  You would not even have to write the applications in PHP.  Any programming language that can make HTTP requests and interpret JSON could be used to write something on WordPress.
-->

WordPress REST API には、多くのユースケースがあります。最も大きなユースケースの一つは、WordPress 上に SPA (シングルページ・アプリケーション) を作成することです。WordPress のまったく新しい管理画面を作ったり、WordPress のまったく新しいフロントエンドを作ったりできます。アプリケーションを PHP で書く必要もありません。HTTP リクエストを行い、JSON を解釈できるプログラミング言語であれば、WordPress 上で何かを書くことができるのです。

<!--
The WordPress REST API can also serve as a strong replacement for the admin-ajax API in core.  By using the REST API, you can more easily structure the way you want to get data into and out of WordPress.  AJAX calls can be greatly simplified by using the REST API, enabling us to provide better user experiences in our work.
-->

WordPress REST API は、コアの admin-ajax API の強力な代替手段としても機能します。REST API を使うことで、WordPress にデータを出し入れする方法をより簡単に構造化できます。AJAX 呼び出しは、REST API を使用することで大幅に簡素化でき、より良いユーザー体験を提供できます。

<!--
The use cases extend beyond these and really our imagination is the only limit to what can be done.  The bottom line is, if you want an structured, extensible, and simple way to get data in and out of WordPress, you probably want to use the REST API.  The API, for all of its simplicity, can be quite complex at first and we will attempt to break it down into smaller components so that we can easily piece together the larger puzzle.
-->

ユースケースはこれら以外にもあり、私たちの想像力ができることの唯一の限界です。要するに、構造化され、拡張可能で、WordPress からデータを出し入れするシンプルな方法を求めるなら、おそらく REST API を使用したい、ということです。API はシンプルであるがゆえに、最初は非常に複雑かもしれません。ですので、より大きなパズルを簡単に組み立てることができるように、より小さな構成要素に分解することを試みます。

<!--
## Key Concepts
-->

## 主要コンセプト

<!--
To get started with using the WordPress REST API we will break down some of the key concepts and terms associated with the API:
-->

WordPress REST API を使い始めるために、API に関連する主要な概念と用語をいくつか説明します:

<!--
- Routes/Endpoints
- Requests
- Responses
- Schema
- Controller Classes
-->

- ルート/エンドポイント
- リクエスト
- レスポンス
- スキーマ
- コントローラ・クラス

<!--
Each of these concepts play a crucial role in using and understanding the WordPress REST API.  Let’s briefly break them down so that we can later explore each in greater depth.
-->

これらのコンセプトはそれぞれ、WordPress REST API を使い、理解するうえで重要な役割を果たします。後でそれぞれをより深く掘り下げることができるように、簡単に分解してみましょう。

<!--
### Routes & Endpoints
-->

### ルートとエンドポイント

<!--
A route, in the context of the WordPress REST API, is a URI which can be mapped to different HTTP methods.  The mapping of an individual HTTP method to a route is known as an endpoint.  To clarify: If we make a `GET` request to `http://oursite.com/wp-json/`, we will get a JSON response showing us what routes are available, and within each route, what endpoints are available. `/wp-json/` Is a route itself and when a `GET` request is made it matches to the endpoint that displays what is known as the index for the WordPress REST API. We will learn how to register our own routes and endpoints in the following sections.
-->

WordPress REST API の文脈におけるルートとは、異なる HTTP メソッドにマッピングできる URI のことです。個々の HTTP メソッドをルートにマッピングすることは、エンドポイントとして知られています。明確にすると: `http://oursite.com/wp-json/` に `GET` リクエストをすると、どのルートが利用可能か、そして、それぞれのルート内で、どのエンドポイントが利用可能かを示してくれる JSON レスポンスが返ってきます。`/wp-json/` はルートそのものであり、`GET` リクエストが行われると、WordPress REST API 用のインデックスと呼ばれるものを示すエンドポイントに合致します。次のセクションでは、独自のルートとエンドポイントを登録する方法を学びます。

<!--
### Requests
-->

### リクエスト

<!--
In the WordPress REST API infrastructure one of the primary classes is `WP_REST_Request`. The request class is used to store and retrieve information for the current request, requests can also be made internally within PHP to avoid using HTTP. `WP_REST_Request` objects are automatically generated for you whenever you make an HTTP request to a registered route. The data specified in the request will have an impact on what response you get back out of the API. There are a lot of neat things that can be done using the request class. The request section will go into greater detail.
-->

WordPress REST API 基盤には、主要なクラスのひとつに `WP_REST_Request` があります。リクエストクラスは、現在のリクエストの情報を格納したり取得したりするために使用され、HTTP を使用しないように PHP 内部でリクエストを行うこともできます。`WP_REST_Request` オブジェクトは、登録されたルートに HTTP リクエストを行うたびに自動的に生成されます。リクエストで指定したデータは、API から返されるレスポンスに影響します。リクエストクラスを使ってできることは実にたくさんあります。リクエストのセクションではさらに詳しく説明します。

<!--
### Responses
-->

### レスポンス

<!--
Responses are the data you get back from the API. The `WP_REST_Response` provides a way to interact with the response data returned by endpoints. Responses can return the desired data, and they can also be used to return errors.
-->

レスポンスは、API から返されるデータです。`WP_REST_Response` は、エンドポイントから返されるレスポンスデータを相互作用する方法を提供します。レスポンスは、必要なデータを返すことができ、エラーを返すためにも使用できます。

<!--
### Schema
-->

### スキーマ

<!--
When we have responses and requests of different kinds of data, we need to be able to tell what type of data we are interacting with. Schema provides us a way to structure our data. Schema also provides security benefits for the API as it enables us to validate requests being made to the API. Schema is a large topic and we will get into that in the schema section.
-->

さまざまな種類のデータに対するレスポンスやリクエストがある場合、どのような種類のデータと相互作用しているのかを見分けられるようにする必要があります。スキーマは、データを構造化する方法を提供してくれます。スキーマはまた、API へのリクエストを検証できるため、API にセキュリティの利点をもたらします。スキーマは大きなトピックですので、スキーマのセクションで説明することにしましょう。

<!--
### Controller Classes
-->

### コントローラ・クラス

<!--
As you can see the WordPress REST API has a lot of moving parts that all need to work together. Controller classes enable us to bring all of these elements together in a single place. With a controller class we will be able to manage the registering of routes & endpoints, handle requests, utilize schema, and generate responses.
-->

このように、WordPress REST API には多くの可動部分があり、それらがすべて連動する必要があります。コントローラクラスは、これらすべての要素をひとつの場所にまとめることを可能にします。コントローラクラスがあれば、ルートやエンドポイントの登録、リクエストの処理、スキーマの利用、レスポンスの生成などを管理できます。

<!--
## Next Steps
-->

## 次のステップ

<!--
Let’s dive into how to register routes and endpoints for the REST API.
-->

REST API のルートとエンドポイントを登録する方法を説明しましょう。
