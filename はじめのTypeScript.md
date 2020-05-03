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
ts-node@8.5.4 | MIT | deps: 5 | versions: 105
$ npm install ts-node@8.5.4 --save-dev

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

# 基本的な型(Type)

## プリミティブ型

- boolean ... 真偽値
- number ... 数値
- string ... 文字列
- number[] or Array<number> ... 配列
- number[][] ... 二次元配列
- [string, number] ...tuple 型という
- any ... 基本的には型が不明になってしまうので使用禁止

以下のような json がある場合

```json
{
  "id": 1,
  "title": "title",
  "description": "description",
},
```

以下のような型定義をすることができる
(Article は任意の型文字列)

```js
interface Article {
  id: number;
  title: string;
  description: string;
}
let data: Article[];
```

- void

```js
function returnNothing(): void {
  console.log('I dont return anything.');
}
console.log(returnNothing());
```

- null, undefined

```js
let absence: null = null;
// absence = 'hello'; // Error!!

let data: undefined = undefined;
// data = 123; // Error!!
```

- never ... 呼び元に戻ってこないよ、の意味の型(return なし)

```js
function error(message: string): never {
  throw new Error(message);
}

try {
  let result = error('test');
  console.log('未到達ロジック' + result);
} catch (error) {
  console.log({ error });
}
```

- object

```js
let profile1: object = { name: 'Ham' };
profile1 = { brithYear: 1976 };

// 上記でもObject型を定義できるが、TypeScriptでは以下のようにできるだけ強い型を付けることが推奨されている

let profile2: {
  name: string,
} = { name: 'Ham' };
// profile2 = { brithYear: 1976 }; // Error!!
```

- Type Aliases

```js
type Mojiretsu = string;
const fooMojiretsu: Mojiretsu = 'Hello';

type Profile = {
  name: string,
  age: number,
};
const example1: Profile = {
  name: 'Ham',
  age: 43,
};

// typeofで既存の型をそのまま定義できる
const example2 = {
  name: 'Ham',
  age: 43,
};
type Profile2 = typeof example2;
```

- interface

```js
interface ObjectInterface {
  name: string;
  age: number;
}

let object: ObjectInterface = {
  name: 'Ham-san',
  // name: true, // Error!!
  age: 43,
};
```

- unknown ... typeof と組み合わせて型推論してから処理を実行する(このことをタイプガードという)

```js
const kansu = (): number => 43;
let numberUnknown: unknown = kansu();
let sumAny = numberAny + 7;
if (typeof numberUnknown === 'number') {
  let sumUnknown = numberUnknown + 7;
}
```

- intersection(交差型) ... 複数を合体

```js
type Pitcher1 = {
  throwingSpeed: number,
};
type Batter1 = {
  battingAverage: number,
};
// ２つのタイプ（型）を合体できる
type TwoWayPlayer = Pitcher1 & Batter1;

const OtaniShohei: TwoWayPlayer = {
  throwingSpeed: 154,
  battingAverage: 0.367,
};
```

- union ... 複数の型を許容するための型

```js
let value: number | string = 1;
value = 'foo';
```

- Literal ... 特定の値のみを許容するための型

```js
let dayOfTheWeek: '日' | '月' | '火' | '水' | '木' | '金' | '土';
dayOfTheWeek = '月';
// dayOfTheWeek = '31'; // Error!!
```

- enum

```js
enum Months {
  January = 1,  // 1始まりからを定義できる
  February,     // 2
  March,        // 3
  April,        // 4
}
console.log(Months.April);

enum COLORS {
  RED = '#ff0000',
  WHITE = '#ffffff',
  GREEN = '#008000',
}
console.log(COLORS.GREEN);
```

# 【Tips】ライブラリ

- [axios](https://github.com/axios/axios) ... 外部 API と通信するためのライブラリ

```bash
$ npm info axios
axios@0.19.2 | MIT | deps: 1 | versions: 42

$ npm install axios@0.19.2
```
