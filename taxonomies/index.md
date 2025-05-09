<!--
## Taxonomies
-->

# タクソノミー

<!--
A **Taxonomy** is a fancy word for the classification/grouping of things. Taxonomies can be hierarchical (with parents/children) or flat.
-->

**タクソノミー**とは、物事を分類/グループ化するための専門用語です。タクソノミーは、階層的 (親/子) にもフラットにもなります。

<!--
WordPress stores the Taxonomies in the `term_taxonomy` database table allowing developers to register Custom Taxonomies along the ones that already exist.
-->

WordPress は `term_taxonomy` データベース・テーブルにタクソノミーを格納し、開発者はすでに存在するタクソノミーの他に、カスタム・タクソノミーを登録できます。

<!--
Taxonomies have **Terms** which serve as the topic by which you classify/group things. They are stored inside the `terms` table.
-->

タクソノミーには「ターム」があり、トピックとして分類/グループ化されます。これらは `terms` テーブルに格納されます。

<!--
For example: a Taxonomy named "Art" can have multiple Terms, such as "Modern" and "18th Century".
-->

たとえば: タクソノミー「Art」は、「Modern」や「18th Century」といった複数のタームを持つことができます。

<!--
This chapter will show you how to register Custom Taxonomies, how to retrieve their content from the database, and how to render them to the public.
-->

本章では、カスタムタクソノミーの登録方法、データベースからの取得方法、公開方法について説明します。

<!--
[info]WordPress 3.4 and earlier had a Taxonomy named "Links" which was deprecated in WordPress 3.5.[/info]
-->

[info]WordPress 3.4以前には「Links」というタクソノミーがありましたが、WordPress 3.5では廃止されました。[/info]
