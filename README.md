<!--
# developer-plugins-handbook
Welcome to the WordPress Plugin Developer Handbook; are you ready to jump right in to the world of WordPress plugins?
-->

# プラグイン開発ハンドブック翻訳作業用リポジトリ

これは[プラグイン開発ハンドブック 日本語版](https://ja.wordpress.org/team/handbook/plugin-development/)の翻訳ファイル用リポジトリです。

## 日本語訳への質問やコメント

[Issues](https://github.com/jawordpressorg/developer-plugins-handbook/issues) から新しい issue を作成してください。[こちら](https://github.com/jawordpressorg/developer-plugins-handbook/issues/new) のリンクをクリックしても作成できます。

画面は英語ですが、日本語を入力できます。

## (管理者向け) リポジトリの管理方法

Takayuki Miyauchi さんの発案された翻訳方式を採用して、プラグイン開発ハンドブックのドキュメントを翻訳しています。
https://qiita.com/miya0001/items/4745cf900a66c0bbf8e5

```
% git clone git@github.com:WordPress/developer-plugins-handbook.git
% cd developer-plugins-handbook
% git remote add upstream https://github.com/WordPress/developer-plugins-handbook.git
```

### 原文の更新・反映方法

1. 原文の更新を取得します。
   ```
   % git fetch upstream
   ```
2. `main` ブランチから、原文更新用のブランチをチェックアウトします (例: `update-document` ブランチ)。
   ```
   % git checkout -b update-document
   ```
3. 原文の更新を現在のブランチにマージします。
   ```
   % git merge upstream/main
   ```
4. 以下のように、自動マージが失敗する場合があります。
   ```
   % Auto-merging path/to/auto-merged-file.md
   % CONFLICT (content): Merge conflict in path/to/conflict-file.md
   % Automatic merge failed; fix conflicts and then commit the result.
   ```
   コンフリクトが発生した場合は、その箇所を確認し、手動でコンフリクトを解消します。
5. 全てのコンフリクトを解消したら、commit します。
   ```
   % git add .
   % git commit -m "原文を更新"
   ```
6. 原文に新しいテキストが追加されている場合は、それらを日本語翻訳し、commit します。
   新しいページの追加等、追加されたテキストの量が大きい場合は、ここで全てを翻訳する必要はありません。原文の更新を `main` ブランチからにマージした後に、順次日本語訳を進めてもかまいません。
7. 最新の原文、および日本語化済の情報を含んだブランチ (例: `update-document`) から、プルリクエストを作成します。
8. 差分を確認し、問題なければ `main` ブランチにマージします。
