<!--
# Shortcodes
-->

# ショートコード

<!--
As a security precaution, running PHP inside WordPress content is forbidden; to allow dynamic interactions with the content, Shortcodes were presented in WordPress version 2.5.
-->

セキュリティの予防措置として、WordPress コンテンツ内で PHP を実行することは禁止されています。コンテンツとの動的なインタラクションを可能にするために、WordPress バージョン2.5でショートコードが導入されました。

<!--
Shortcodes are macros that can be used to perform dynamic interactions with the content. i.e creating a gallery from images attached to the post or rendering a video.
-->

ショートコードは、コンテンツとの動的なインタラクション、たとえば、投稿に添付された画像からギャラリーを作成したり、ビデオをレンダリングする、等を実行するために使用できるマクロです。

<!--
## Why Shortcodes?
-->

## なぜショートコードなのですか ?

<!--
Shortcodes are a valuable way of keeping content clean and semantic while allowing end users some ability to programmatically alter the presentation of their content.
-->

ショートコードは、コンテンツをクリーンでセマンティックに保ちながら、コンテンツの表示をエンドユーザーがプログラムで変更できるようにする、便利な方法です。

<!--
When the end user adds a photo gallery to their post using a shortcode, they’re using the least data possible to indicate how the gallery should be presented.
-->

エンドユーザーがショートコードを使用してフォトギャラリーを投稿に追加する場合、可能な限り最小限のデータを使用して、ギャラリーの表示方法を指示できます。

<!--
Advantages:
-->

利点:

<!--
- No markup is added to the post content, which means that markup and styling can easily be manipulated on the fly or at a later state.
- Shortcodes can also accept parameters, allowing users to modify how the shortcode behaves on an instance by instance basis.
-->

- 投稿コンテンツにマークアップが追加されないので、マークアップやスタイリングを、その場で、または後で、簡単に操作できます。
- ショートコードは、パラメータを受け取ることもでき、インスタンスごとにショートコードの動作をユーザーが変更できます。

<!--
## Built-in Shortcodes
-->

## 組込みのショートコード

<!--
By default, WordPress includes the following shortcodes:
-->

デフォルトでは、WordPress には以下のショートコードが用意されています:

<!--
- `[caption]` – allows you to wrap captions around content
- `[gallery]` – allows you to show image galleries
- `[audio]` – allows you to embed and play audio files
- `[video]` – allows you to embed and play video files
- `[playlist]` – allows you to display collection of audio or video files
- `[embed]` – allows you to wrap embedded items
-->

- `[[caption]]` – コンテンツのキャプションをラップ (回り込み) できます。
- `[[gallery]]` – 画像ギャラリーを表示できます。
- `[[audio]]` – 音声ファイルを埋め込んで再生できます。
- `[[video]]` – 動画ファイルを埋め込んで再生できます。
- `[[playlist]]` – オーディオファイルやビデオファイルのコレクションを表示できます。
- `[[embed]]` – 埋め込み項目をラップ (回り込み) できます。

<!--
## Shortcode Best Practices
-->

## ショートコードのベストプラクティス

<!--
Best practices for developing shortcodes include the [plugin development best practices](https://developer.wordpress.org/plugins/plugin-basics/best-practices/) and the list below:
-->

ショートコード開発に関するベストプラクティスには、[プラグイン開発のベストプラクティス](https://ja.wordpress.org/team/handbook/plugin-development/plugin-basics/best-practices/)と以下のリストがあります:

<!--
- **Always return!** Shortcodes are essentially filters, so creating "[side effects](https://en.wikipedia.org/wiki/Side_effect_(computer_science))" will lead to unexpected bugs.
- Prefix your shortcode names to avoid collisions with other plugins.
- Sanitize the input and escape the output.
- Provide users with clear documentation on all shortcode attributes.
-->

- **常に return を実行しましょう !** ショートコードは基本的にフィルターですので、「[副作用](https://en.wikipedia.org/wiki/Side_effect_(computer_science))」を作ると予期せぬバグにつながります。
- 他のプラグインとの衝突を避けるために、ショートコード名に接頭辞をつけましょう。
- 入力をサニタイズし、出力をエスケープしましょう。
- すべてのショートコード属性に関して明確なドキュメントをユーザーに提供しましょう。

<!--
## Quick Reference
-->

## クイック・リファレンス

<!--
See the complete example of using a [basic shortcode structure, taking care of self-closing and enclosing scenarios, shortcodes within shortcodes and securing output](https://developer.wordpress.org/plugins/shortcodes/shortcodes-with-parameters/#complete-example).
-->

[基本的なショートコードの構造、自己完結型と囲み型シナリオの取り扱い、入れ子状態のショートコード、出力の安全確保](https://ja.wordpress.org/team/handbook/plugin-development/shortcodes/shortcodes-with-parameters/#complete-example)を使用する完全な例を参照してください。

<!--
## External Resources
-->

## 外部リソース

<!--
- [WordPress Shortcodes Generator](https://generatewp.com/shortcodes/)
-->

- [WordPress ショートコード・ジェネレーター](https://generatewp.com/shortcodes/)
