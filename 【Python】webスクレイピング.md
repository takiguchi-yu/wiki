# はじめに
今回は、`Anaconda` を使う。  
`Anaconda` は主に数値やデータ解析，機械学習系のライブラリ，Pythonにおいてよく使われるライブラリをセットしてくれているPythonパッケージである。  
CONTINUUM というデータ解析を生業としている会社が無料で提供している。

Anaconda をインストールすると `IPython`(現在は、`Jupyter`という)が使えるようになる。  
`IPython` はブラウザ上でPythonの開発ができるIDEである。

# Anaconda のインストール
以下のページから`Anaconda`をダウンロードしてインストールする。  
https://www.anaconda.com/distribution/#macos

# IPython 起動
```bash
ipython notebook
```
下図のように「Python 3」を選択するとさっそく始められる。  
<img width="500" alt="Home" src="https://user-images.githubusercontent.com/8340629/70404572-e09f6c80-1a7d-11ea-9fe1-138f5a402086.png">

# `Python`で`Webスクレイピング`
## 必要なパッケージをインストール

```bash
# BeautifulSoup
# Web解析のためのHTMLパーサー
conda install beautifulsoup4

# lxml
conda install lxml

# requests
conda install requests
```

## ソースコードサンプル
```python
from bs4 import BeautifulSoup
import requests
import pandas as pd
from pandas import Series, DataFrame

# サンプルではカリフォルニア大学のレポートテーブルを解析する
url = 'http://www.ucop.edu/operating-budget/budgets-and-reports/legislative-reports/2013-14-legislative-session.html'

# requests を使ってHTMLを取得
result = requests.get(url)
c = result.content
# 取得結果の確認
c

# BeautifulSoup を使ってHTMLを整形
soup = BeautifulSoup(c, 'lxml')
# 取得結果の確認
soup

# find()を使って必要なコンテンツに絞る
summary = soup.find('div', {'class': 'list-land', 'id': 'content'})

# find_all()を使ってtableのみを取得
tables  = summary.find_all('table')

# 取得できたtableの数を取得
len(tables)

# 取得結果の確認
summary
tables

# HTMLの行(tr)を取得
data = []
rows = tables[0].find_all('tr')

# 取得できた行数を確認
len(rows)

# 列(td)を取得してdata変数に格納していく
for tr in rows:
    cols = tr.find_all('td')
    for td in cols: 
        text = td.find(text = True)
        print(text)
        data.append(text)

# 取得結果の確認
data

# pdfの文字列が入っている列を取得
# unicodeの"\xa0"も空白に置換
reports = []
date = []
index = 0

for item in data:
    if 'pdf' in item:
        date.append(data[index-1])
        reports.append(item.replace('\xa0', ' '))
    index += 1

# 取得結果の確認
data
reports

# データフレームに格納していく
# シリーズに変換
date = Series(date)
reports = Series(reports)

# 取得した列を結合
web_df = pd.concat([date, reports], axis=1)

# 取得結果の確認
web_df

# 列にタイトルに付ける
web_df.columns = ['Date', 'Reports']

# 確認
web_df
```