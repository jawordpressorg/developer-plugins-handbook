<!-- 
# Determining Plugin and Content Directories
 -->
# プラグインとコンテンツ・ディレクトリの特定

<!-- 
When coding WordPress plugins you often need to reference various files and folders throughout the WordPress installation and within your plugin or theme.
 -->
WordPress のプラグインをコーディングするとき、WordPress のインストレーション全体やプラグインやテーマ内の、さまざまなファイルやフォルダーを参照する必要があります。

<!-- 
WordPress provides several functions for easily determining where a given file or directory lives. Always use these functions in your plugins instead of hard-coding references to the wp-content directory or using the WordPress internal constants.
 -->
WordPress には、指定したファイルやディレクトリの場所を簡単に特定するための関数がいくつか用意されています。プラグインでは、wp-content ディレクトリへの参照をハードコーディングしたり、WordPress の内部定数を使用したりする代わりに、常にこれらの関数を使用してください。

<!-- 
[tip]WordPress allows users to place their wp-content directory anywhere they want and rename it whatever they want. Never assume that plugins will be in wp-content/plugins, uploads will be in wp-content/uploads, or that themes will be in wp-content/themes.[/tip]
 -->
[tip]WordPress では、wp-content ディレクトリを好きな場所に配置し、好きな名前に変更できます。プラグインは wp-content/plugins に、アップロードは wp-content/uploads に、テーマは wp-content/themes に置くものだとは、決して思わないでください。[/tip]

<!-- 
PHP's `__FILE__` magic-constant resolves symlinks automatically, so if the `wp-content/` or `wp-content/plugins/` or even the individual plugin directory is symlinked, hardcoded paths will not work correctly.
 -->
`wp-content/` や `wp-content/plugins/`、あるいは個々のプラグインディレクトリがシンボリックリンクされている場合、PHP のマジック定数 `__FILE__` は、シンボリックリンクを自動的に解決しますが、ハードコードされたパスは正しく動作しません。

<!-- 
## Common Usage
 -->
## 一般的な使い方

