## create-react-app で React アプリケーションの雛形を作成

### 準備
```bash
# create-react-app をインストール
npm install -g create-react-app

# バージョン指定する場合
npm install -g create-react-app@3.0.0

# アプリケーション作成
create-react-app <アプリケーション名>

# アプリケーションの起動を確認
yarn start
```

### Visual Stadio Code で Emmet を有効化
1. コマンド + , で設定画面を開く  
1. Emmet で検索し、「Edit in setting.json」のリンクをクリック  
1. 以下を追加する  
```json
"emmet.syntaxProfiles": {
  "javascript": "jsx"
},
"emmet.triggerExpansionOnTab": true
```
もしくは、VSCodeの言語選択を「Javasript」から「JavascriptReact」に変更することでも有効になる  


### github
https://github.com/takiguchi-yu/react-hooks-101/tree/master

### Redux
複数の状態を管理するために `redux combineReducers(reducers)` を使用する  
https://redux.js.org/api/combinereducers/
```bash
# 最新バージョンを確認
npm info redux

redux@4.0.5 | MIT | deps: 2 | versions: 66
Predictable state container for JavaScript apps
http://redux.js.org

# redux インストール
yarn add redux@4.0.5
```

### React Hooks
ドキュメント：https://ja.reactjs.org/docs/hooks-reference.html
```javascript
import React, { useState, useEffect, useContext, useReducer } from 'react';
```
#### useState
状態変化を司る。  
第一引数でstateの値、第二引数でstateを更新するためのset関数が返却される。
```javascript
(例)
const [title, setTitle] = useState('')
```
#### useEffect
状態変化する度に呼ばれる。  
いままでの componentDidMount や componentDidUpdate みたいなやつ。  
第一引数でstateの値、第二引数でstateを更新するためのset関数が返却される。
```javascript
(例)
// 例では、state の変化を監視
useEffect(() => {
  console.log('I am useEffect.')
}, [state])
```
### useReducer
Reducer を使うための関数。  
```javascript
import reducer from '../reducers'
const App = () => {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <AppContext.Provider value={{ state, dispatch }}>
      <div className="container-fluid">
        <EventForm />
      </div>
    </AppContext.Provider>
  )
};
export default App;

```

#### useContext
prop drilling 問題のための関数。  
別コンポーネントに値の引き継ぎの行う。
```javascript
(例)
// AppContext.js
import { createContext } from 'react';
const AppContext = createContext();
export default AppContext;

// App.js
import AppContext from '../contexts/AppContext'
import reducer from '../reducers'
import EventForm from './EventForm'
const App = () => {
  const initialState = appState ? JSON.parse(appState) : {
    events: [],
    operationLogs: [],
  }
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <AppContext.Provider value={{ state, dispatch }}>
      <div><EventForm /></div>
    </AppContext.Provider>
  )
};
export default App;

// EventForm.js
import React, { useContext, useState } from 'react'
const EventForm = () => {
  const { state, dispatch } = useContext(AppContext)
  return (
    <button className="btn btn-danger" onClick={deleteAllEvents} disabled={state.events.length === 0}>イベントボタン</button>
  )
}
export default EventForm
```

## eslintを使う
package.json にスクリプトを登録する
```git
   "scripts": {
+    "lint": "eslint src/ --ext .js",
     "start": "react-scripts start",
```
これで以下のコマンドで実行可能になる
```bash
npm run lint 

# 自動修正する場合
npm run lint -- --fix
```
ルールを初期化する
```bash
npx eslint --init

# 以下は選択肢
? How would you like to use ESLint? To check syntax, find problems, and enforce code style
? What type of modules does your project use? JavaScript modules (import/export)
? Which framework does your project use? React
? Does your project use TypeScript? No
? Where does your code run? Browser
? How would you like to define a style for your project? Use a popular style guide
? Which style guide do you want to follow? Airbnb: https://github.com/airbnb/javascript
? What format do you want your config file to be in? JavaScript
```

.eslintrc.js
```javascript
module.exports = {
  env: {
    browser: true,
    es6: true,
  },
  extends: [
    'plugin:react/recommended',
    'airbnb',
  ],
  globals: {
    Atomics: 'readonly',
    SharedArrayBuffer: 'readonly',
  },
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 2018,
    sourceType: 'module',
  },
  plugins: [
    'react',
  ],
  rules: {
    // 拡張子が.jsの場合でも.jsxとして扱われるようにする
    "react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx"] }],
    // ブラケットを省略しなくてもエラーにしない
    "arrow-body-style": ["error", "always"],
  },
};

```