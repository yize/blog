---
title: 安利一把 Visual Studio Code
date: 2018-01-29 16:39:33
tags: 
- VSCode
- tools
---

> 2018-01-02 14:02:25  
> 经过一年的使用，重新整理了下。


## 总

* **免费**
* 配置方便
* 完善的插件体系
* 速度快，不卡顿（`WebStrom` 重度用户感觉超爽）
* 内置 `Terminal` ，左侧面板支持复制粘贴（`Sublime` 对这个支持不好）
* `ESLint` 和格式化做的很强大，如果当时就知道这玩意，我们第一批标准化的时间会大大减少。


![undefined | center](https://private-alipayobjects.alipay.com/alipay-rmsdeploy-image/skylark/png/25579065-bcca-4af2-8b3e-f9a895f06da3.png "")


## 设置项

```js
{
    "editor.fontFamily": "Fira Code",
    "terminal.integrated.fontFamily": "Fira Code",
    "terminal.integrated.fontSize": 14,
    "editor.fontSize": 14,
    "editor.detectIndentation": true,
    "editor.tabSize": 2,
    // 配置文件路径的 glob 模式以从文件监视排除。更改此设置要求重启。如果在启动时遇到 Code 消耗大量 CPU 时间，则可以排除大型文件夹以减少初始加载。
    "files.watcherExclude": {
        "**/.git/**": true,
        "**/node_modules/**": true,
        "**/bower_components/**": true,
        "**/docs/**": true,
        "**/build/**": true,
        "**/dist/**": true,
        "**/.happypack/**": true,
        "**/.module-cache/**": true,
        "**/.history/**": true,
        "**/.package/**": true,
        "**/*.svg": true,
        "**/*.log": true,
        "**/*.js.map": true,
        "**/*.min.js": true,
        "**/*~*.js": true,
        "**/*.md": true,
        "**/uxcore*.js": true
    },
    // 配置 glob 模式以排除文件和文件夹。
    "files.exclude": {
        "**/.git": true,
        "**/.svn": true,
        "**/.hg": true,
        "**/.DS_Store": true,
        "**/.idea": true,
        "**/node_modules": true,
        "**/dist/**": true,
        "**/.happypack": true,
        "**/.module-cache": true,
        "**/.history": true,
        "**/.package": true
    },
    "search.exclude": {
        "**/.git/**": true,
        "**/node_modules/**": true,
        "**/bower_components/**": true,
        "**/docs/**": true,
        "**/build/**": true,
        "**/dist/**": true,
        "**/.happypack/**": true,
        "**/.module-cache/**": true,
        "**/.history/**": true,
        "**/.package/**": true,
        "**/*.svg": true,
        "**/*.log": true,
        "**/*.js.map": true,
        "**/*.min.js": true,
        "**/*~*.js": true,
        "**/*.md": true,
        "**/uxcore*.js": true
    },
	"search.followSymlinks": false, // 必须加，不然 tnpm 的 link 模块，卡死你。
    "javascript.validate.enable": false, // 跟 eslint 有冲突
    "editor.snippetSuggestions": "inline",
    "extensions.autoUpdate": true,
    "beautify.tabSize": 2,
    "window.nativeTabs": true,
    "workbench.editor.swipeToNavigate": true,
    "editor.minimap.enabled": false,
    "window.zoomLevel": 0,
    "spellright.language": "en",
    "workbench.statusBar.visible": true,
    "terminal.external.osxExec": "iTerm.app",
    "editor.multiCursorModifier": "ctrlCmd",
    "workbench.startupEditor": "welcomePage",
    "explorer.confirmDragAndDrop": false,
    "explorer.confirmDelete": false,
    "git.autofetch": true,
    "git.enableSmartCommit": true,
    "workbench.colorTheme": "Material Theme",
    "editor.fontLigatures": true,
    "liveServer.settings.donotShowInfoMsg": true,
    "editor.quickSuggestions": {
        "other": true,
        "comments": true,
        "strings": true
    },
    "files.associations": {
        "*.html": "html"
    },
    "[html]": {},
    "editor.formatOnSave": true,
    "prettier.eslintIntegration": true,
    "gitlens.advanced.messages": {
        "suppressCommitHasNoPreviousCommitWarning": false,
        "suppressCommitNotFoundWarning": true,
        "suppressFileNotUnderSourceControlWarning": false,
        "suppressGitVersionWarning": false,
        "suppressLineUncommittedWarning": false,
        "suppressNoRepositoryWarning": false,
        "suppressUpdateNotice": true,
        "suppressWelcomeNotice": true
    },
    "debugwrapper.wrappers": {
        "javascript": "console.log('$eSEL', $SEL);",
        "typescript": "console.log('$eSEL', $SEL);",
        "php": "echo '<pre>$eSEL<br />'; var_dump($SEL); echo '</pre>';",
        "default": "print($SEL);"
    }
}
```

## 键盘快捷方式

设置项在：首选项 -> 键盘快捷方式

```json
// 将键绑定放入此文件中以覆盖默认值
[
    {
        "key": "cmd+k q",
        "command": "extension.debugWrapAfter",
        "when": "editorTextFocus"
    }
]
```

## 插件

| 包名 | 功能 | 备注 |
| :--- | :--- | :--- |
| [Auto Close Tag 👍](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-close-tag) | 自动闭合标签 | 写 HTML 和 JSX 的时候特别爽 |
| [Beautify css/sass/scss/less 👍](https://marketplace.visualstudio.com/items?itemName=michelemelluso.code-beautifier) |  |  |
| [Auto Rename Tag 👍](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag) | 开闭标签同时改 |  |
| [Bracket Pair Colorizer 👍👍👍](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer) | 自动把配对的括号（({）改成一样的颜色 | 老人视力拯救神器 |
| [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) |  |  |
| [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) |  |  |
| [Git Lens 👍👍👍](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) | Git 可视化版，超爽 |  |
| [IntelliSense for CSS class names](https://marketplace.visualstudio.com/items?itemName=Zignd.html-css-class-completion) | CSS className 的全局联想 |  |
| [Live Server 👍👍](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) | Hot Reload Web Server，爽 |  |
| [Log Wrapper 👍](https://marketplace.visualstudio.com/items?itemName=chrisvltn.log-wrapper-for-vscode) | 老年人 console.log 语法糖 |  |
| [Material Theme 👍](https://marketplace.visualstudio.com/items?itemName=Equinusocio.vsc-material-theme) | 主题 |  |
| [Node.js Modules Intellisense](https://marketplace.visualstudio.com/items?itemName=leizongmin.node-module-intellisense) | Node 模块路径提示 |  |
| [Prettier - Code formatter 👍👍👍](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) | 超爽，可以调用 ESLint 的 autofix |  |
| [Quick and Simple Text Selection 👍👍](https://marketplace.visualstudio.com/items?itemName=dbankier.vscode-quick-select) | 选单词等等，效率神器 |  |
| [Spell Right](https://marketplace.visualstudio.com/items?itemName=ban.spellright) | 采用系统原生的翻译引擎的语法检测，支持 「26 国」语言 |  |


## 字体

[https://github.com/tonsky/FiraCode](https://github.com/tonsky/FiraCode) 装一下就好




