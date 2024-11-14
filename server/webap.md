# WebAP

* ssh
  * root loginを禁止する

    sshd_config の `PermitRootLogin yes`を`no`にする。
* apache
  * ディレクトリリスティングを無効化

     /etc/httpd/conf/httpd.conf の `Options Indexes FollowSymLinks`の`Indexes`を削除

  * バージョン情報を公開しない

    /etc/httpd/conf/httpd.conf に `ServerTokens Prod`を追加

* ftp
  * Anonymousログインを無効化

    /etc/vsftpd/vsftpd.confの`anonymous_enable=YES`を`anonymous_enable=NO`に変更
