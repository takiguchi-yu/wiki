## React とは
Facebook が開発した Javascript で画面開発できるライブラリ  
Slack, Qiita, NETFLIX, Airbnb など多くのWebサービスで採用されている言語  
仮想DOM といって DOM の変更箇所のみをレンダリングする機構を持っているため高速な処理が可能

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

## Yarn のインストール
パッケージ管理ツールである yarn をインストールする。
```bash
npm install --global yarn
yarn --version
```

## create-react-app のインストール
今までは babel や webpack をひとつずつインストールしていたが、
この問題を解消するために facebook が便利なテンプレートを開発した
```bash
yarn global add create-react-app
```

## react アプリケーションの作成
```bash
# 現在のディレクトリに作成
create-react-app ./<アプリ名>
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
