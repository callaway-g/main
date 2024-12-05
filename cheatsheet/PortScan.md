# PortScan

1. ping sweet サンプル

    ``` shell
        for i in {1..254}; do ping xxx.yyy.zzz.$i -c 1 -W 1 | grep ttl | cut -d ' ' -f 4 | tr -d ':' >> ip_list.txt & done
        #または
        for i in {1..254};do (ping -c 1 XXX.XXX.XX.$i | grep "bytes from" &) ;done
    ```

2. 解放ポートや使用しているサービスの取得

    ``` shell
        ss -antu 
    ```

3. pingのレスポンスの違い

    | response | 状態                         |
    | :------: | ---------------------------- |
    | SYN,ACK  | IPが存在してPortが開いている |
    | RST,ACK  | IPが存在してPortが閉じている |
    |   None   | パケットがdropされている     |
    |          | IPが存在しない               |
    |          | タイムアウト |

4. バナーの取得
`printf "HEAD /index.html HTTP/1.0\r\n\r\n" | nc XXX.YYY.ZZZ.AAA`

5. バージョン情報の収集

    ``` shell
        nmap XXX.YYY.ZZZ.AAA -p 80 -sV | grep open
    ```

6. ncでポートスキャン
    * シングルバイナリで実行できるので転送先で実行しやすい

    ```shell
        # tcp
        nc -zv XXX.XXX.XXX.XXX
        # udp
        nc -uzv XXX.XXX.XXX.XXX
    ```

7. nc,nmapがないときの即席スキャン

    ``` shell
        nmap2 () {
        [[ $# -ne 1 ]] && echo "Please provide server name" && return 1
        
        for i in {1..9000} ; do
        SERVER="$1"
        PORT=$i
        (echo  > /dev/tcp/$SERVER/$PORT) >& /dev/null &&
            echo "Port $PORT seems to be open"
        done
        }

        nmap2 XXX.XXX.XXX.XXX
        #解放ポートが返ってくる
    ```
