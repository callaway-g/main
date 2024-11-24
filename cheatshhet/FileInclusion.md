# File Inclusion

* File Inclusion(Remote)

1. クエリストリングにファイル名があるかを確認
2. phpinfo()を実行させるphpファイルを作成
3. ローカルでhttpサーバを立てる`python -m http.server 1030`
4. 攻撃したいURLの`file=`にローカルのphpファイルのパスを記述

* File Inclusion(Local)
  
1. ファイルアップロード時にファイルパスを確認できるかを検証
