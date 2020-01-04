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