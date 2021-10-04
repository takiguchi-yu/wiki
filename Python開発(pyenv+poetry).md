## pyenvとvirtualenvをインストール 
```bash
# インストール
brew update
brew install pyenv
brew install pyenv-virtualenv
# bashの場合
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(pyenv init --path)"' >> ~/.bash_profile
echo 'if [ -n "$PS1" -a -n "$BASH_VERSION" ]; then source ~/.bashrc; fi' >> ~/.bash_profile
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
```

## pyenv設定
```bash
# pyenvインストール可能一覧
$ pyenv install --list
# pyenvインストール
$ pyenv install 3.8.11 # or $ pyenv uninstall {python-version}
# pyenv確認
$ pyenv versions
* system (set by /Users/xxx/.pyenv/version)
  3.8.11
# pyenv有効化
$ pyenv global 3.8.11 # or $ pyenv local 3.8.11
$ pyenv versions
  system
* 3.8.11 (set by /Users/xxx/.pyenv/version)
```

## virtualenv設定
```bash
mkdir {project-name}
cd {project-name}
pyenv virtualenv 3.8.11 {env-name}
pyenv local {env-name}
pyenv versions
  system
  3.8.11
  3.8.11/envs/{env-name}
* {env-name} (set by /Users/xxx/git/paiza/{env-name}/.python-version)
pyenv install -r requirements.txt
```

# poetry
上記で設定したpyenv-virtualenv+pipをよりももっと快適にパッケージ管理するための仕組みです。

## poetryをインストール
```bash
brew install poetry
```

## poetry設定
```bash
# 新規プロジェクトの場合
poetry new {project-name}
# 既存プロジェクトに追加する場合
poetry init
# 依存関係をインストール
poetry install
# 依存関係をインストール(developmentが不要の場合)
poetry install --no-dev
# 依存関係の追加
poetry add {package-name}
# 依存関係の追加(developmentのみ)
poetry add -D {package-name}
# 依存関係の更新
poetry update 
# 依存関係の更新(dry-run)
poetry update --dry-run
# 仮想環境で実行(入ったら抜ける)
poetry run python {python-file}
# 仮想環境で実行(入ったまま)
poetry shell
poetry {python-file}
# 仮想環境でテストを実行(入ったら抜ける)
poetry run pytest
# 仮想環境でテストを実行(入ったまま)
poetry shell
pytest
```
https://python-poetry.org/
