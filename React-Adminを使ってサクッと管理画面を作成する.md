# React Admin とは
```
ReactとMaterial Designを用いて、REST/GraphQL APIの上で、ブラウザ上で動作するデータドリブンなアプリケーションを構築するためのフロントエンドフレームワークです。
```
引用元： https://marmelab.com/react-admin/Readme.html

# Getting Started

こちらの[チュートリアル](https://marmelab.com/react-admin/Tutorial.html)に沿って構築します。

```bash
yarn create react-app test-admin --template typescript
cd test-admin
yarn add react-admin ra-data-json-server prop-types
yarn start
```

# APIエンドポイントとリソースのマッピング

```js:src/App.tsx
// in src/App.tsx
import * as React from "react";
import {Admin, Resource, ListGuesser} from "react-admin";
import jsonServerProvider from "ra-data-json-server";

const dataProvider = jsonServerProvider("https://jsonplaceholder.typicode.com");
const App = () => (
  <Admin dataProvider={dataProvider}>
    <Resource name="users" list={ListGuesser} />
  </Admin>
);

export default App;
```


# Node.jsの設定

```bash
# 現在のバージョンを確認
$ nodebrew ls
v15.14.0

current: v15.14.0

# インストール可能なバージョンを確認
$ nodebrew ls-remote
:
v16.0.0   v16.1.0   v16.2.0   v16.3.0   v16.4.0   v16.4.1   v16.4.2   v16.5.0
v16.6.0   v16.6.1   v16.6.2   v16.7.0   v16.8.0   v16.9.0   v16.9.1   v16.10.0
:

# インストール
$ nodebrew install-binary v16.10.0

# 有効化
$ nodebrew use v16.10.0
use v16.10.0
$ node -v
v16.10.0
```
