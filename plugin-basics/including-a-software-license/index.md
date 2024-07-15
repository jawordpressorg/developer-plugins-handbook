<!-- 
# Including a Software License
 -->
# ソフトウェアライセンスの包含

<!-- 
Most WordPress plugins are released under the [GPL](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html), which is the same license that [WordPress itself uses](https://wordpress.org/about/license/). However, there are other compatible options available. It is always best to clearly indicate the license your plugin uses.
 -->
ほとんどの WordPress プラグインは [GPL](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html) の下でリリースされており、これは [WordPress 自体が使用している](https://wordpress.org/about/license/)ライセンスと同じです。しかし、他にも互換性のあるオプションがあります。プラグインが使用しているライセンスを明示するのが常にベストです。

<!-- 
In the [Header Requirements](https://developer.wordpress.org/plugins/plugin-basics/header-requirements/) section, we briefly mentioned how you can indicate your plugin's license within the plugin header comment. Another common, and encouraged, practice is to place a license block comment near the top of your main plugin file (the same one that has the plugin header comment).
 -->
[ヘッダーの必要条件](https://developer.wordpress.org/plugins/plugin-basics/header-requirements/)のセクションで、プラグインのライセンスをプラグインヘッダーのコメントで示す方法について簡単に触れました。もう一つの一般的で推奨される方法は、メインのプラグインファイルの一番上にライセンスブロックのコメント (プラグインヘッダーのコメントと同じもの) を置くことです。

<!-- 
This license block comment usually looks something like this:
 -->
このライセンス・ブロックのコメントは、通常次のようになります:

```
/*
{Plugin Name} is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 2 of the License, or
any later version.

{Plugin Name} is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with {Plugin Name}. If not, see {URI to Plugin License}.
*/
```
