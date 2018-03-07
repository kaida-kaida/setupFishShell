# VSCodeの設定

## setting.json

```
{
    "editor.renderWhitespace": "all",
    "editor.fontFamily": "Chalkboard SE, Monaco, Menlo, Courier New, monospace",
    "editor.fontWeight": "bold",
    "editor.fontSize": 14,
    "editor.tabSize": 4,
    "editor.insertSpaces": true,
    "editor.cursorBlinking": "smooth",
    "files.trimTrailingWhitespace": true,
    "files.insertFinalNewline": true,
    "files.associations": {
        "*.js": "javascript",
        "*.jsx": "javascript",
        ".nycrc": "json",
        ".stylelintrc": "json"
    },
    "markdown.preview.fontFamily": "JKゴシックM, Chalkboard SE",
    "workbench.colorTheme": "Material Theme",
    "workbench.colorCustomizations": {
        "tab.activeBackground": "#745b29",
        "activityBar.background": "#102a5c",
        "editorGroup.background": "#174a9c",
        "sideBar.background": "#132644",
        "editor.background": "#192b2b",
    },
    "workbench.iconTheme": "material-icon-theme",
    "workbench.startupEditor": "newUntitledFile",
    "window.zoomLevel": 0,
    "material-icon-theme.showUpdateMessage": false,
    "javascript.validate.enable": false,
    "explorer.confirmDragAndDrop": false,
    "editor.formatOnSave": false,
    "javascript.format.enable": false,
    "prettier.eslintIntegration": true,
    "stylelint.enable": true,
    "css.validate": false,
    "scss.validate": false,
    "extensions.ignoreRecommendations": true,
    "explorer.confirmDelete": false
}

```

prettierをONにする時は
`"editor.formatOnSave": true`
にする。

## plugin
- Auto Rename Tag
- Auto-Open Markdown
- Babel ES6/ES7
- Babel JavaScript
- Bracket Pair Colorizer
- Color Picker
- Docker
- ESLint
- Material Icon Theme
- Material Theme
- Path Intellisense
- Prettier
- stylelint
- Tralling Spaces
