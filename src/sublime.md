# sublime

## setting

```json
{
  "always_show_minimap_viewport": true,
  "caret_style": "phase",
  "color_scheme": "Packages/User/SublimeLinter/base16-eighties.dark (SL).tmTheme",
  "css":
  {
    "indent_char": " ",
    "indent_size": 2
  },
  "enable_tab_scrolling": false,
  "folder_exclude_patterns":
  [
    ".svn",
    ".git",
    "node_modules",
    ".hg",
    "CVS"
  ],
  "font_options":
  [
    "gray_antialias",
    "subpixel_antialias"
  ],
  "font_size": 16,
  "highlight_line": true,
  "highlight_modified_tabs": true,
  "html":
  {
    "indent_char": " ",
    "indent_size": 2
  },
  "ignored_packages":
  [
    "Vintage"
  ],
  "indent_guide_options":
  [
    "draw_normal",
    "draw_active"
  ],
  "js":
  {
    "indent_char": " ",
    "indent_size": 2
  },
  "line_padding_bottom": 3,
  "line_padding_top": 3,
  "material_theme_accent_cyan": true,
  "material_theme_compact_sidebar": true,
  "material_theme_contrast_mode": true,
  "material_theme_small_tab": true,
  "material_theme_tabs_autowidth": true,
  "overlay_scroll_bars": "enabled",
  "rulers":
  [
    120
  ],
  "scroll_past_end": true,
  "show_full_path": true,
  "tab_completion": true,
  "tab_size": 2,
  "theme": "Material-Theme-Darker.sublime-theme",
  "translate_tabs_to_spaces": true,
  "vintage_start_in_command_mode": true,
  "word_wrap": true
}
```

## package

- MarkdownLivePreview
- Babel
- BracketHighlighter
- CSS Format
- CSScomb
- DockBlockr
- Emmet
- HTML-CSS-JS Prettify
- jQuery
- jsfmt
- liveStyle
- Meterial Theme
- Package Control
- PyV8
- Sass
- SideBarEnhancements
- SublimeLinter
- Sublimelinter-contrib-standard
- Theme - Spacegray
- TrailingSpaces

在 `~/` 目录增加 `HTML-CSS-JS Prettify` 的配置文件 `.jsbeautifyrc`

```json
{
  "html": {
    "indent_char": " ",
    "indent_size": 2
  },
  "js": {
    "indent_char": " ",
    "indent_size": 2
  },
  "css": {
    "indent_char": " ",
    "indent_size": 2
  }
}
```
