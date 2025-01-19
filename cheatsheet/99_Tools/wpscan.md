# wpscan

wordpress用脆弱性スキャンツール

* スキャン

``` shell
    wpscan --url http://<url>
    #or
    wpscan --url <IP address>
```

* ユーザ名の列挙

``` shell
    wpscan --url <target IP or hostname> -e u vp
```

* パスワードクラック

``` shell
    wpscan --url <target IP or hostname> -e u --password <password_list.txt>
```
