<!-- 
# Using Settings API
 -->
# 設定 API の使用

<!-- 
## Adding Settings
 -->
## 設定の追加

<!-- 
You must define a new setting using [`register_setting()`](https://developer.wordpress.org/reference/functions/register_setting/), it will create an entry in the `{$wpdb->prefix}_options` table.
 -->
[`register_setting()`](https://developer.wordpress.org/reference/functions/register_setting/) を使って新しい設定を定義すると、テーブル `{$wpdb->prefix}_options` にエントリーが作成されます。

<!-- 
You can add new sections on existing pages using [`add_settings_section()`](https://developer.wordpress.org/reference/functions/add_settings_section/).
 -->
既存のページに新しいセクションを追加するには、[`add_settings_section()`](https://developer.wordpress.org/reference/functions/add_settings_section/) を使います。

<!-- 
You can add new fields to existing sections using [`add_settings_field()`](https://developer.wordpress.org/reference/functions/add_settings_field/).
 -->
既存のセクションに新しいフィールドを追加するには、[`add_settings_field()`](https://developer.wordpress.org/reference/functions/add_settings_field/) を使います。

<!-- 
[alert][`register_setting()`](https://developer.wordpress.org/reference/functions/register_setting/) as well as the mentioned `add_settings_*()` functions should all be added to the `admin_init` action hook.[/alert]
 -->
[alert][`register_setting()`](https://developer.wordpress.org/reference/functions/register_setting/) と同様に、前述の関数 `add_settings_*()` もすべてアクションフック `admin_init` に追加されるべきです。[/alert]

<!-- 
### Add a Setting
 -->
### 設定の追加

```
register_setting(
  string $option_group,
  string $option_name,
  callable $sanitize_callback = ''
);
```

<!-- 
Please refer to the Function Reference about [`register_setting()`](https://developer.wordpress.org/reference/functions/register_setting/) for full explanation about the used parameters.
 -->
使用されるパラメータについての完全な説明は、[`register_setting()`](https://developer.wordpress.org/reference/functions/register_setting/) に関する関数リファレンスを参照してください。

<!-- 
### Add a Section
 -->
### セクションの追加

```
add_settings_section(
  string $id,
  string $title,
  callable $callback,
  string $page
);
```

<!-- 
Sections are the groups of settings you see on WordPress settings pages with a shared heading. In your plugin you can add new sections to existing settings pages rather than creating a whole new page. This makes your plugin simpler to maintain and creates fewer new pages for users to learn.
 -->
セクションとは、WordPress の設定ページで見られる、共通の見出しを持つ設定グループのことです。プラグインでは、まったく新しいページを作成するのではなく、既存の設定ページに新しいセクションを追加できます。これにより、プラグインのメンテナンスが簡単になり、ユーザーが学習するための新しいページが少なくなります。

<!-- 
Please refer to the Function Reference about [`add_settings_section()`](https://developer.wordpress.org/reference/functions/add_settings_section/) for full explanation about the used parameters.
 -->
使用されるパラメータについての完全な説明は、[`add_settings_section()`](https://developer.wordpress.org/reference/functions/add_settings_section/) に関する関数リファレンスを参照してください。

<!-- 
### Add a Field
 -->
### フィールドの追加

```
add_settings_field(
  string $id,
  string $title,
  callable $callback,
  string $page,
  string $section = 'default',
  array $args = []
);
```

<!-- 
Please refer to the Function Reference about [`add_settings_field()`](https://developer.wordpress.org/reference/functions/add_settings_field/) for full explanation about the used parameters.
 -->
使用されるパラメータについての完全な説明は、[`add_settings_field()`](https://developer.wordpress.org/reference/functions/add_settings_field/) に関する関数リファレンスを参照してください。

<!-- 
### Example
 -->
### 例

```
function wporg_settings_init() {
  // register a new setting for "reading" page
  register_setting('reading', 'wporg_setting_name');

  // register a new section in the "reading" page
  add_settings_section(
    'wporg_settings_section',
    'WPOrg Settings Section', 'wporg_settings_section_callback',
    'reading'
  );

  // register a new field in the "wporg_settings_section" section, inside the "reading" page
  add_settings_field(
    'wporg_settings_field',
    'WPOrg Setting', 'wporg_settings_field_callback',
    'reading',
    'wporg_settings_section'
  );
}

/**
 * register wporg_settings_init to the admin_init action hook
 */
add_action('admin_init', 'wporg_settings_init');

/**
 * callback functions
 */

// section content cb
function wporg_settings_section_callback() {
  echo '<p>WPOrg Section Introduction.</p>';
}

// field content cb
function wporg_settings_field_callback() {
  // get the value of the setting we've registered with register_setting()
  $setting = get_option('wporg_setting_name');
  // output the field
  ?>
  <input type="text" name="wporg_setting_name" value="<?php echo isset( $setting ) ? esc_attr( $setting ) : ''; ?>">
  <?php
}
```

<!-- 
## Getting Settings
 -->
## 設定の取得

```
get_option(
  string $option,
  mixed $default = false
);
```

<!-- 
Getting settings is accomplished with the [`get_option()`](https://developer.wordpress.org/reference/functions/get_option/) function.
 -->
設定の取得は、関数 [`get_option()`](https://developer.wordpress.org/reference/functions/get_option/) で実現します。

<!-- 
The function accepts two parameters: the name of the option and an optional default value for that option.
 -->
この関数は2つのパラメータを受け付けます。オプションの名前と、そのオプションに対する省略可能なデフォルト値です。

<!-- 
### Example
 -->
### 例

```
// Get the value of the setting we've registered with register_setting()
$setting = get_option('wporg_setting_name');
```