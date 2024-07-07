# Git Udemy講座メモ

## 0. Git概念
- ローカルワークツリー / ステージ / リポジトリの三階層でGitは運用されている
- ステージはコミットしたいものだけをローカルから分割するためにある

## 1. 設定変更
#### 初期設定
```
$ git config --global user.name "ユーザー名"
$ git config --global user.email "メールアドレス"

# 確認
$ git config user.name
$ git config user.email
```
#### コマンドにエイリアスを付ける
```
$ git config --global alias.ci commit
$ git config --global alias.st status
$ git config --global alias.br branch
$ git config --global alias.co checkout
```

#### バージョン管理しないファイル
```
- .gitignoreファイルを作成

# 書き方

# ルートディレクトリを指定
/root.html
# ディレクトリ以下を除外
dir/
# /以外の文字列マッチ 「*」
/*/*.css
```

## 2. Gitコマンド一覧
- git init：初期操作

- git add：ステージへの追加
- git commit：リポジトリへコミット
  - -m "コメント"：エディタを開かずにコメントを挿入
  - -v：差分を表示
- git status：現在のステータスを表示
- git diff：オプションなしの場合ローカルとステージとの差分を出力
  - --staged：ステージとコミットとの差分を出力
- git log：履歴を一覧表示
  - --oneline：コミット履歴の確認。一行表示
  - -n 数字：表示数を制限
  - -p：変更内容まで確認
- git rm：削除
  - <ファイル名>：ローカルとリポジトリの対象ファイルを削除
  - -r <ディレクトリ名>：ローカルとリポジトリの対象ディレクトリを削除
  - --cached<ファイル名>：ファイルを残してリポジトリのみ削除
- git mv<旧ファイル> <新ファイル>：ファイルの移動、ファイル名の変更(ステージに記録されるのでコミットが必要)

## 3. GitHubコマンド一覧
#### リモートリポジトリの新規追加
- git remote add <リモート名> <リモートURL>：GitHubを新規追加(URLを登録することにより毎回GitHubにプッシュするときにURLを打ち込む必要がなくなる、originに登録される)
- git push <リモート名> <ブランチ名>：GitHubへ送信
  - Ex：git push origin masterなど
-  git push -u origin master：最初にやっておくと後でgit pushだけでよくなる

#### リモートリポジトリの情報表示
```
$ git remote：リモートリポジトリを表示
$ git remote -v：URLを表示
```

#### リモートリポジトリから取得
```
# fetch編
## リモートブランチというローカルリポジトリに反映させるだけでローカルワークツリーには影響を与えない
$ git fetch <リモート名>
$ git branch -a：作成されたブランチを確認
$ git checkout <ブランチ名>：ブランチの切り替え
# 取り込み先にブランチを切り替えてマージする
$ git merge origin/master

# pull編
## リモートから情報を取得してマージまでを一度にやりたい場合
$ git pull <リモート名> <ブランチ名>
# リモート名、ブランチ名は省略可能
# git fetchとgit mergeコマンドを効果は同じ
```

#### 変更取り消し
```
$ git checkout -- <ファイル名> or <ディレクトリ名>
# 全変更取り消し
$ git checkout -- .
``` 

#### ステージ追加を取り消し
※ステージからの取り消しのみでワークツリーには変更を加えない
```
$ git reset HEAD <ファイル名> or <ディレクトリ名>
# 全取り消し
$ git reset HEAD .
```

#### 直前コミットの修正
※リモートリポジトリにPushしたものはコミットしなおしはダメ！！
```
$ git commit --amend
```