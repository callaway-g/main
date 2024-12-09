# Git

## リポジトリ

``` shell
    # ローカルにリポジトリを作成し、リモートにプッシュする
    git init
    git add .
    git commit -, "Initial commit"
    git remote add origin <remote_repogitory>
    git push -u origin master
    # リモートからクローン
    git clone <remote_repogitory_url>
```

## コミット

``` shell
    # コミット
    git commit -m "コメント"
    # commitの履歴
    git log
    # commitの変更点
    git show <commit hash>
    # コミットの取り消し
    git revert <commit hash>
```

## pull/fetch

``` shell
    git pull
    # or
    git fetch
    git merge origin/master
```

## push

``` shell
    # 通常のpush
    git push origin <branch name>
    # 初めてのpush
    git push --set-upstream origin <branch name>
    # or
    git push -u origin <branch name>
    # 取り消し
    git reset --hard <戻したいコミットのhash>
    git push -f
```

## ファイル追加

``` shell
    git add <ファイル名>
    #ディレクトリ以下すべて
    git add .
    # 取り消し
    git reset --hard HEAD^
```

## 差分 remote/local

``` shell
    git diff <file_name>
```

## ブランチ

``` shell
    # 作成(local)
    git branch <branch_name>
    # 切り替え
    git checkout <branch_name>
    # 作成・切り替え
    git checkout -b <branch_name>
    # ブランチ名変更
    git branch -m <old_name> <new_name>
    # 削除
    git branch -d <branch_name>
    # local -> remoteに反映
    git push -u origin <local_branch>
    # remote -> local
    git branch <branch_name> origin/<branch_name>
    # remote -> local & 切り替え
    git checkout -b <branch_name> origin/<branch_name>
    # すべてのブランチを確認
    git branch -a
```
