# ZAP

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
