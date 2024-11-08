<!-- 
# Common issues
 -->
# 一般的な課題

<!-- 
This is a compilation of some of the most common issues the Plugin Review Team encounters when reviewing plugins.
 -->
これはプラグイン・レビューチームがプラグインをレビューする際に遭遇する、最も一般的な課題の集録です。

<!-- 
This list contains excerpts from the team's email messages, and should not be considered a complete or exhaustive list; the outcome of the reviews depends on the manual review performed by the team.
 -->
このリストは、チームの E メールメッセージからの抜粋であり、完全または網羅的なリストとみなしてはいけません; レビューの結果は、チームによる手動レビューに依存します。

<!-- 
## Security
 -->
## セキュリティ

<!-- 
### Sanitize
 -->
### サニタイズ

<!-- 
**Input data must be Sanitized, Validated, and Escaped on output**
 -->
**入力データは、サニタイズ、バリデーション、および出力時にエスケープしなければなりません**

<!-- 
When you include POST/GET/REQUEST/FILE calls in your plugin, it's important to sanitize, validate, and escape them. The goal here is to prevent a user from accidentally sending trash data through the system, as well as protecting them from potential security issues. 
 -->
POST/GET/REQUEST/FILE 呼び出しをプラグインに搭載する場合、それらをサニタイズ、検証、エスケープすることが重要です。ここでの目的は、ユーザーが誤ってシステムを通してゴミのようなデータを送信するのを防ぐことと、潜在的なセキュリティの課題からユーザーを守ることです。

<!-- 
SANITIZE: Data that is input (either by a user or automatically) must be sanitized as soon as possible. This lessens the possibility of XSS vulnerabilities and MITM attacks where posted data is subverted. 
 -->
SANITIZE: (ユーザーによって、あるいは自動的に) 入力されたデータは、できるだけ早くサニタイズされなければなりません。これにより、XSS 脆弱性や、投稿されたデータが改竄される MITM 攻撃の可能性を減らすことができます。

<!-- 
VALIDATE: All data should be validated, no matter what. Even when you sanitize, remember that you don’t want someone putting in ‘dog’ when the only valid values are numbers. 
 -->
VALIDATE: すべてのデータは、何があっても、検証される必要があります。サニタイズする場合でも、有効な値が数字だけなのに、誰かが「dog」と入力しないようにすることを忘れないでください。

<!-- 
ESCAPE: Data that is output must be escaped properly when it is echo'd, so it can't hijack admin screens. There are many esc_*() functions you can use to make sure you don't show people the wrong data.
 -->
ESCAPE: 出力するデータは echo する際に適切にエスケープして管理画面の乗っ取りを防がなければなりません。間違ったデータを表示しないために利用できる、多くの `esc_*()` 関数があります。

<!-- 
To help you with this, WordPress comes with a number of sanitization and escaping functions. You can read about those here:
 -->
そのために、WordPress には多くのサニタイズ機能とエスケープ機能が用意されています。これらについては、こちらをご覧ください:

<!-- 
https://developer.wordpress.org/apis/security/sanitizing/
https://developer.wordpress.org/apis/security/escaping/
 -->
https://developer.wordpress.org/apis/security/sanitizing/
https://developer.wordpress.org/apis/security/escaping/

<!-- 
Remember: You must use the most appropriate functions for the context. If you’re sanitizing email, use sanitize_email(), if you’re outputting HTML, use wp_kses_post(), and so on.
 -->
覚えておいてください: コンテキストに最も適した関数を使う必要があります。電子メールをサニタイズするなら `sanitize_email()` を、HTML を出力するなら `wp_kses_post()` を、といった感じです。

<!-- 
An easy mantra here is this:
 -->
簡単な真言は、以下の通りです:

<!-- 
Sanitize early  
Escape Late  
Always Validate
 -->
早めにサニタイズ
遅れてエスケープ  
常にバリデート

<!-- 
Clean everything, check everything, escape everything, and never trust the users to always have input sane data. After all, users come from all walks of life.
 -->
すべてをクリーニングし、すべてをチェックし、すべてをエスケープし、そして、ユーザーが常に適切なデータを入力していると信じてはいけません。結局のところ、ユーザーにはいろいろな人がいるものですから。

<!-- 
#### Sanitize: Confusion about escape and sanitize functions
 -->
#### サニタイズ: エスケープ関数とサニタイズ関数に関する混乱

<!-- 
**Note**: escape functions cannot be used to sanitize. They serve different purposes. Even if they seem to be perfect for this purpose, most of the functions are filterable and people expect to use them to escape. Therefore, another plugin may change what they do and make yours at risk and exploitable.
 -->
**メモ**: エスケープ関数は、サニタイズには利用できません。これらには異なる目的があります。たとえエスケープ関数がサニタイズの目的に完璧であるように見えても、ほとんどのエスケープ関数はフィルターで変更可能であり、エスケープのための使用が期待されています。別のプラグインが自身のために悪意なくエスケープ関数を変更することで、あなたのプラグインが危険にさらされ、悪用される可能性があります。


<!-- 
If you are trying to echo the variable, you have to first sanitize it and then escape it, as for example:
 -->
変数を echo しようとする場合は、まず変数をサニタイズしてからエスケープしなければなりません。たとえば:

```php
echo esc_html(sanitize_text_field($_POST['example']));
```

<!-- 
#### Sanitize: Using filter functions to sanitize
 -->
#### サニタイズ: フィルター関数を使ったサニタイズ

