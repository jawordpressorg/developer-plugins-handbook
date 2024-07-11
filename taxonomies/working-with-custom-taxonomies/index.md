<!-- 
# Working with Custom Taxonomies
 -->
# カスタムタクソノミーの操作

<!-- 
## Introduction to Taxonomies
 -->
## タクソノミーの概要

<!-- 
To understand what Taxonomies are and what they do please read the [Taxonomy](https://developer.wordpress.org/plugins/taxonomies/) introduction.
 -->
タクソノミーとは何か、タクソノミーが何をするのかについて理解するには、[タクソノミー](https://developer.wordpress.org/plugins/taxonomies/)概要をお読みください。

<!-- 
## Custom Taxonomies
 -->
## カスタムタクソノミー

<!-- 
As classification systems go, "Categories" and "Tags" aren't very structured, so it may be beneficial for a developer to create their own.
 -->
分類システムとしては、「カテゴリー」と「タグ」はあまり構造化されていないので、開発者が独自に作成することは有益かもしれません。

<!-- 
WordPress allows developers to create **Custom Taxonomies**. Custom Taxonomies are useful when one wants to create distinct naming systems and make them accessible behind the scenes in a predictable way.
 -->
WordPress では、開発者が**カスタムタクソノミー**を作成できます。カスタムタクソノミーは、明確なネーミングシステムを作成し、予測可能な方法で舞台裏からアクセスできるようにしたい場合に便利です。

<!-- 
## Why Use Custom Taxonomies?
 -->
## どうしてカスタムタクソノミーを使うの ?

<!-- 
You might ask, "Why bother creating a Custom Taxonomy, when I can organize by Categories and Tags?"
 -->
「カテゴリーやタグで分類できるのに、なぜわざわざカスタムタクソノミーを作成するの ?」と疑問に思うかもしれません。

<!-- 
Well… let's use an example. Suppose we have a client that is a chef who wants you to create a website where she'll feature original recipes.
 -->
さて…例を挙げましょう。シェフであるクライアントが、オリジナルレシピを紹介する Web サイトを作ってほしいと依頼したとします。

<!-- 
One way to organize the website might be to create a Custom Post Type called "Recipes" to store her recipes. Then create a Taxonomy "Courses" to separate "Appetizers" from "Desserts", and finally a Taxonomy "Ingredients" to separate "Chicken" from "Chocolate" dishes.
 -->
Web サイトを編成する一つの方法として、彼女のレシピの格納にカスタム投稿タイプ「レシピ」を作成する方法があります。タクソノミー「コース」を作成して「前菜」と「デザート」を分け、タクソノミー「食材」を作成して「チキン」と「チョコレート」の料理を分けます。

<!-- 
These groups _could_ be defined using Categories or Tags, you could have a "Courses" Category with Subcategories for "Appetizers" and "Desserts", and an "Ingredients" Category with Subcategories for each ingredient.
 -->
これらのグループは、カテゴリーやタグを使っても定義することが「可能」です。例えばカテゴリー「コース」にサブカテゴリー「前菜」と「デザート」を作成し、カテゴリー「食材」に各食材のサブカテゴリーを作成します。

<!-- 
The main advantage of using Custom Taxonomies is that you can reference "Courses" and "Ingredients" independently of Categories and Tags. They even get their own menus in the Administration area.
 -->
カスタムタクソノミーを使う主な利点は、「コース」と「食材」をカテゴリーやタグとは別に参照できることです。さらに、管理エリアに独自のメニューも用意されています。

<!-- 
In addition, creating Custom Taxonomies allows you to build custom interfaces which will ease the life of your client and make the process of inserting data intuitive to their business nature.
 -->
さらに、カスタムタクソノミーを作成することで、データを挿入するプロセスをクライアントのビジネスの性質に合わせて直感的に行うことができるカスタムインターフェースを構築し、クライアントの生活を楽にできます。

<!-- 
Now imagine that these Custom Taxonomies and the interface is implemented inside a plugin; you've just built your own Recipes plugin that can be reused on any WordPress website.
 -->
これらのカスタムタクソノミーとインターフェイスが、プラグインの中に実装されているとします。どの WordPress サイトでも再利用できる独自のレシピ・プラグインができあがりました。

<!-- 
## Example: Courses Taxonomy
 -->
## 例: タクソノミー「コース」

<!-- 
The following example will show you how to create a plugin which adds a Custom Taxonomy "Courses" to the default `post` Post Type. Note that the code to add custom taxonomies does not have to be in its own plugin; it can be included in a theme or as part of an existing plugin if desired.
 -->
以下の例では、デフォルトの投稿タイプ `post` に、カスタムタクソノミー「コース」を追加するプラグインの作成方法を紹介します。カスタムタクソノミーを追加するコードは、プラグインに含める必要はないことに注意してください。必要であれば、テーマや既存のプラグインの一部に含めることができます。

<!-- 
Please make sure to read the [Plugin Basics](https://developer.wordpress.org/plugins/plugin-basics/) chapter before attempting to create your own plugin.
 -->
独自のプラグインを作ろうとする前に、必ず[プラグインの基本](https://developer.wordpress.org/plugins/plugin-basics/)の章を読んでください。

<!-- 
### Step 1: Before You Begin
 -->
### ステップ1: 始める前に

<!-- 
Go to **Posts > Add New** page. You will notice that you only have Categories and Tags.
 -->
**投稿 > 新規投稿を追加**ページに移動します。カテゴリーとタグしかないことに気付くでしょう。

<!-- 
![No Custom Taxonomy Meta Box (Yet)](https://make.wordpress.org/docs/files/2014/02/no-custom-taxonomy-meta-box.png)
 -->
![カスタムタクソノミーのメタボックスは (まだ) 存在しません](https://make.wordpress.org/docs/files/2014/02/no-custom-taxonomy-meta-box.png)

<!-- 
## Step 2: Creating a New Plugin
 -->
## ステップ2: 新しいプラグインの作成

<!-- 
Register the Taxonomy "course" for the post type "post" using the `init` action hook.
 -->
アクションフック `init` を使って、タクソノミー「course」を投稿タイプ「post」に登録します。

```
/*
 * Plugin Name: Course Taxonomy
 * Description: A short example showing how to add a taxonomy called Course.
 * Version: 1.0
 * Author: developer.wordpress.org
 * Author URI: https://codex.wordpress.org/User:Aternus
 */

function wporg_register_taxonomy_course() {
  $labels = array(
    'name'              => _x( 'Courses', 'taxonomy general name' ),
    'singular_name'     => _x( 'Course', 'taxonomy singular name' ),
    'search_items'      => __( 'Search Courses' ),
    'all_items'         => __( 'All Courses' ),
    'parent_item'       => __( 'Parent Course' ),
    'parent_item_colon' => __( 'Parent Course:' ),
    'edit_item'         => __( 'Edit Course' ),
    'update_item'       => __( 'Update Course' ),
    'add_new_item'      => __( 'Add New Course' ),
    'new_item_name'     => __( 'New Course Name' ),
    'menu_name'         => __( 'Course' ),
  );
  $args   = array(
    'hierarchical'      => true, // make it hierarchical (like categories)
    'labels'            => $labels,
    'show_ui'           => true,
    'show_admin_column' => true,
    'query_var'         => true,
    'rewrite'           => [ 'slug' => 'course' ],
  );
  register_taxonomy( 'course', [ 'post' ], $args );
}
add_action( 'init', 'wporg_register_taxonomy_course' );
```

<!-- 
### Step 3: Review the Result
 -->
### ステップ3: 結果の検証

<!-- 
Activate your plugin, then go to **Posts > Add New**. You should see a new meta box for your "Courses" Taxonomy.
 -->
プラグインを有効にして、**投稿 > 新規投稿を追加**に移動してください。タクソノミー「コース」の新しいメタボックスが表示されるはずです。

<!-- 
![Courses Taxonomy Post Screen](https://make.wordpress.org/docs/files/2014/02/courses_taxonomy_post_screen.png)
 -->
![タクソノミー「コース」の投稿画面](https://make.wordpress.org/docs/files/2014/02/courses_taxonomy_post_screen.png)

<!-- 
### Code Breakdown
 -->
### コード・ブレークダウン

<!-- 
The following discussion breaks down the code used above describing the functions and parameters.
 -->
以下の議論では、上記で使用したコードを分解し、関数とパラメータを説明します。

<!-- 
The function `wporg_register_taxonomy_course` contains all the steps necessary for registering a Custom Taxonomy.
 -->
関数 `wporg_register_taxonomy_course` は、カスタムタクソノミーを登録するために必要なすべてのステップを含んでいます。

<!-- 
The `$labels` array holds the labels for the Custom Taxonomy.
 -->
配列 `$labels` は、カスタムタクソノミーのラベルを保持します。

<!-- 
These labels will be used for displaying various information about the Taxonomy in the Administration area.
 -->
これらのラベルは、管理エリアでタクソノミーに関するさまざまな情報を表示するために使用されます。

<!-- 
The `$args` array holds the configuration options that will be used when creating our Custom Taxonomy.
 -->
配列 `$args` は、カスタムタクソノミーを作成する際に使用する設定オプションを保持します。

<!-- 
The function [`register_taxonomy()`](https://developer.wordpress.org/reference/functions/register_taxonomy/) creates a new Taxonomy with the identifier `course` for the `post` Post Type using the `$args` array for configuration.
 -->
関数 [`register_taxonomy()`](https://developer.wordpress.org/reference/functions/register_taxonomy/) は、設定用の配列 `$args` を使用して、投稿タイプ `post` 用の識別子 `course` を持つ新しいタクソノミーを作成します。

<!-- 
The function [`add_action()`](https://developer.wordpress.org/reference/functions/add_action/) ties the `wporg_register_taxonomy_course` function execution to the `init` action hook.
 -->
関数 [`add_action()`](https://developer.wordpress.org/reference/functions/add_action/) は、関数 `wporg_register_taxonomy_course` の実行をアクションフック `init` に関連付けます。

#### $args

<!-- 
The $args array holds important configuration for the Custom Taxonomy, it instructs WordPress how the Taxonomy should work.
 -->
配列 $args は、カスタムタクソノミーの重要な設定を保持し、タクソノミーの動作を WordPress に指示します。

<!-- 
### Summary
 -->
### まとめ

<!-- 
Take a look at [`register_taxonomy()`](https://developer.wordpress.org/reference/functions/register_taxonomy/) function for a full list of accepted parameters and what each of these do.
 -->
使用可能なパラメータの完全なリストと各パラメータが何をするかについては、関数 [`register_taxonomy()`](https://developer.wordpress.org/reference/functions/register_taxonomy/) を参照してください。

<!-- 
With our Courses Taxonomy example, WordPress will automatically create an archive page and child pages for the `course` Taxonomy.
 -->
タクソノミー「コース」の例では、WordPress は自動的にタクソノミー `course` のアーカイブページと子ページを作成します。

<!-- 
The archive page will be at `/course/` with child pages spawning under it using the Term's slug (`/course/%%term-slug%%/`).
 -->
アーカイブページは `/course/` にあり、その下に子ページがタームのスラッグ (`/course/%%term-slug%%/`) を使って生成されます。

<!-- 
## Using Your Taxonomy
 -->
## あなたのタクソノミーの利用

<!-- 
WordPress has **many** functions for interacting with your Custom Taxonomy and the Terms within it.
 -->
WordPress には、カスタムタクソノミーとその中のタームとのインタラクションのための**多くの**機能があります。

<!-- 
Here are some examples:
 -->
いくつか例を挙げてみましょう:

<!-- 
- `the_terms`: Takes a Taxonomy argument and renders the terms in a list.
- `wp_tag_cloud`: Takes a Taxonomy argument and renders a tag cloud of the terms.
- `is_taxonomy`: Allows you to determine if a given taxonomy exists.
 -->
- `the_terms`: タクソノミーの引数をとり、タームをリストで表示します。
- `wp_tag_cloud`: タクソノミーの引数をとり、タームのタグクラウドを表示します。
- `is_taxonomy`: 指定したタクソノミーが存在するかどうかを判別できます。
