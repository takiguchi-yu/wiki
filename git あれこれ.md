## よく使うコマンドのエイリアス設定
```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
git config --global alias.df diff
git config --global alias.gr grep
```

## 開発の流れ
```bash
# ローカルブランチを作成
git checkout -b <任意のブランチ名>

# 変更内容を確認
git status

# 更新内容をステージングに登録
git add .

# 差分確認
git diff --cached -w 

# ローカルブランチにコミット
git commit -m"<ワンラインコメント>"

# コミットログを確認
git log
git reflog

# git log をキレイに見るためのあれこれ
git log --graph --oneline --decorate --all
git log --pretty=format:"%h %ad %s" --date=short --all

# 複数あるコミットログをまとめる
git rebase -i HEAD~<遡ってまとめるログを数で指定>
# 例）過去3つ分のコミットログをまとめる
# git rebase -i HEAD~3
# pick
# pick --> f
# pick --> f

# リモートブランチを更新
git push -u origin HEAD
```

## 現在のブランチを確認
```bash
git branch -a
```

## ローカルリポジトリをリモートリポジトリに push できないとき
以下のようなエラーが発生したときの対処法
```
error: failed to push some refs to 'https://github.com/xxxx/xxxxx.git'
```
コマンド:
```bash
git merge --allow-unrelated-histories origin/master
```

## 日本語の文字化けを解消する
```
$ git status
On branch master
 
Initial commit
 
Untracked files:
  (use "git add <file>..." to include in what will be committed)
 
  "\343\202\212\343\203\274\343\201\251\343\201\277\343\203\274.md"
 
nothing added to commit but untracked files present (use "git add" to track)
```
```bash
# 自分だけに適用
git config --local core.quotepath false

# 全体に適用
git config --global core.quotepath false
```

## 既存のgitリポジトリにローカルをpushする
```bash
git remote add origin <git url>
git push -u origin master
```
## git reflog 詳細
https://gist.github.com/kymmt90/9c997726b638b316f9be07aa4e3eea5e

## ローカルの変更を破棄する
```bash
# ファイル名指定
git checkout <filename>

# 特定のファイルではなく、全てをもとに戻す
git checkout .
```

## リモートブランチをローカルにチェックアウト
```bash
# 現在のブランチを確認
$ git branch -a
  develop
* feature/hoge
  master
  remotes/origin/HEAD -> origin/master
  remotes/origin/develop
  remotes/origin/master

# 名前を付けてブランチをチェックアウト
$ git checkout -b feature/fuga origin/develop
```

## リモートリポジトリを追加
```bash
git remote add origin git@github.com:ユーザー名/リポジトリ名.git
```

## リモートリポジトリの変更
```bash
git remote set-url origin git@github.com:ユーザー名/リポジトリ名.git
```