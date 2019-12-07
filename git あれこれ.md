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


