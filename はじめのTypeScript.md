# 環境構築

## 環境

- MacOS
- VSCode
  - Prettier(コードフォーマッター)
  - setting.json(VSCode 本体の設定ファイル)
  ```json
  {
    "editor.detectIndentation": false,
    "explorer.confirmDragAndDrop": false,
    "editor.minimap.enabled": false,
    "explorer.confirmDelete": false,
    "editor.tabSize": 2,
    "git.autofetch": true,
    "workbench.iconTheme": "file-icons",
    "emmet.syntaxProfiles": {
      "javascript": "jsx"
    },
    "emmet.triggerExpansionOnTab": true,
    "window.zoomLevel": 0,
    "javascript.updateImportsOnFileMove.enabled": "always",
    "liveServer.settings.donotShowInfoMsg": true,
    "editor.formatOnSave": true,
    "prettier.semi": true,
    "prettier.singleQuote": true
  }
  ```

````

## nodejs

- [nodebrew](https://github.com/hokaccha/nodebrew)

## github

- https://github.com/takiguchi-yu/type-script-for-javascript-developers

## package.json

```bash
$ npm init -y
````

## TypeScript

- [TypeScript](https://github.com/microsoft/TypeScript)

```bash
$ npm info typescript
typescript@3.8.3 | Apache-2.0 | deps: none | versions: 1566

$ npm install typescript@3.8.3 --save-dev

# typescriptはdevにインストールしたためこのままでは使えない
$ tsc src/install-typescript.ts
zsh: command not found: tsc

# パッケージを直指定をして実行
$ ./node_modules/.bin/tsc src/install-typescript.ts
or
$ npx tsc src/install-typescript.ts
# 生成されたjsを実行
$ node src/install-typescript.js
```

初期化

```bash
npx tsc init
```

- [ts-node](https://github.com/TypeStrong/ts-node)  
  ts ファイルを直接実行するためのツール

```bash
$ npm info ts-node
ts-node@8.9.1 | MIT | deps: 5 | versions: 105
$ npm install ts-node@8.9.1 --save-dev

$ npx ts-node src/install-typescript.ts
```

- [ts-node-dev](https://github.com/whitecolor/ts-node-dev)

```bash
$ npm info ts-node-dev
ライブコーディングするためのツール
ts-node-dev@1.0.0-pre.44 | MIT | deps: 12 | versions: 44
$ npm install ts-node-dev@1.0.0-pre.44 --save-dev

# 実行
$ npx ts-node-dev --respawn src/install-typescript.ts
Using ts-node version 8.9.1, typescript version 3.8.3
```

package.json にスクリプトを登録

```diff
   "scripts": {
+    "dev": "ts-node-dev --respawn",
     "test": "echo \"Error: no test specified\" && exit 1"
   },
```

```bash
$ npm run dev src/install-typescript.ts
```