<!-- 
If your plugin includes JavaScript files, CSS files or other external files, then it's likely you'll need the URL to these files so you can load them into the page. To do this you should use the [plugins_url()](https://developer.wordpress.org/reference/functions/plugins_url/) function like so:
 -->
プラグインに JavaScript ファイル、CSS ファイル、その他の外部ファイルが含まれている場合、ページに読み込むためにこれらのファイルの URL が必要になる可能性があります。これを行うには、[plugins_url()](https://developer.wordpress.org/reference/functions/plugins_url/) 関数を次のように使用します:

```
plugins_url( 'myscript.js', __FILE__ );
```

<!-- 
This will return the full URL to myscript.js, such as `example.com/wp-content/plugins/myplugin/myscript.js`.
 -->
これは、`example.com/wp-content/plugins/myplugin/myscript.js` のように、myscript.js への完全な URL を返します。

<!-- 
To load your plugins' JavaScript or CSS into the page you should use [`wp_enqueue_script()`](https://developer.wordpress.org/reference/functions/wp_enqueue_script/) or [`wp_enqueue_style()`](https://developer.wordpress.org/reference/functions/wp_enqueue_style/) respectively, passing the result of `plugins_url()` as the file URL.
 -->
プラグインの JavaScript または CSS をページに読み込むには、それぞれ [`wp_enqueue_script()`](https://developer.wordpress.org/reference/functions/wp_enqueue_script/) または [`wp_enqueue_style()`](https://developer.wordpress.org/reference/functions/wp_enqueue_style/) を使用し、`plugins_url()` の結果をファイルの URL として渡します。

<!-- 
## Available Functions
 -->
## 利用可能な関数

<!-- 
WordPress includes many other functions for determining paths and URLs to files or directories within plugins, themes, and WordPress itself. See the individual DevHub pages for each function for complete information on their use.
 -->
WordPress には、プラグイン、テーマ、WordPress 自体のファイルやディレクトリへのパスや URL を特定するための機能が他にもたくさんあります。各関数の使い方については、それぞれの DevHub ページを参照してください。

<!-- 
### Plugins
 -->
### プラグイン

- [`plugins_url()`](https://developer.wordpress.org/reference/functions/plugins_url/)
- [`plugin_dir_url()`](https://developer.wordpress.org/reference/functions/plugin_dir_url/)
- [`plugin_dir_path()`](https://developer.wordpress.org/reference/functions/plugin_dir_path/)
- [`plugin_basename()`](https://developer.wordpress.org/reference/functions/plugin_basename/)

<!-- 
### Themes
 -->
### テーマ

- [`get_template_directory_uri()`](https://developer.wordpress.org/reference/functions/get_template_directory_uri/)
- [`get_stylesheet_directory_uri()`](https://developer.wordpress.org/reference/functions/get_stylesheet_directory_uri/)
- [`get_stylesheet_uri()`](https://developer.wordpress.org/reference/functions/get_stylesheet_uri/)
- [`get_theme_root_uri()`](https://developer.wordpress.org/reference/functions/get_theme_root_uri/)
- [`get_theme_root()`](https://developer.wordpress.org/reference/functions/get_theme_root/)
- [`get_theme_roots()`](https://developer.wordpress.org/reference/functions/get_theme_roots/)
- [`get_stylesheet_directory()`](https://developer.wordpress.org/reference/functions/get_stylesheet_directory/)
- [`get_template_directory()`](https://developer.wordpress.org/reference/functions/get_template_directory/)

<!-- 
### Site Home
 -->
### サイトのホーム

- [`home_url()`](https://developer.wordpress.org/reference/functions/home_url/)
- [`get_home_path()`](https://developer.wordpress.org/reference/functions/get_home_path/)


### WordPress

- [`admin_url()`](https://developer.wordpress.org/reference/functions/admin_url/)
- [`site_url()`](https://developer.wordpress.org/reference/functions/site_url/)
- [`content_url()`](https://developer.wordpress.org/reference/functions/content_url/)
- [`includes_url()`](https://developer.wordpress.org/reference/functions/includes_url/)
- [`wp_upload_dir()`](https://developer.wordpress.org/reference/functions/wp_upload_dir/)

<!-- 
### Multisite
 -->
### マルチサイト

- [`get_admin_url()`](https://developer.wordpress.org/reference/functions/get_admin_url/)
- [`get_home_url()`](https://developer.wordpress.org/reference/functions/get_home_url/)
- [`get_site_url()`](https://developer.wordpress.org/reference/functions/get_site_url/)
- [`network_admin_url()`](https://developer.wordpress.org/reference/functions/network_admin_url/)
- [`network_site_url()`](https://developer.wordpress.org/reference/functions/network_site_url/)
- [`network_home_url()`](https://developer.wordpress.org/reference/functions/network_home_url/)

<!-- 
## Constants
 -->
## 定数

<!-- 
WordPress makes use of the following constants when determining the path to the content and plugin directories. These should not be used directly by plugins or themes, but are listed here for completeness.
 -->
WordPress は、コンテンツとプラグインのディレクトリへのパスを特定する際に、以下の定数を使用します。これらはプラグインやテーマによって直接使用されるべきものではありませんが、万全を期すためにここに列挙します。

```
WP_CONTENT_DIR  // no trailing slash, full paths only
WP_CONTENT_URL  // full url 
WP_PLUGIN_DIR  // full path, no trailing slash
WP_PLUGIN_URL  // full url, no trailing slash

// Available per default in MS, not set in single site install
// Can be used in single site installs (as usual: at your own risk)
UPLOADS // (If set, uploads folder, relative to ABSPATH) (for e.g.: /wp-content/uploads)
```

<!-- 
## Related
 -->
## 関連

<!-- 
### WordPress Directories
 -->
### WordPress ディレクトリ

<!-- 
| Function | | Directory |
| --- | --- | --- |
| [`home_url()`](https://developer.wordpress.org/reference/functions/home_url/) | Home URL | `https://www.example.com` |
| [`site_url()`](https://developer.wordpress.org/reference/functions/site_url/) | Site directory URL | `https://www.example.com` or `https://www.example.com/wordpress` |
| [`admin_url()`](https://developer.wordpress.org/reference/functions/admin_url/) | Admin directory URL | `https://www.example.com/wp-admin` |
| [`includes_url()`](https://developer.wordpress.org/reference/functions/includes_url/) | Includes directory URL | `https://www.example.com/wp-includes` |
| [`content_url()`](https://developer.wordpress.org/reference/functions/content_url/) | Content directory URL | `https://www.example.com/wp-content` |
| [`plugins_url()`](https://developer.wordpress.org/reference/functions/plugins_url/) | Plugins directory URL | `https://www.example.com/wp-content/plugins` |
| [`wp_upload_dir()`](https://developer.wordpress.org/reference/functions/wp_upload_dir/) | Upload directory URL (returns an array) | `https://www.example.com/wp-content/uploads` |
 -->
| 関数 | | ディレクトリ |
| --- | --- | --- |
| [`home_url()`](https://developer.wordpress.org/reference/functions/home_url/) | ホームの URL | `https://www.example.com` |
| [`site_url()`](https://developer.wordpress.org/reference/functions/site_url/) | Site ディレクトリの URL | `https://www.example.com` or `https://www.example.com/wordpress` |
| [`admin_url()`](https://developer.wordpress.org/reference/functions/admin_url/) | Admin ディレクトリの URL | `https://www.example.com/wp-admin` |
| [`includes_url()`](https://developer.wordpress.org/reference/functions/includes_url/) | Includes ディレクトリの URL | `https://www.example.com/wp-includes` |
| [`content_url()`](https://developer.wordpress.org/reference/functions/content_url/) | Content ディレクトリの URL | `https://www.example.com/wp-content` |
| [`plugins_url()`](https://developer.wordpress.org/reference/functions/plugins_url/) | Plugins ディレクトリの URL | `https://www.example.com/wp-content/plugins` |
| [`wp_upload_dir()`](https://developer.wordpress.org/reference/functions/wp_upload_dir/) | Upload ディレクトリの URL (配列を返す) | `https://www.example.com/wp-content/uploads` |