<!-- 
**Note**: When using functions like `filter_var`, `filter_var_array`, `filter_input` and/or `filter_input_array` you will need to [set the FILTER parameter to any kind of filter that sanitizes the input](https://www.php.net/manual/en/filter.filters.php).
 -->
**メモ**: `filter_var`、`filter_var_array`、`filter_input` および/または `filter_input_array` のような関数を使用する場合は、[入力をサニタイズする任意の種類のフィルタに、パラメータ FILTER を設定](https://www.php.net/manual/en/filter.filters.php)する必要があります。

<!-- 
Leaving the filter parameter empty, PHP by default will apply the filter "FILTER_DEFAULT" **which is not sanitizing at all**.
 -->
パラメータ filter を空にすると、PHP はデフォルトでフィルター「FILTER_DEFAULT」を適用し、**これはまったくサニタイズされていません**。

```php
$post_id = filter_input(INPUT_GET, 'post_id', FILTER_SANITIZE_NUMBER_INT);
```

<!-- 
#### Sanitize: Nonces
 -->
#### サニタイズ: nonce

<!-- 
**Note**: When checking a nonce using `wp_verify_nonce` you will need to sanitize the input using `wp_unslash` AND `sanitize_text_field`, [this is because this function is pluggable, and extenders should not trust its input values](https://developer.wordpress.org/news/2023/08/understand-and-use-wordpress-nonces-properly/#verifying-the-nonce).
 -->
**メモ**: `wp_verify_nonce` を使用して nonce をチェックする際には、`wp_unslash` と `sanitize_text_field` を使用して入力をサニタイズする必要があります。[なぜなら、この関数は差し替え可能であり、エクステンダーはその入力値を信用すべきではないから](https://developer.wordpress.org/news/2023/08/understand-and-use-wordpress-nonces-properly/#verifying-the-nonce)です。

<!-- 
Example:
 -->
例:

```php
if ( ! isset( $_POST['prefix_nonce'] ) || ! wp_verify_nonce( sanitize_text_field( wp_unslash ( $_POST['prefix_nonce'] ) ) , 'prefix_nonce' ) )
```

<!-- 
### Processing the whole input
 -->
### 入力全体の処理

<!-- 
We strongly recommend you **never** attempt to process the whole $_POST/$_REQUEST/$_GET stack. This makes your plugin slower as you're needlessly cycling through data you don't need. Instead, you should only be attempting to process the items within that are required for your plugin to function.
 -->
`$_POST`/`$_REQUEST`/`$_GET` スタック全体を処理することを **決して** 試みないことを、私たちは強く推奨します。これは、必要のないデータを無駄に循環させることになり、プラグインを遅くします。その代わりに、プラグインが機能するために必要な項目だけを処理するようにしましょう。

<!-- 
### Escape
 -->
### エスケープ

<!-- 
**Variables and options must be escaped when echo'd**
 -->
**変数とオプションは、echo する際にエスケープしなければなりません**

<!-- 
Much related to sanitizing everything, all variables that are echoed need to be escaped when they're echoed, so it can't hijack users or (worse) admin screens. There are many esc_*() functions you can use to make sure you don't show people the wrong data, as well as some that will allow you to echo HTML safely.
 -->
すべてのサニタイズに関連しますが、ユーザーや (さらに最悪) 管理画面をハイジャックされないよう、echo する変数はすべて、echo する際にエスケープしてください。間違ったデータを人に見せないようにするために使える `esc_*()` 関数はたくさんありますし、HTML を安全に echo できるものもあります。

<!-- 
At this time, we ask you escape **all $-variables, options, and any sort of generated data when it is being echoed**. That means you should not be escaping when you build a variable, but when you output it at the end. We call this 'escaping late.'
 -->
このとき、**echo する際、すべての$変数、オプション、生成されたあらゆる種類のデータ** をエスケープしてください。つまり、変数を構築するときにエスケープするのではなく、最後に出力するときにエスケープしてください。これを「遅れてエスケープ」と表現します。

<!-- 
Besides protecting yourself from a possible XSS vulnerability, escaping late makes sure that you're keeping the future you safe. While today your code may be only outputted hardcoded content, that may not be true in the future. By taking the time to properly escape **when** you echo, you prevent a mistake in the future from becoming a critical security issue.
 -->
XSS 脆弱性の可能性から身を守るだけでなく、遅れてエスケープすることで、将来のあなたの安全を確保できます。現在、あなたのコードはハードコードした内容しか出力しないかもしれませんが、将来はそうでなくなるかもしれません。echo する **際に** 適切なタイミングでエスケープすることで、重大なセキュリティ課題になる将来のミスを防ぐことができます。

<!-- 
This remains true of options you've saved to the database. Even if you've properly sanitized when you saved, the tools for sanitizing and escaping aren't interchangeable. Sanitizing makes sure it's safe for processing and storing in the database. Escaping makes it safe to output.
 -->
これは、データベースに保存したオプションについても同様です。保存時に適切にサニタイズした場合でも、サニタイズとエスケープのツールは互換性がありません。サニタイズは、処理とデータベースへの格納が安全であることを確認します。エスケープは、出力する際の安全性を確保します。

<!-- 
Also keep in mind that sometimes a function is echoing when it should really be returning content instead. This is a common mistake when it comes to returning JSON encoded content. Very rarely is that actually something you should be echoing at all. Echoing is because it needs to be on the screen, read by a human. Returning (which is what you would do with an API) can be json encoded, though remember to **sanitize** when you save to that json object!
 -->
また、本当はコンテンツを返すべきなのに、関数が echo していることもあることを覚えておいてほしい。これは、JSON エンコードされたコンテンツを返す際によくある間違いです。実際に echo すべき内容であることはほとんどありません。echo するのは、それが画面上に表示され、人間が読む必要があるからです。(API で行うような) 返却は、json エンコードできますが、json オブジェクトに保存する際には、**サニタイズ** することを忘れずに !

<!-- 
There are a number of options to secure all types of content (html, email, etc). Yes, even HTML needs to be properly escaped.
 -->
あらゆるタイプのコンテンツ (html、e-mail など) をセキュアにするためのオプションはいくつもあります。そう、HTML でさえも適切にエスケープする必要があるのです。

<!-- 
[https://developer.wordpress.org/apis/security/escaping/](https://developer.wordpress.org/apis/security/escaping/)
 -->
[https://developer.wordpress.org/apis/security/escaping/](https://developer.wordpress.org/apis/security/escaping/)

<!-- 
Remember: You must use the most appropriate functions for the context. There is pretty much an option for everything you could echo. Even echoing HTML safely.
 -->
覚えておいてください: その文脈に最も適した関数を使う必要があります。echo できるものすべてに最適なオプションがあります。HTML を安全に echo することさえも。

<!-- 
#### Escape: Use of esc_url_raw
 -->
#### エスケープ: esc_url_raw の使用

<!-- 
We know this is confusing, the `esc_url_raw` function is not an escaping function, but a sanitizing function similar to `sanitize_url`. Specifically it is used to sanitize a URL for use in a database or a redirection.
 -->
まぎらわしいとは思いますが、`esc_url_raw` 関数はエスケープ関数ではなく、`sanitize_url` と同様のサニタイズ関数です。具体的には、データベースやリダイレクトで使用する URL をサニタイズするために使用されます。

<!-- 
The appropriate function to escape a URL is `esc_url`.
 -->
URL をエスケープする適切な関数は、`esc_url` です。

<!-- 
#### Escape: Use of __
 -->
#### エスケープ: __ の使用

<!-- 
The function `__` retrieves the translation without escaping, please either:
 -->
関数 `__` は、エスケープせずに翻訳を取得します。以下のどちらかを使用してください:

<!-- 
- Use an alternative function that escapes the resulting value such as `esc_html__` or `esc_attr__`.
- Or wrap the `__` function with a proper escaping function such as `esc_html`, `esc_attr`, `wp_kses_post`, etc.
 -->
- `esc_html__` や `esc_attr__` のように、結果の値をエスケープする代替関数を使用する。
- または、`__` 関数を `esc_html`、`esc_attr`、`wp_kses_post` などの、適切なエスケープ関数でラップする。

<!-- 
Examples:
 -->
例:

```php
<h2><?php echo esc_html__('Settings page', 'plugin-slug'); ?></h2>
<h2><?php echo esc_html(__('Settings page', 'plugin-slug')); ?></h2>
```

<!-- 
#### Escape: Use of _e and _ex
 -->
#### エスケープ: _e および _ex の使用

<!-- 
The functions `_e` and `_ex` output the translation without escaping, please use an alternative function that escapes the output.
 -->
関数 `_e` と `_ex` は、エスケープせずに翻訳を出力します。出力をエスケープする代替関数を使用してください。

<!-- 
- An alternative to `_e` would be `esc_html_e`, `esc_attr_e` or simply using `__` wrapped by an escaping function and inside an `echo`.
- An alternative to `_ex` would be using `_x` wrapped by an escaping function and inside an `echo`.
 -->
- `_e` の代替としては、`esc_html_e`、`esc_attr_e`、あるいは単に、エスケープ関数でラップして `echo` の中に記述する `__` を使うこともできる。
- `_ex` の代替としては、エスケープ関数でラップして、`echo` の中に記述する `_x` を使うこともできる。

<!-- 
Examples:
 -->
例:

```php
<h2><?php esc_html_e('Settings page', 'plugin-slug'); ?></h2>
<h2><?php echo esc_html(__('Settings page', 'plugin-slug')); ?></h2>
<h2><?php echo esc_html(_x('Settings page', 'Settings page title', 'plugin-slug')); ?></h2>
```

<!-- 
#### Escape: Use json_encode
 -->
#### エスケープ: json_encode の使用

<!-- 
When you need to echo a JSON, it's better to make use of the function `wp_json_encode`, also, make sure you are not avoiding escaping with the options passed on the second parameter.
 -->
JSON を echo する必要がある場合は、関数 `wp_json_encode` を使用するほうが良いでしょう。また、第2パラメータに渡されるオプションでエスケープを回避していないか確認してください。

```php
echo wp_json_encode($array_or_object);
```

<!-- 
#### Escape: HTML
 -->
#### エスケープ: HTML

<!-- 
When escaping, there are cases where your plugin will need to output HTML. This can be done using the functions `wp_kses_post` or `wp_kses`. The function `wp_kses_post` will allow any common HTML that can go inside a post content, `wp_kses` will allow any HTML that you set up using its second and third parameters, please [refer to its documentation](https://developer.wordpress.org/reference/functions/wp_kses/).
 -->
エスケープする際、プラグインが HTML を出力する必要がある場合があります。これには、`wp_kses_post` または `wp_kses` 関数を使います。`wp_kses_post` 関数は、投稿コンテンツの中に入れる一般的な HTML を許可します。`wp_kses` は、2番目と3番目のパラメータを使って設定した HTML を許可します。[ドキュメントを参照](https://developer.wordpress.org/reference/functions/wp_kses/)してください。

<!-- 
A common mistake is to use `esc_html` to escape HTML. This function is not intended for that, it's intended to escape the output that will go **inside** an HTML tag, therefore it will strip any HTML tags.
 -->
よくある間違いは、`esc_html` を使って HTML をエスケープすることです。この関数はそのためのものではありません。この関数は、HTML タグ **内部** に入る出力をエスケープするためのものであり、したがって HTML タグは、すべて取り除かれることになります。

<!-- 
Examples:
 -->
例:

```php
echo wp_kses_post($html_content);
echo wp_kses($html_content, array( 'a', 'div', 'span' ));
```

<!-- 
#### Escape: Using sanitizing functions
 -->
#### エスケープ: サニタイジング関数の使用

<!-- 
Sanitize functions cannot be used to escape. They serve different purposes. Even if they seem to be perfect for this purpose, most of the functions are filterable and people expect to use them to sanitize. Therefore, another plugin may change what they do and make yours at risk and exploitable.
 -->
サニタイズ関数は、エスケープには利用できません。これらには異なる目的があります。たとえサニタイズ関数がエスケープの目的に完璧であるように見えても、ほとんどのサニタイズ関数はフィルターで変更可能であり、サニタイズのための使用が期待されています。別のプラグインが自身のために悪意なくサニタイズ関数を変更することで、あなたのプラグインが危険にさらされ、悪用される可能性があります。

<!-- 
If you are trying to echo the variable, you have to first sanitize it and then escape it, as for example:
 -->
変数を echo しようとする場合は、まず変数をサニタイズしてからエスケープしなければなりません。たとえば:

```php
echo esc_html(sanitize_text_field($_POST['example']));
```

<!-- 
### Files
 -->
### ファイル

<!-- 
#### Files: Use the WordPress file uploader
 -->
#### ファイル: WordPress ファイル・アップローダーの使用

<!-- 
**Please use WordPress' file uploader**
 -->
**WordPress ファイル・アップローダーをご利用ください**

<!-- 
When plugins use `move_uploaded_file(), they exclude their uploads from the built-in checks and balances with WordPress's functions. Instead of that, you should use the built in function:
 -->
プラグインで `move_uploaded_file()` を使用すると、アップロードは組み込みのチェック機能や、WordPress 関数とのバランスが取られません。代わりに、内蔵関数を使用してください:

<!-- 
[https://developer.wordpress.org/reference/functions/wp_handle_upload/](https://developer.wordpress.org/reference/functions/wp_handle_upload/)
 -->
[https://developer.wordpress.org/reference/functions/wp_handle_upload/](https://developer.wordpress.org/reference/functions/wp_handle_upload/)

<!-- 
#### Files: Unfiltered uploads
 -->
#### ファイル: フィルタリングされていないアップロード

<!-- 
**ALLOW_UNFILTERED_UPLOADS is not allowed.**
 -->
**ALLOW_UNFILTERED_UPLOADS は、許可されていません。**

<!-- 
Setting this constant to true will allow the user to upload any type of file (including PHP and other executables), creating serious potential security risks. As developers, we should not use or allow the use of this constant in any kind of logic, not even in a conditional.
 -->
この定数を true に設定すると、ユーザーは (PHP やその他の実行可能ファイルを含む) あらゆるタイプのファイルをアップロードできるようになり、深刻な潜在的なセキュリティリスクが発生します。開発者としては、この定数をいかなるロジックでも、条件付きでも使用したり 許可したりすべきではありません。

<!-- 
WordPress includes a list of safe files, as you can see in the function [wp_get_mime_types](https://developer.wordpress.org/reference/functions/wp_get_mime_types).
 -->
WordPress には、関数 [wp_get_mime_types](https://developer.wordpress.org/reference/functions/wp_get_mime_types) で見ることができるように、安全なファイルのリストが含まれています。

<!-- 
If you need to add a specific file that is not in the list and that won't represent a security risk, you can do so using the [upload_mimes](https://developer.wordpress.org/reference/hooks/upload_mimes/) filter.
 -->
リストにない特定のファイルを追加する必要があり、セキュリティ上のリスクがない場合は、フィルター [upload_mimes](https://developer.wordpress.org/reference/hooks/upload_mimes/) を使用して追加できます。

<!-- 
#### Files: Calling files remotely
 -->
#### ファイル: リモートでファイルを呼び出す

<!-- 
Offloading images, js, css, and other scripts to your servers or any remote service (like Google, MaxCDN, jQuery.com etc) is disallowed. When you call remote data you introduce an unnecessary dependency on another site. If the file you're calling isn't a part of WordPress Core, then you should include it -locally- in your plugin, not remotely. If the file IS included in WordPress core, please call that instead.
 -->
画像、js、css、その他のスクリプトをあなたのサーバーやリモートサービス (Google、MaxCDN、jQuery.com など) にオフロードすることは禁止されています。リモートのデータを呼び出すと、他のサイトへの不必要な依存が生じます。呼び出しているファイルが WordPress Core の一部でない場合は、リモートではなく -ローカルで- プラグインに含める必要があります。そのファイルが WordPress Core に含まれているなら、代わりにそれを呼び出してください。

<!-- 
An exception to this rule is if your plugin is performing a service. We will permit this on a case by case basis. Since this can be confusing we have some examples of what are not permitted:
 -->
このルールの例外は、プラグインがサービスを提供している場合です。この場合、ケースバイケースで許可します。混乱しやすいので、許可されない例をいくつか挙げておきます:

<!-- 
- Offloading jquery CSS files to Google - You should include the CSS in your plugin.
- Inserting an iframe with a help doc - A link, or including the docs in your plugin is preferred.
- Calling images from your own domain - They should be included in your plugin.
 -->
- jquery の CSS ファイルを Google にオフロード - プラグインに CSS を含める必要があります。
- iframe にヘルプドキュメントを挿入 - リンクを貼るか、プラグインにドキュメントを含めるのが望ましいでしょう。
- 独自ドメインから画像の呼び出し - プラグインに含める必要があります。

<!-- 
Here are some examples of what we would permit:
 -->
以下に、許可する例をいくつか挙げておきます:

<!-- 
- Calling font families from Google or their approved CDN (if GPL compatible)
- API calls back to your server to process possible spam comments (like Akismet)
- Offloading comments to your own servers (like Disqus)
- oEmbed calls to a service provider (like Twitter or YouTube)
 -->
- (GPL 互換の場合) Google またはその承認された CDN からフォントファミリーの呼び出し
- (Akismet のように) スパムコメントを処理するため、あなたのサーバーに API がコールバック
- (Disqus のように) 独自サーバーにコメントをオフロード
- (Twitter や YouTube のように) サービスプロバイダへの oEmbed 呼び出し

<!-- 
Please remove external dependencies from your plugin and, if possible, include all files within the plugin (that is not called remotely). If instead you feel you are providing a service, please re-write your readme.txt in a manner that explains the service, the servers being called, and if any account is needed to connect.
 -->
プラグインから外部の依存関係を削除し、可能であれば、プラグイン内に (リモートから呼び出されない) すべてのファイルを搭載してください。代わりにサービスを提供していると思われる場合は、readme.txt を書き直し、サービス、呼び出されるサーバー、接続に必要なアカウントについて説明してください。

<!-- 
### Libraries
 -->
### ライブラリ

<!-- 
#### Libraries: Using development versions
 -->
#### ライブラリ: 開発版の使用

<!-- 
**Using Beta / Alpha / Development versions of libraries**
 -->
**ライブラリのベータ版/アルファ版/開発版の使用**

<!-- 
We do not recommend you use the beta version of a library unless it has features required by your plugin. Instead, you should be using the most stable release of the library.
 -->
あなたのプラグインに必要な機能がない限り、ライブラリのベータ版を使用することはおすすめしません。代わりに、そのライブラリの最も安定したリリースを使うべきです。

<!-- 
If there is a technical reason you must use the beta version, please explain why. Otherwise, please change your library to the stable release.
 -->
技術的な理由でベータ版を使用しなければならない場合は、その理由を説明してください。そうでなければ、あなたのライブラリを安定版リリースに変更してください。

<!-- 
#### Libraries: Not maintained
 -->
#### ライブラリ: メンテナンスされていない

<!-- 
**Libraries that are no longer maintained are not permitted**
 -->
**メンテナンスが行われなくなったライブラリは、許可されません**

<!-- 
We no longer accept using any library that is no longer supported or maintained by their developers, as they pose a significant security risk. Please consider other options.
 -->
開発者によるサポートやメンテナンスが終了したライブラリの使用は、重大なセキュリティリスクをもたらすため、我々は受け付けておりません。他の選択肢をご検討ください。

<!-- 
#### Libraries: Out of Date
 -->
#### ライブラリ: 期限切れ

<!-- 
At least one of the 3rd party libraries you're using is out of date. Please upgrade to the latest stable version for better support and security. We do not recommend you use beta releases.
 -->
サードパーティ・ライブラリが期限切れの場合は、より良いサポートとセキュリティのために、最新の安定版にアップグレードしてください。ベータリリースの使用は、おすすめしません。

<!-- 
### WPDB: Unsafe SQL calls
 -->
### WPDB: 安全でない SQL 呼び出し

<!-- 
When making database calls, it's highly important to protect your code from SQL injection vulnerabilities. You need to update your code to use wpdb calls and prepare() with your queries to protect them.
 -->
データベースを呼び出す際には、SQL インジェクションの脆弱性からコードを保護することが非常に重要です。`wpdb` 呼び出しを使用するようにコードを更新し、クエリーで `prepare()` を使用して保護する必要があります。

<!-- 
Please review the following:
 -->
以下をご確認ください:

<!-- 
*   [https://developer.wordpress.org/reference/classes/wpdb/#protect-queries-against-sql-injection-attacks](https://developer.wordpress.org/reference/classes/wpdb/#protect-queries-against-sql-injection-attacks)
*   [https://codex.wordpress.org/Data\_Validation#Database](https://codex.wordpress.org/Data_Validation#Database)
*   [https://make.wordpress.org/core/2012/12/12/php-warning-missing-argument-2-for-wpdb-prepare/](https://make.wordpress.org/core/2012/12/12/php-warning-missing-argument-2-for-wpdb-prepare/)
*   [https://ottopress.com/2013/better-know-a-vulnerability-sql-injection/](https://ottopress.com/2013/better-know-a-vulnerability-sql-injection/)
 -->
*   [https://developer.wordpress.org/reference/classes/wpdb/#protect-queries-against-sql-injection-attacks](https://developer.wordpress.org/reference/classes/wpdb/#protect-queries-against-sql-injection-attacks)
*   [https://codex.wordpress.org/Data\_Validation#Database](https://codex.wordpress.org/Data_Validation#Database)
*   [https://make.wordpress.org/core/2012/12/12/php-warning-missing-argument-2-for-wpdb-prepare/](https://make.wordpress.org/core/2012/12/12/php-warning-missing-argument-2-for-wpdb-prepare/)
*   [https://ottopress.com/2013/better-know-a-vulnerability-sql-injection/](https://ottopress.com/2013/better-know-a-vulnerability-sql-injection/)

<!-- 
#### WPDB: Arrays of placeholders
 -->
#### WPDB: プレースホルダーの配列

<!-- 
**Note**: Passing individual values to wpdb::prepare using placeholders is fairly straightforward, but what if we need to pass an array of values instead?
 -->
**メモ**: プレースホルダを使用して `wpdb::prepare` に個々の値を渡すのは非常に簡単だが、代わりに値の配列を渡す必要がある場合はどうするのでしょうか ?

<!-- 
You'll need to create a placeholder for each item of the array and pass all the corresponding values to those placeholders, this seems tricky, but here is a snippet to do so.
 -->
配列の各項目にプレースホルダーを作成し、対応するすべての値をそのプレースホルダーに渡す必要があります。これはトリッキーに見えますが、ここにそのためのスニペットがあります。

```php
$wordcamp_id_placeholders = implode( ', ', array_fill( 0, count( $wordcamp_ids ), '%d' ) );
$prepare_values = array_merge( array( $new_status ), $wordcamp_ids );
$wpdb->query( $wpdb->prepare( "
    UPDATE `$table_name`
    SET `post_status` = %s
    WHERE ID IN ( $wordcamp_id_placeholders )",
    $prepare_values
) );
```

<!-- 
There is a core ticket that could make this easier in the future: [https://core.trac.wordpress.org/ticket/54042](https://core.trac.wordpress.org/ticket/54042)
 -->
将来的にこれを容易にする core チケットがあります: [https://core.trac.wordpress.org/ticket/54042](https://core.trac.wordpress.org/ticket/54042)

<!-- 
### Not use HEREDOC-NOWDOC
 -->
### HEREDOC-NOWDOC の不使用

<!-- 
**Do not use HEREDOC or NOWDOC syntax in your plugins**
 -->
**プラグインで HEREDOC または NOWDOC 構文を使用しないでください**

<!-- 
While both are totally valid, and in many ways desirable features of PHP that allow you to output content, it comes with a cost that is too high for most plugins.
 -->
どちらもまったく有効であり、コンテンツを出力するための PHP の機能としては、多くの点で望ましいものです。これは、ほとんどのプラグインにとって高すぎるコストを伴います。

<!-- 
The primary issue is that most (if not all) codesniffers won't detect lack of escaping in code when you use HEREDOC or NOWDOC. While there are ways around this they have the end result of dashing all that readability to the rubbish pile and leaving you with a jumbled mess that won't properly be scanned.
 -->
主な課題は、HEREDOC や NOWDOC を使用した場合、ほとんどの (すべてではないにせよ) codesniffer がコード内のエスケープの欠如を検出しないことです。これを回避する方法はありますが、せっかくの可読性を台なしにする、正しくスキャンできないゴチャゴチャしたものに、最終的になってしまいます。

<!-- 
We feel the risk here is much higher than the benefits, which is why we don't permit their use.
 -->
私たちは、このリスクはメリットよりもはるかに高いと考え、使用を許可していません。

<!-- 
### Direct file access
 -->
### 直接ファイル・アクセス

<!-- 
**Allowing Direct File Access to plugin files**
 -->
**プラグインファイルへの直接ファイル・アクセスの許可**

<!-- 
Direct file access is when someone directly queries your file. This can be done by simply entering the complete path to the file in the URL bar of the browser but can also be done by doing a POST request directly to the file. For files that only contain a PHP class the risk of something funky happening when directly accessed is pretty small. For files that contain procedural code, functions and function calls, the chance of security risks is a lot bigger.
 -->
直接ファイル・アクセスとは、誰かがあなたのファイルに直接クエリーを行うことです。これは、単純にブラウザの URL バーにファイルへのフルパスを入力で可能ですが、ファイルに直接 POST リクエストを行うことでも可能です。PHP のクラスを含むだけのファイルでは、直接アクセスしたときに何かおかしなことが起こる危険性はほとんどありません。手続きコード、関数、関数呼び出しを含むファイルでは、セキュリティ・リスクの可能性はより大きくなるでしょう。

<!-- 
You can avoid this by putting this code at the top of all PHP files that could potentially execute code if accessed directly :
 -->
直接アクセスするとコードを実行する可能性のある PHP ファイルの先頭に、このコードを記述することで、これを回避できます:

```php
if ( ! defined( 'ABSPATH' ) ) exit; // Exit if accessed directly
```

<!-- 
## Compatibility
 -->
## 互換性

<!-- 
### Prefixing
 -->
### 接頭辞

<!-- 
**Generic function/class/define/namespace/option names**
 -->
**一般的な関数名/クラス名/定義名/名前空間名/オプション名**

<!-- 
All plugins must have unique function names, namespaces, defines, class and option names. This prevents your plugin from conflicting with other plugins or themes. We need you to update your plugin to use more unique and distinct names.
 -->
すべてのプラグインは、固有の関数名、名前空間、定義、クラス名、オプション名を持つ必要があります。これはプラグインが他のプラグインやテーマと衝突するのを防ぐためです。よりユニークで明確な名前を使用するようにプラグインを更新する必要があります。

<!-- 
A good way to do this is with a prefix. For example, if your plugin is called "Easy Custom Post Types" then you could use names like these:
 -->
これを行う良い方法は、接頭辞を使うことです。たとえば、あなたのプラグインが「Easy Custom Post Types」という名前なら、以下のような名前を使うことができます:

<!-- 
- function ecpt_save_post()
- class ECPT_Admin{}
- namespace ECPT;
- update_option( 'ecpt_settings', $settings );
- define( 'ECPT_LICENSE', true );
- global $ecpt_options;
 -->
- `function ecpt_save_post()`
- `class ECPT_Admin{}`
- `namespace ECPT;`
- `update_option( 'ecpt_settings', $settings );`
- `define( 'ECPT_LICENSE', true );`
- `global $ecpt_options;`

<!-- 
Don't try to use two (2) or three (3) letter prefixes anymore. We host nearly 100-thousand plugins on WordPress.org alone. There are tens of thousands more outside our servers. Believe us, you’re going to run into conflicts.
 -->
2文字や3文字の接頭辞を、使用しようと思わないでください。私たちは WordPress.org だけで10万近いプラグインをホストしています。私たちのサーバーの外には、さらに何万ものプラグインがあります。WordPress.org だけを見ていると、あなたは衝突することになるでしょう。

<!-- 
You also need to avoid the use of __ (double underscores), wp_ , or _ (single underscore) as a prefix. Those are reserved for WordPress itself. You can use them inside your classes, but not as stand-alone function.
 -->
また、接頭辞として、`__` (ダブル・アンダースコア)、`wp_`、`_` (シングル・アンダースコア) の使用も避ける必要があります。これらは WordPress 自身のために予約されています。クラスの中で使うことはできますが、独立した関数として使うことはできません。

<!-- 
Please remember, if you're using _n() or __() for translation, that's fine. We're **only** talking about functions you've created for your plugin, not the core functions from WordPress. In fact, those core features are why you need to not use those prefixes in your own plugin! You don't want to break WordPress for your users.
 -->
翻訳のために `_n()` や `__()` を使っているのであれば、それはそれでかまわないので、覚えておいてください。WordPress のコア機能ではなく、プラグイン用に作成した機能について **だけ** 話しています。実際、そのようなコア機能があるからこそ、独自のプラグインではそのような接頭辞を使わないようにする必要があるのです ! ユーザーのために WordPress を壊したくはないでしょう。

<!-- 
Related to this, using if (!function_exists('NAME')) { around all your functions and classes sounds like a great idea until you realize the fatal flaw. If something else has a function with the same name and their code loads first, your plugin will break. Using if-exists should be reserved for shared libraries only.
 -->
これに関連して、すべての関数やクラスで `if (!function_exists('NAME')) {` を使うのは、致命的な欠点に気付くまでは、すばらしいアイデアのように聞こえます。もし他が同じ名前の関数を持っていて、そのコードが先にロードされると、あなたのプラグインは壊れてしまいます。if-exists を使うのは、共有ライブラリだけにしましょう。

<!-- 
Remember: Good prefix names are unique and distinct to your plugin. This will help you and the next person in debugging, as well as prevent conflicts.
 -->
覚えておいてください: 良い接頭辞名は、あなたのプラグインに固有のものです。これは、あなたや次の人のデバッグに役立ちますし、競合を防ぐこともできます。

<!-- 
### PHP
 -->
### PHP

<!-- 
#### PHP: Do not use Short Tags
 -->
#### PHP: ショートタグを使用しない

<!-- 
The primary issue with PHP's short tags is that PHP managed to choose a tag (`<?`) that was used by another syntax: XML. This is a big issue when you consider how common XML parsing and management is.
 -->
PHP のショートタグの主な課題は、PHP が他の構文 (つまり、XML) で使われているタグ (`<?`) を選んでしまったことです。これは、XML の解析や管理がいかに一般的であるかを考えると大きな課題です。

<!-- 
We know as of PHP 5.4, `<?= ... ?>` tags are supported everywhere, regardless of short tags settings. This should mean they're safe to use in portable code but in reality that has proven not to be the case. Add on to that the fact that many codesniffers won't detect lack of escaping in code when you use short-tags, and it becomes not worth the headache for anyone.
 -->
PHP 5.4では、ショートタグの設定にかかわらず、`<?= ... ?>` タグがサポートされています。これは、移植可能なコードで使用しても安全であることを意味するはずだが、現実にはそうではないことが証明されています。さらに、多くの codesniffer は、ショートタグを使用している場合、コード内のエスケープの欠如を検出しないという事実も加わり、誰にとっても頭痛の種にする価値はなくなります。

<!-- 
Basically the risk here is way higher than the benefits, which is why we don't permit their use.
 -->
基本的に、ここでのリスクはメリットよりもはるかに高いのです。それが、私たちが使用を許可しない理由です。

<!-- 
#### PHP: Changing Settings globally
 -->
#### PHP: グローバルに設定の変更

<!-- 
**Don't Force Set PHP Settings Globally**
 -->
**PHP の設定をグローバルに強制設定しない**

<!-- 
While many plugins can need optimal settings for PHP, we ask you please not set them as global defaults.
 -->
多くのプラグインは PHP に最適な設定を必要としますが、グローバルなデフォルト設定にしないようお願いします。

<!-- 
Having defines like ini_set('memory_limit', '-1'); run globally (like on init or in the __construct() part of your code) means you'll be running that for everything on the site, which may cause your users to fall out of compliance with any limits or restrictions on their host.
 -->
(`init` またはコードの `__construct()` 部分のように) `ini_set('memory_limit', '-1');` のような定義をグローバルに実行することは、サイト上のすべてのものに対してそれを実行することを意味します。これは、あなたのユーザーが、そのホストの制限や制約のコンプライアンスから外れてしまう可能性があります。

<!-- 
If you must use those, you need to limit them specifically to only the exact functions that require them.
 -->
どうしても使いたいのであれば、それを必要とする機能だけに限定する必要があります。

<!-- 
#### PHP: Setting a default timezone
 -->
#### PHP: デフォルト・タイムゾーンの設定

<!-- 
This is rarely a good idea. People should be able to define their own timezones in WordPress.
 -->
これはほとんど良いアイデアとは言えません。人々は WordPress で独自のタイムゾーンを定義できるはずです。

<!-- 
Also WordPress explicitly sets and expects the default timezone to be UTC (in settings.php) and the date/time functions sometimes rely on the fact that the default timezone is UTC. For instance if you do date_default_timezone_set(get_option('timezone_string')) and then later try to get a GMT timestamp from get_post_time() or get_post_modified_time(), it will fail to give you the right date.
 -->
また、WordPress は、デフォルトのタイムゾーンを明示的に UTC に設定しており (settings.php 内)、日付/時刻関数は、デフォルトのタイムゾーンが UTC であることに依存していることがあります。たとえば、`date_default_timezone_set(get_option('timezone_string'))` と入力した後に、`get_post_time()` や `get_post_modified_time()` から GMT タイムスタンプを取得しようとすると、正しい日付を取得できません。

<!-- 
#### PHP: Error reporting
 -->
#### PHP: エラー・レポート

<!-- 
**Don't Use Error Reporting in Production Code**
 -->
**プロダクション・コードで、エラー・レポートを使用しない**

<!-- 
While error_reporting() is a great tool in PHP ( [https://www.php.net/manual/en/function.error-reporting.php](https://www.php.net/manual/en/function.error-reporting.php) ) but if you set it permanently in your plugin, you mess things up for everyone who uses your code. Should they have a reason to try to debug their site which happens to use your code, they won't be able to get a clean test because you're messing with the output. It has no place in the day to day function of your plugin.
 -->
`error_reporting()` は、PHP ではすばらしいツールです ( [https://www.php.net/manual/en/function.error-reporting.php](https://www.php.net/manual/en/function.error-reporting.php) ) が、これをプラグインに恒久的に設定すると、あなたのコードを使うすべての人に迷惑をかけることになります。仮に、あなたのコードが使われているサイトをデバッグしようとする理由があったとしても、あなたが出力をいじっているせいで、彼らはクリーンなテストを受けることができません。これは、プラグインの日常的な機能には関係ありません。

<!-- 
### Plugin standards
 -->
### プラグイン標準

<!-- 
#### Main file convention
 -->
#### メインファイル規約

<!-- 
**The main file of the plugin has a name that does not follow the convention.**
 -->
**プラグインのメイン・ファイルには、慣例に従わない名前がついています。**

<!-- 
We expect the main plugin file (the file containing the plugin headers) to have the same name as the plugin folder, which is also the same name as the slug / permalink of the plugin.
 -->
メインプラグインファイル (プラグインヘッダーを含むファイル) は、プラグインフォルダーと同じ名前であることを期待され、それはプラグインのスラッグ/パーマリンクと同じ名前でもあります。

<!-- 
For example, if your plugin slug is `ecpt-social-manager` we expect your main plugin filename to be `ecpt-social-manager.php`.
 -->
たとえば、プラグインのスラッグが `ecpt-social-manager` であれば、メイン・プラグインのファイル名は `ecpt-social-manager.php` になるでしょう。

<!-- 
Note that using some common names as the filename for the main plugin file can lead to issues in some configurations.
 -->
メインのプラグインファイルのファイル名として、一般的な名前を使用すると、構成によっては課題が発生する可能性があることに注意してください。

<!-- 
Please check out our tips on how to [structure files and folders in a plugin](https://developer.wordpress.org/plugins/plugin-basics/best-practices/#folder-structure).
 -->
[プラグイン内のファイルやフォルダの構造化](https://developer.wordpress.org/plugins/plugin-basics/best-practices/#folder-structure)の方法についてのヒントをご覧ください。

<!-- 
#### Incomplete Headers
 -->
#### 不完全なヘッダー

<!-- 
Your headers are either missing or incomplete.
 -->
ヘッダーが欠けているか、不完全です。

<!-- 
Please review [Header Requirements](https://developer.wordpress.org/plugins/the-basics/header-requirements/) and update your plugin accordingly, putting the headers in only the main file.
 -->
[ヘッダーの必要条件](https://developer.wordpress.org/plugins/the-basics/header-requirements/)を確認し、それに従ってプラグインを更新して、ヘッダーをメインファイルだけに置いてください。

<!-- 
#### Incomplete Readme
 -->
#### 不完全な Readme

<!-- 
Your readme is either missing or incomplete.
 -->
Readme が欠けているか、不完全です。

<!-- 
In some cases, such as for first plugins, ones with dependencies, or plugins that call external services, we require you to provide a complete readme. This means your readme has to have headers as well as a proper description and documentation as to how it works and how one can use it.
 -->
最初のプラグイン、依存関係のあるプラグイン、外部サービスを呼び出すプラグインなど、場合によっては、完全な Readme を提供する必要があります。つまり、Readme には、ヘッダーだけでなく、どのように動作し、どのように使用できるのかについての適切な説明やドキュメントが必要です。

<!-- 
Our goal with this is to make sure everyone knows what they're installing and what they need to do before they install it. No surprises. This is especially important if your plugin is making calls to other servers. You are expected to provide users with all the information they need before they install your plugin.
 -->
私たちのこうしたゴールは、インストールする前に、「インストールするもの」と「するべきもの」を皆さんに知ってもらうことです。サプライズはありません。あなたのプラグインが他のサーバーを呼び出す場合、これは特に重要です。プラグインをインストールする前に、ユーザーに必要なすべての情報を提供することが求められます。

<!-- 
Your readme also must validate per [Validator](https://wordpress.org/plugins/about/validator/) or we will reject it. Keep in mind, we don't want to see a readme.MD. While they can work, a readme.txt file will always be given priority, and not all of the markdown will work as expected.
 -->
あなたの Readme も [Validator](https://ja.wordpress.org/plugins/about/validator/) に従って検証されなければなりません。さもなければ、リジェクトします。私たちは readme.md を見たくないことを覚えておいてください。readme.md は機能しますが、readme.txt が常に優先され、すべての Markdown が期待通りに機能するわけではありません。

<!-- 
We ask you please create your readme one based on this: [https://wordpress.org/plugins/readme.txt](https://wordpress.org/plugins/readme.txt)
 -->
Readme はこちらを参考に作成してください: [https://ja.wordpress.org/plugins/readme.txt](https://ja.wordpress.org/plugins/readme.txt)

<!-- 
#### No GPL-compatible license declared
 -->
#### GPL 互換ライセンスの宣言なし

<!-- 
It is necessary to declare the license of this plugin. You can do this using the fields available both in the plugin readme and in the plugin headers.
 -->
このプラグインのライセンスを宣言する必要があります。これは、プラグインの readme とプラグインヘッダーの両方で利用可能なフィールドを使用して行うことができます。

<!-- 
Remember that all code, data, and images — anything stored in the plugin directory hosted on WordPress.org — must comply with the GPL or a GPL-Compatible license. Included third-party libraries, code, images, or otherwise, must be also compatible.
 -->
すべてのコード、データ、画像 - WordPress.org でホストされているプラグイン・ディレクトリに登録されているもの - は、GPL または GPL 互換ライセンスに準拠しなければならないことを覚えておいてください。搭載されるサードパーティのライブラリ、コード、画像、その他も、互換性がなければなりません。

<!-- 
For a specific list of compatible licenses, [please read the GPL-Compatible license list on gnu.org](https://www.gnu.org/licenses/license-list.html#GPLCompatibleLicenses).
 -->
互換性のあるライセンスの具体的なリストについては、[gnu.orgのGPL互換ライセンス・リストをご覧ください](https://www.gnu.org/licenses/license-list.html#GPLCompatibleLicenses)。

<!-- 
#### Incorrect Stable Tag
 -->
#### 不正確な Stable Tag

<!-- 
In your readme, your 'Stable Tag' does not match the Plugin Version as indicated in your main plugin file.
 -->
Readme にある「Stable Tag」が、メインプラグインファイルに記載されているプラグインバージョンと一致していません。

<!-- 
Your Stable Tag is meant to be the stable version of your plugin, not of WordPress. For your plugin to be properly downloaded from WordPress.org, those values need to be the same. If they're out of sync, your users won't get the right version of your code.
 -->
Stable Tag は、WordPress の安定版ではなく、あなたのプラグインの安定版を意味します。あなたのプラグインが WordPress.org から適切にダウンロードされるためには、これらの値が同じである必要があります。これらの値が同期されていないと、ユーザーは正しいバージョンのコードを取得できません。

<!-- 
We recommend you use Semantic Versioning (aka SemVer) for managing versions:
 -->
バージョン管理には、Semantic Versioning (別名 SemVer) を使用することをおすすめします:

<!-- 
- [Software Versioning](https://en.wikipedia.org/wiki/Software_versioning)
- [SemVer](https://semver.org/)
 -->
- [ソフトウェアのバージョン管理](https://en.wikipedia.org/wiki/Software_versioning)
- [SemVer](https://semver.org/)

<!-- 
Please note: While currently using the stable tag of trunk currently works in the Plugin Directory, it's not actually a supported or recommended method to indicate new versions and has been known to cause issues with automatic updates.
 -->
ご注意ください: 現在のところ trunk の stable タグを使用していますが、プラグイン・ディレクトリで動作しています。新しいバージョンを示す方法としては、実はサポートされていないし、推奨もされていませんし、自動アップデートで問題を引き起こすことが知られています。

<!-- 
We ask you please properly use tags and increment them when you release new versions of your plugin, just like you update the plugin version in the main file. Having them match is the best way to be fully forward supporting.
 -->
プラグインの新バージョンをリリースする際には、メインファイルでプラグインのバージョンを更新するように、タグを適切に使用し、インクリメントしてください。タグを一致させることが、完全なフォワード・サポートであるための最善の方法です。

<!-- 
#### Declared license mismatched
 -->
#### 宣言ライセンスの不一致

<!-- 
When declaring the license for this plugin, it has to be the same.
 -->
このプラグインのライセンスを宣言する際には、同じでなければなりません。

<!-- 
Please make sure that you are declaring the same license in both the readme file and the plugin headers.
 -->
readme ファイルとプラグインヘッダーの両方で、同じライセンスを宣言していることを確認してください。

<!-- 
It is fine for this plugin to contain code from other sources under other licenses as long those are well documented and are under GPL or GPL-Compatible license, but we need a sole license declared for your code.
 -->
GPL または GPL 互換ライセンス下で、きちんとドキュメント化されている限り、このプラグインが他ライセンス下で他ソースからのコードを含むことは問題ありませんが、私たちはあなたのコードに対して唯一のライセンスを宣言する必要があります。

<!-- 
### Use HTTP API
 -->
### HTTP API の使用

<!-- 
**Using CURL Instead of HTTP API**
 -->
**HTTP API の代わりに CURL の使用**

<!-- 
WordPress comes with an extensive HTTP API that should be used instead of creating your own curl calls. It’s both faster and more extensive. It’ll fall back to curl if it has to, but it’ll use a lot of WordPress’ native functionality first.
 -->
WordPress には、独自の curl コールを作成する代わりに使用すべき、広範な HTTP API が付属しています。より高速で、より広範囲にわたります。必要であれば curl にフォールバックしますが、WordPress のネイティブ機能の多くを最初に使用します。

<!-- 
[https://developer.wordpress.org/plugins/http-api/](https://developer.wordpress.org/plugins/http-api/)
 -->
[https://developer.wordpress.org/plugins/http-api/](https://developer.wordpress.org/plugins/http-api/)

<!-- 
In case you need, you can use setopt with [https://developer.wordpress.org/reference/hooks/http_api_curl/](https://developer.wordpress.org/reference/hooks/http_api_curl/)
 -->
必要であれば、[https://developer.wordpress.org/reference/hooks/http_api_curl/](https://developer.wordpress.org/reference/hooks/http_api_curl/) で `setopt` を使うことができます。

<!-- 
Please note: If you're using CURL in 3rd party vendor libraries, that's permitted. It's in your own code unique to this plugin (or any dedicated WordPress libraries) that we need it corrected.
 -->
ご注意ください: サードパーティ・ベンダーのライブラリで CURL を使用している場合、それは許可されています。修正が必要なのは、このプラグイン独自のコード (または任意の WordPress 専用ライブラリ) です。

<!-- 
### Use wp_enqueue commands
 -->
### wp_enqueue コマンドの使用

<!-- 
Your plugin is not correctly including JS and/or CSS. You should be using the built in functions for this:
 -->
プラグインが JS や CSS を正しくインクルードしていません。これには内蔵関数を使用する必要があります:

<!-- 
When including **JavaScript code** you can use:
 -->
**JavaScript コード** をインクルードする場合は、以下のように使います:

<!-- 
- wp_register_script() and [wp_enqueue_script()](https://developer.wordpress.org/reference/functions/wp_enqueue_script/) to add JavaScript code from a file.
- [wp_add_inline_script()](https://developer.wordpress.org/reference/functions/wp_add_inline_script/) to add inline JavaScript code to previous declared scripts.
 -->
- `wp_register_script()` と [wp_enqueue_script()](https://developer.wordpress.org/reference/functions/wp_enqueue_script/) で、ファイルから JavaScript コードを追加します。
- [wp_add_inline_script()](https://developer.wordpress.org/reference/functions/wp_add_inline_script/) で、以前に宣言されたスクリプトにインライン JavaScript コードを追加します。

<!-- 
When including **CSS** you can use:
 -->
**CSS** をインクルードする場合は、以下のように使います:

<!-- 
- wp_register_style() and [wp_enqueue_style()](https://developer.wordpress.org/reference/functions/wp_enqueue_style/) to add CSS from a file.
- [wp_add_inline_style()](https://developer.wordpress.org/reference/functions/wp_add_inline_style/) to add inline CSS to previously declared CSS.
 -->
- `wp_register_style()` と [wp_enqueue_style()](https://developer.wordpress.org/reference/functions/wp_enqueue_style/) で、ファイルから CSS を追加します。
- [wp_add_inline_style()](https://developer.wordpress.org/reference/functions/wp_add_inline_style/) で、以前に宣言された CSS にインライン CSS を追加します。

<!-- 
Note that as of WordPress 5.7, you can pass attributes like async, nonce, and type by using new functions and filters: [Script Attributes Related Functions in WordPress 5.7](https://make.wordpress.org/core/2021/02/23/introducing-script-attributes-related-functions-in-wordpress-5-7/)
 -->
WordPress 5.7では、新しい関数やフィルターを使うことで、async、nonce、type などの属性を渡すことができる様になりました: [WordPress 5.7 のスクリプト属性関連関数](https://make.wordpress.org/core/2021/02/23/introducing-script-attributes-related-functions-in-wordpress-5-7/)

<!-- 
If you're trying to enqueue on the admin pages you'll want to use the admin enqueues.
 -->
管理者ページでエンキューしようとする場合、管理者エンキューを使いたいでしょう。

<!-- 
- [admin_enqueue_scripts](https://developer.wordpress.org/reference/hooks/admin_enqueue_scripts/)
- [admin_print_scripts](https://developer.wordpress.org/reference/hooks/admin_print_scripts/)
- [admin_print_styles](https://developer.wordpress.org/reference/hooks/admin_print_styles/)
 -->
- [admin_enqueue_scripts](https://developer.wordpress.org/reference/hooks/admin_enqueue_scripts/)
- [admin_print_scripts](https://developer.wordpress.org/reference/hooks/admin_print_scripts/)
- [admin_print_styles](https://developer.wordpress.org/reference/hooks/admin_print_styles/)

<!-- 
### Including Libraries Already In Core
 -->
### すでにコアに含まれているライブラリのインクルード

<!-- 
Your plugin has included a copy of a library that WordPress already includes.
 -->
あなたのプラグインは、WordPress がすでに搭載しているライブラリのコピーを含んでいます。

<!-- 
WordPress includes a number of useful libraries, such as jQuery, Atom Lib, SimplePie, PHPMailer, PHPass, and more. For security and stability reasons, plugins may not include those libraries in their own code, but instead must use the versions of those libraries packaged with WordPress.
 -->
WordPress には、jQuery、Atom Lib、SimplePie、PHPMailer、PHPass などの便利なライブラリが多数搭載されています。セキュリティと安定性の理由から、プラグインはこれらのライブラリを独自のコードにインクルードできませんが、代わりに、WordPress に同梱されているバージョンのライブラリを使用する必要があります。

<!-- 
You can see the list of JS Libraries here:
 -->
JavaScript ライブラリのリストは、こちらでご覧いただけます:

<!-- 
[Default Scripts and JS Libraries included and registered by WordPress](https://developer.wordpress.org/reference/functions/wp_enqueue_script/#default-scripts-and-js-libraries-included-and-registered-by-wordpress)
 -->
[WordPress にインクルードされ登録されている、デフォルトのスクリプトと JavaScript ライブラリ](https://developer.wordpress.org/reference/functions/wp_enqueue_script/#default-scripts-and-js-libraries-included-and-registered-by-wordpress)

<!-- 
While we do not YET have a decent public facing page to list all these libraries, we do have a list here:
 -->
これらすべてのライブラリをリストアップした、きちんとした一般向けのページはまだありませんが、ここにはリストがあります:

<!-- 
[Core Credits](https://meta.trac.wordpress.org/browser/sites/trunk/api.wordpress.org/public_html/core/credits/wp-59.php#L739)
 -->
[Core クレジット](https://meta.trac.wordpress.org/browser/sites/trunk/api.wordpress.org/public_html/core/credits/wp-59.php#L739)

<!-- 
It’s fine to locally include add-ons not in core, but please ONLY add those additional files. For example, you do not need the entire jQuery UI library for one file. If your code doesn't work with the built-in versions of jQuery, it's most likely a noConflict issue.
 -->
core にないアドオンをローカルにインクルードするのはかまいませんが、追加するファイルはそのファイルだけにしてください。たとえば、1つのファイルに対して jQuery UI ライブラリ全体が必要なわけではありません。あなたのコードが jQuery の内蔵バージョンで動作しない場合、それは noConflict の課題である可能性が高いです。

<!-- 
### Internationalization
 -->
### 国際化

<!-- 
#### Internationalization: Using variables
 -->
#### 国際化: 変数の使用

<!-- 
**Internationalization: Don't use variables or defines as text, context or text domain parameters.**
 -->
**国際化: テキスト、コンテキスト、テキスト・ドメインのパラメータとして、変数や define を使用しないでください。**

<!-- 
In order to make a string translatable in your plugin you are using a set of special functions. These functions collectively are known as "gettext".
 -->
プラグインで文字列を翻訳可能にするには、特別な関数のセットを使います。これらの関数を総称して「gettext」と呼びます。

<!-- 
There is a [dedicated team in the WordPress community](https://make.wordpress.org/polyglots/) to translate and help other translating strings of WordPress core, plugins and themes to other languages.
 -->
WordPress core、プラグイン、テーマの文字列の、他の言語への翻訳を支援する [WordPress コミュニティの専任チーム](https://make.wordpress.org/polyglots/) があります。

<!-- 
To make them be able to translate this plugin, please **do not use variables or function calls** for the text, context or text domain parameters of any gettext function, all of them **NEED to be strings**. Note that the translation parser reads the code without executing it, so it won't be able to read anything that is not a string within these functions.
 -->
このプラグインを翻訳できるようにするには、gettext 関数の text、context、または text domain のパラメータには **変数や関数呼び出しを使わないでください**。これらはすべて **文字列でなければなりません**。翻訳パーサーはコードを実行せずに読み込むため、これらの関数内で非文字列を読み取ることはできないことに注意してください。

<!-- 
For example, if your gettext function looks like this...
 -->
たとえば、gettext 関数が次のようなものだとすると…

`esc_html__( $greetings , 'plugin-slug' );`

<!-- 
...the translator won't be able to see anything to be translated as `$greetings` is not a string, it is not something that can be translated.
You need to give them the string to be translated, so they can see it in the translation system and can translate it, the correct would be as follows...
 -->
…`$greetings` は文字列ではないので、翻訳者は翻訳されるものを見ることができず、翻訳できるようなものは何もありません。翻訳する文字列を伝える必要があります。そうすれば、彼らは翻訳システムでそれを見ることができ、翻訳でき、正しくは次のようになります…

`esc_html__( 'Hello, how are you?' , 'plugin-slug' );`

<!-- 
This also applies to the translation domain, this is a bad call:
 -->
これは翻訳ドメインにも当て嵌まります。こちらは、悪い呼び出し:

`esc_html__( 'Hello, how are you?' , $plugin_slug );`

<!-- 
The fix here would be like this:
 -->
この修正は、次のようなものでしょう:

`esc_html__( 'Hello, how are you?' , 'plugin-slug' );`

<!-- 
Also note that the translation domain needs to be the same as your plugin slug.
 -->
また、翻訳ドメインは、プラグインのスラッグと同じである必要があることに注意してください。

<!-- 
What if we want to include a dynamic value inside the translation? Easy, you need to add a placeholder which will be part of the string and change it after the gettext function does its magic, you can use `printf` to do so, like this:
 -->
翻訳文の中に動的な値を含めたい場合は、どうすればいいのでしょう ? 簡単です。文字列の一部となるプレースホルダを追加し、gettext 関数が魔法をかけた後にそれを変更する必要があります。そのためには、次のように `printf` を使います:

```php
printf(
    /* translators: %s: First name of the user */
    esc_html__( 'Hello %s, how are you?', 'plugin-slug' ),
    esc_html( $user_firstname )
);
```

<!-- 
You can read [more information here](https://developer.wordpress.org/plugins/internationalization/how-to-internationalize-your-plugin/#text-domains).
 -->
[詳しくはこちら](https://developer.wordpress.org/plugins/internationalization/how-to-internationalize-your-plugin/#text-domains)をご覧ください。

<!-- 
## Compliance
 -->
## 遵守

<!-- 
### Changing Active Plugins
 -->
### アクティブ・プラグインの変更

<!-- 
It is not allowed for plugins to change the activation status of other plugins, this is an action that must be performed by the user.
 -->
プラグインが他のプラグインの有効化ステータスを変更することは許可されていません。これはユーザーが行うべき行為です。

<!-- 
It is also not allowed to interfere with the user's actions when activating or deactivating a plugin, unless that's done to prevent errors (For example: When your plugin depends on another plugin, deactivate your own plugin when that other plugin is not active).
 -->
また、エラーを防ぐために行われる場合を除き、プラグインを有効化または無効化する際に、ユーザーの操作を妨害することも禁じられています (たとえば: 自分のプラグインが他のプラグインに依存している場合、他のプラグインが有効でないときに自分のプラグインを無効にする)。

<!-- 
WordPress 6.5 introduces [Plugin Dependencies](https://make.wordpress.org/core/2024/03/05/introducing-plugin-dependencies-in-wordpress-6-5/), you can use it to manage dependencies (although it's fine if you use this as a fallback).
 -->
WordPress 6.5で [Plugin Dependencies](https://make.wordpress.org/core/2024/03/05/introducing-plugin-dependencies-in-wordpress-6-5/) が導入され、依存関係の管理に使えるようになりました (これを、機能や性能を制限して動かす、フォールバックとして利用する分には、かまいませんが)。

<!-- 
### Update checker
 -->
### 更新チェッカー

<!-- 
**Including An Update Checker / Changing Updates functionality**
 -->
**更新チェッカーの搭載 / アップデート機能の変更**

<!-- 
Please remove the checks you have in your plugin to provide for updates.
 -->
アップデートを提供するためにプラグインで行っているチェックを、削除してください。

<!-- 
We do not permit plugins to phone home to other servers for updates, as we are providing that service for you with WordPress.org hosting. One of our guidelines is that you actually use our hosting, so we need you to remove that code.
 -->
私たちは WordPress.org ホスティングでサービスを提供しているため、プラグインがアップデートのために他のサーバーに接続することを許可していません。私たちのガイドラインの一つは、あなたが実際に私たちのホスティングを使用することですので、あなたはそのコードを削除する必要があります。

<!-- 
We also ask that plugins not interfere with the built-in updater as it will cause users to have unexpected results with WordPress 5.5 and up.
 -->
また、プラグインが内蔵アップデータを妨害しないようにお願いします。WordPress 5.5以上で、予期せぬ結果を引き起こす可能性があります。

<!-- 
### Undocumented 3rd party
 -->
### ドキュメント化されていないサードパーティ

<!-- 
**Undocumented use of a 3rd Party or external service**
 -->
**サードパーティまたは外部サービスの、ドキュメント化されていない使用**

<!-- 
We permit plugins to require the use of 3rd party (i.e. external) services, provided they are properly documented in a clear manner.
 -->
私たちは、プラグインがサードパーティ (つまり外部) のサービスの利用を要求することを許可しています。ただし、それらが明確な方法で適切にドキュメント化されている場合に限ります。

<!-- 
We require plugins that reach out to other services to disclose this, in clear and plain language, so users are aware of where data is being sent. This allows them to ensure that any legal issues with data transmissions are covered. This is true even if you are the 3rd party service.
 -->
私たちは、データがどこに送信されるかをユーザーが認識できるように、他のサービスにアクセスするプラグインには、明確でわかりやすい言葉でこれを開示するよう要求しています。これにより、データ送信に関するあらゆる法的課題を確実にカバーできます。これは、あなたがサードパーティのサービスであっても同じです。

<!-- 
In order to do so, you must update your readme to do the following:
 -->
そのためには、readme を以下のように更新する必要があります:

<!-- 
- Clearly explain that your plugin is relying on a 3rd party as a service and under what circumstances
- Provide a link to the service.
- Provide a link to the service terms of use and/or privacy policies.
 -->
- あなたのプラグインがサービスとしてサードパーティに依存していること、そしてどのような状況下にあるのかの、明確な説明。
- サービスへのリンクの提供。
- サービスの利用規約および/またはプライバシーポリシーへのリンクの提供。

<!-- 
Remember, this is for your own legal protection. Use of services must be upfront and well documented.
 -->
これはあなた自身の法的保護のためであることを忘れないでください。サービスの利用は、前もって、しっかりとドキュメント化されなければなりません。

<!-- 
### Included Unneeded Folders
 -->
### 不必要フォルダーを含む

<!-- 
This plugin includes folders and files that looks like are not required for the running of your plugin. Some examples are:
 -->
このプラグインには、プラグインの実行には必要ないと思われるフォルダーやファイルが含まれています。例としては:

<!-- 
- development tools
- unneeded vendor folders for production (bower, node, grunt, etc)
- demos
- unit tests
 -->
- 開発ツール
- 製品用に不要なベンダーフォルダー (bower、node、grunt など)
- デモ
- ユニットテスト

<!-- 
If you're trying to include the human-readable version of your own code (in order to comply with our guidelines) that's fine, remember that we also permit you to put links to them in your readme.
 -->
(私たちのガイドラインに準拠するために) 独自コードの人間が読めるバージョンを含めようとしているのであれば、それはかまいません。Readme にリンクを貼ることも許可していることを忘れないでください。

<!-- 
You should also keep and/or link configuration files, as for example, the `composer.json` file in order to allow others to review, study, and yes, fork this code.
 -->
また、たとえば、`composer.json` ファイルのような構成ファイルを保管したりリンクしたりして、他の人がこのコードをレビューしたり、研究したり、フォークしたりできるようにしておく必要があります。

<!-- 
[Detailed Plugin Guidelines](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/#4-code-must-be-mostly-human-readable)
 -->
[詳細なプラグインガイドライン](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/#4-code-must-be-mostly-human-readable)

<!-- 
But you can, and should, safely remove those other unneeded folders from your plugins.
 -->
しかし、プラグインから他の不要なフォルダーを安全に削除できるし、そうするべきです。

<!-- 
### Not permitted files
 -->
### 未許可ファイル

<!-- 
A plugin typically consists of files related to the plugin functionality (php, js, css, txt, md) and maybe some multimedia files (png, svg, jpg) and / or data files (json, xml).
 -->
プラグインは通常、プラグインの機能に関連するファイル (php、js、css、txt、md) と、マルチメディアファイル (png、svg、jpg)、および/またはデータファイル (json、xml) で構成されます。

<!-- 
We have detected files that are not among of the files normally found in a plugin, are they necessary? If not, then those won't be allowed.
 -->
プラグインに通常含まれないファイルを検出しました。それらは必要ですか ? でなければ、それらは許可されません。

<!-- 
#### Including code from a "premium" source
 -->
#### 「プレミアム」ソースのコード搭載

<!-- 
Some premium libraries are specifically not permitted to be included in free (WordPress.org hosted) plugins. Those must be removed.
 -->
一部のプレミアムライブラリは、無償 (WordPress.org ホスト) プラグインに含めることを、特に許可されていません。それらは削除しなければなりません。

<!-- 
### GPL
 -->
### GPL

<!-- 
#### GPL: Non-GPL compatible Code Included
 -->
#### GPL: 非 GPL 互換コードの搭載

<!-- 
It's required that all code be compatible with the GPLv2 (or later) license in order to be included in our directory.
 -->
私たちのディレクトリに収録されるためには、すべてのコードが GPLv2 (またはそれ以降) ライセンスと互換性があることが要求されます。

<!-- 
You must remove the code and alter the plugin so it is not required. We suggest you find code that is GPL compatible and use that instead. For more information on what types of licenses are compatible with GPL, please review the following links:
 -->
そのコードを削除し、プラグインを変更する必要がありますから、それは要求されません。GPL 互換のコードを見つけて、それを代わりに使うことをおすすめします。どのような種類のライセンスが GPL 互換なのかについては、以下のリンクをご覧ください:

<!-- 
- [GNU Licenses - License List](https://www.gnu.org/licenses/license-list.html)
- [GPL FAQ - All Compatibility](https://www.gnu.org/licenses/gpl-faq.html#AllCompatibility)
 -->
- [GNU ライセンス - ライセンス一覧](https://www.gnu.org/licenses/license-list.html)
- [GPL FAQ - すべての互換性](https://www.gnu.org/licenses/gpl-faq.html#AllCompatibility)

<!-- 
#### GPL: No publicly documented resource
 -->
#### GPL: 一般に開示されたリソースがない

<!-- 
**No publicly documented resource for your compressed content**
 -->
**圧縮コンテンツについて、公的にドキュメント化されたリソースがない**

<!-- 
In reviewing your plugin, we cannot find a non-compiled version of your javascript and/or css related source code.
 -->
プラグインをレビューしたところ、未コンパイル版の javascript および/または css 関連のソースコードが見つかりませんでした。

<!-- 
In order to comply with our guidelines of human-readable code, we require you to include the source code and/or a link to the non-compressed, developer libraries you’ve included in your plugin. If you include a link, this may be in your source code, however we require you to also have it in your readme.
 -->
私たちのガイドラインである「人間が読めるコード」に準拠するために、あなたのプラグインに搭載される非圧縮の開発者ライブラリへのソースコードやリンクを含めることを要求します。リンクを含める場合、ソースコードに書いてもかまいませんが、必ず readme にも書いてください。

<!-- 
[Detailed Plugin Guidelines](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/#4-code-must-be-mostly-human-readable)
 -->
[詳細なプラグインガイドライン](https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/#4-code-must-be-mostly-human-readable)

<!-- 
We strongly feel that one of the strengths of open source is the ability to review, observe, and adapt code. By maintaining a public directory of freely available code, we encourage and welcome future developers to engage with WordPress and push it forward.
 -->
私たちは、オープンソースの強みの一つは、コードをレビューし、観察し、適応させる能力であると強く感じています。自由に利用できるコードの公開ディレクトリを維持することで、私たちは将来の開発者が WordPress に関わり、WordPress を前進させることを奨励し、歓迎します。

<!-- 
That said, with the advent of larger and larger plugins using more complex libraries, people are making good use of build tools (such as composer or npm) to generate their distributed production code. In order to balance the need to keep plugin sizes smaller while still encouraging open source development, we require plugins to make the source code to any compressed files available to the public in an easy to find location, by documenting it in the readme.
 -->
とはいえ、より大規模なプラグインが登場し、より複雑なライブラリが使われるようになり、人々は (Composer や npm のような) ビルドツールをうまく利用して、分散されたプロダクションコードを生成しています。プラグインのサイズを小さく保つ必要性と、オープンソースの開発を奨励する必要性とのバランスをとるため、私たちはプラグインに、圧縮ファイルのソースコードを readme でドキュメント化し、見つけやすい場所で公開することを要求します。

<!-- 
For example, if you’ve made a Gutenberg plugin and used npm and webpack to compress and minify it, you must either include the source code within the published plugin or provide access to a public maintained source that can be reviewed, studied, and yes, forked.
 -->
たとえば、Gutenberg プラグインを作成し、npm と webpack を使って圧縮と最小化した場合、公開プラグイン内のソースコードをインクルードするか、レビュー可能で、研究可能で、そしてフォーク可能な、公開メンテナンスされたソースへのアクセスを提供する必要があります。

<!-- 
We strongly recommend you include directions on the use of any build tools to encourage future developers.
 -->
将来の開発者を奨励するため、ビルドツールの使用方法を記載することを強くおすすめします。

<!-- 
#### GPL: Using composer but no composer.json file
 -->
#### GPL: Composer の使用で `composer.json` ファイルがない

<!-- 
We noticed that your plugin is using Composer to handle library dependencies, that's great as it will help maintaining and updating your plugin in the future while avoiding collisions with other plugins that are using same libraries.
 -->
あなたのプラグインが Composer を使ってライブラリの依存関係を処理していることに気付きました。同じライブラリを使用している他のプラグインとの衝突を避けながら、将来あなたのプラグインを保守・更新するのに役立つので、それはすばらしいことです。

<!-- 
The `composer.json` file describes the dependencies of your project and may contain other metadata as well. It's a small file that typically can be found in the top-most directory of your plugin.
 -->
`composer.json` ファイルには、プロジェクトの依存関係が記述されており、その他のメタデータも含まれている場合があります。これは小さなファイルで、通常はプラグインの一番上のディレクトリに存在します。

<!-- 
As one of the strengths of open source is the ability to review, observe, and adapt code, **we would like to ask you to include that file in your plugin**, even if it is only used for development purposes. This will allow others to exercise the open source freedoms from which we all benefit.
 -->
オープンソースの強みの一つは、コードをレビューし、観察し、適応させる能力であるため、たとえそれが開発目的にのみ使用されるとしても、**そのファイルをあなたのプラグインに含めるようお願いします**。そうすることで、私たち全員が恩恵を受けているオープンソースの自由を、他の人たちも行使できます。