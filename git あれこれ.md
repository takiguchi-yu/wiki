## ローカルリポジトリをリモートリポジトリに push できないとき
以下のようなエラーが発生したときの対処法
```
error: failed to push some refs to 'https://github.com/xxxx/xxxxx.git'
```
コマンド:
```bash
git merge --allow-unrelated-histories origin/master
```
