## React とは
Facebook が開発した Javascript で画面開発できるライブラリ  
Slack, Qiita, NETFLIX, Airbnb など多くのWebサービスで採用されている言語  
仮想DOM といって DOM の変更箇所のみをレンダリングする機構を持っているため高速な処理が可能  
公式：https://ja.reactjs.org/

## JSX 
JSX は HTML ライクに記述した文法を Javascript に変換することができる仕組みで、これをトランスファイルという  
直感的にHTMLを表現できる、記述できるのがJSXの利点  
トランスファイルは babel がやっている  

変換の様子は、以下のサイトが確認ができる  
https://babeljs.io/repl  
例)
* Javascript記法
```javascript
class App extends Component {
  render() {
    React.createElement(
      "div",
      null,
      "Hello, World"
    );
  }
}
```
* JSX記法
```javascript
class App extends Component {
  render() {
    return <div>Hello, World</div>
  }
}
```
JSX の方が最終的な成果物（HTML）に近く、分かりやすい

## Webpack
モジュールバンドラーとも呼ばれる  
複数ファイルを bundle.js としてひとつのファイルにまとめくれる  
HTML でいちいち複数のscriptタグで読み込まなくて済む  
公式: https://webpack.js.org/

## props
データの属性のこと  
例えば、props.nameやprops.ageなど props には数値や関数や文字列などなんでも入る  
波括弧で囲って定義してあげる  
```javascript
import Readct from 'react'

const App = () => {
  return (
    <div>
      <User name={"Taro"}/> ★nameという属性を与える
    </div>
  )
}
const User = (prpos) => {
  return <div>Hi, Iam {props.name}</div>  ★propsに入っているnameを参照
}
export default App
```

## prop-types
型チェックするためのパッケージ  

## state
react の component は内部で状態を持つことができる  
これを state という  
component の内部でのみ持つことができる  
props はイミュータブル（変更不可）であったが、state はミュータブル（変更可能）である  

## redux
Reduxは、ReactJSが扱うUIのstate(状態)を管理をするためのフレームワークです。Reactではstateの管理するデータフローにFluxを提案していますが、ReduxはFluxの概念を拡張してより扱いやすく設計されています。  
Reduxはstateを管理するためのライブラリーなので、React以外にもAngularJSやjQueryなどと併せて使用することもできますが、Reactと使用するのが一番相性がいいです。

<img width="619" alt="スクリーンショット 2019-12-08 15 59 13" src="https://user-images.githubusercontent.com/8340629/70385779-c0b36e80-19d3-11ea-81aa-b5dec94d6494.png">


### redux の action
アプリケーションの中で何が起きたかを表すデータのこと  
Javascript のオブジェクトのこと  
オブジェクトの内部で type というキーとtype に対応する値を持つのが特徴  
type の値はユニークなものでないといけない  
action　が定義されたコードを action creator という  
例）
```javascript
const READ_EVENT = 'READ_EVENT'
export const readEvnet = () => ({
  type: READ_EVNET  // ※ type というキーとそれに対応する値
})
```

### redux の reducer
state(状態)をどのように変化させるかを定義するのがreducer  
例）
```javascript
// 全reducer をひとつに結合させるためにcombineReducersを定義
import {combineReducers} from 'redux'

// sample reducers
import foo from './foo'
import bar from './bar'
export default combineReducers({foo, bar})
```
```javascript
import {READ_EVENT} from '../actions'

const initialState = {value: 0}

export default (state = initialState, action) => {
  switch (action.type) {
    case READ_EVENT:
      return {state.value + 1}
    default:
      return state
  }
}
```

### redux の store
reducer をもとに storeを作成する  
store はstate(状態)を保持し、全てのアプリケーションで使用できるようにする役割を持つ  
provider を使用することでstateの受け渡しを簡単にしている  
例）
```javascript
// storeをインポート
import {createStore} from 'redux'
// Provicerをインポート
import {Provider} from 'react-redux'
// reducerをインポート
import reducer from './reducers'
// アプリケーションをインポート
import App from './components/App'
const = store = createStore(reducer)
ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>
  document.getElementById('root')
)
```

## Yarn のインストール
パッケージ管理ツールである yarn をインストールする。
```bash
npm install --global yarn
yarn --version
```

## react アプリケーションの作成
https://create-react-app.dev/docs/getting-started
```bash
# 現在のディレクトリに作成
npx create-react-app ../<現在のディレクトリ名>
```

## react アプリケーションを起動
```bash
yarn run start
or 
yarn start
```

## redux をインストール
```bash
yarn add redux react-redux 
```

## 便利なライブラリをインストール
```bash
# HTTP リクエストするためのライブラリ
yarn add axios

# 非同期処理をするためのライブラリ
yarn add redux-thunk

# ルーティングライブラリ
yarn add react-router-dom

# フォーム関連のライブラリ
yarn add redux-form

# Chrome の拡張機能から Redux の状態管理を可視化するライブラリ
yarn add redux-devtools-extension

# material-ui をインストール
yarn add material-ui
```
