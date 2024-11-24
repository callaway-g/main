# ubuntu bash

* パスワード変更

    ```shell
      passwd [USER_NAME]
    ```

* ユーザ情報

  ``` shell
    id
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
