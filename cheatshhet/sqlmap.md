# sqlmap

* sqlmap

1. SQLインジェクションの脆弱性診断ツール
2. コマンド
   1. BurpSuiteでSQL操作時のリクエストを観測 GETリクエストとCookieでセッションIDを保持しているか。
   2. help `sqlmap -h`
   3. コマンド例 `sqlmap -u "http://URL/vulnerbilities/sqli_blind/?id=1&Submit=Submit#" --cookie="PHPSESSID=...; security=low"`
   4. `--dump`でデータベースをダンプ可能
   5. `--data`POSTで実行できる
