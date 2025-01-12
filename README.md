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

最初の1回だけ
```
% git clone git@github.com:WordPress/developer-plugins-handbook.git
% cd developer-plugins-handbook
% git remote add upstream https://github.com/WordPress/developer-plugins-handbook.git
```
あとは定期的に
```
% git fetch upstream
% git merge upstream/main
```

ここですべてのファイルがマージされる場合でも、どこが変更されたかチェックし、手動で反映する必要があります (例: コードが変更された場合)。画面の出力から「.md」ファイルを抽出して変更一覧を取得します。

すべてのファイルがマージされなかった場合は、以下のコマンドで変更されたファイルの一覧を取得します。
```
% git status | grep \.md | grep -v CHANGELOG
```

変更ファイルの一覧を取得したら、GitHub で最近の変更を確認しながら、日本語版に反映します。
```
% git add -A
% git commit -m "Synched with the latest"
% git push
```
