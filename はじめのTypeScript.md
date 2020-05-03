# 環境構築
## 環境
* MacOS
## nodejs
* [nodebrew](https://github.com/hokaccha/nodebrew)
* [nodemon](https://github.com/remy/nodemon)
## github
* https://github.com/takiguchi-yu/type-script-for-javascript-developers
## package.json
```s
$ npm init -y
```
## TypeScript
* [TypeScript](https://github.com/microsoft/TypeScript)
```s
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

```
