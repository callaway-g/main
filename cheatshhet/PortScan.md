# PortScan

1. ping sweet サンプル

    ``` shell
    for i in {1..254}; do ping xxx.yyy.zzz.$i -c 1 -W 1 | grep ttl | cut -d ' ' -f 4 | tr -d ':' >> ip_list.txt & done
    ```

2. pingのレスポンスの違い

    | response | 状態                         |
    | :------: | ---------------------------- |
    | SYN,ACK  | IPが存在してPortが開いている |
    | RST,ACK  | IPが存在してPortが閉じている |
    |   None   | パケットがdropされている     |
    |          | IPが存在しない               |
    |          | タイムアウト |

3. バナーの取得
`printf "HEAD /index.html HTTP/1.0\r\n\r\n" | nc XXX.YYY.ZZZ.AAA`

4. バージョン情報の収集

```shell
    nmap XXX.YYY.ZZZ.AAA -p 80 -sV | grep open
```
