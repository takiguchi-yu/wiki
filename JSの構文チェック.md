eslint-loaderを導入する。  
eslint-loaderはリアルタイムに構文チェックを実施してくれるツール。


### インストール
```bash
npm eslint -D
npm eslint-loader -D

or 

yarn add eslint -D
yarn add eslint-loader -D
```

### 初期化
```bash
npx eslint --init
```
選択肢は可能通り（選択肢はeslintのバージョンによって異なる）  
```
? How would you like to use ESLint? To check syntax, find problems, and enforce code style
? What type of modules does your project use? JavaScript modules (import/export)
? Which framework does your project use? React
? Does your project use TypeScript? No
? Where does your code run? Browser
? How would you like to define a style for your project? Use a popular style guide
? Which style guide do you want to follow? Google: https://github.com/google/eslint-config-google
? What format do you want your config file to be in? JSON
```
