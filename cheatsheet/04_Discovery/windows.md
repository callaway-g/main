# Windows Discovery

*　現在ログインしているユーザ情報やグループ情報・権限関連の情報を取得する。

```bat
whoami /all
```

* コンピュータ上に登録されているローカルのユーザアカウント一覧を表示する。

```bat
net user
wmic USERACCOUNT Get Domain,Name,Sid 
```

* ログオンやパスワード要件を表示

```bat
net accounts
```

* ローカルグループを確認

``` bat
net localgroup
```

* 特定の文字を含むファイル名検索

```bat
dir /s *secret*
```

* WMICを使用する方法

```bat
wmic DATAFILE where "drive='C:' AND Name like '%secret%'" GET Name,readable,size /VALUE
```

* システム情報を列挙

```bat
systeminfo
```

* WMICを使用する方法

```bat
wmic computersystem LIST full
```

* 起動しているプロセスの列挙

```bat
tasklist /SVC
```

* ネットワーク情報　Ping Sweep

```bat
for /l %i in (1,1,255) do @ping -n 1 -w 100 172.31.35.%i | find "TTL="
```

* ネットワーク情報 ARP テーブル

```bat
arp -a
```

* ネットワーク情報　NetBIOS情報

``` bat
# ローカルNetBIOS名の取得
nbtstat -n

# IPからコンピュータ名を取得
nbtstat -A XXX.XXX.XXX.XXX
```

* ネットワーク情報 解放ポート

```bat
netstat -an | find /i "listening"
```

* ネットワーク情報 接続確認

``` ps
Test-NetConnection XXX.XXX.XXX.XXX. -Port YYYY
```

* マウントされているボリューム情報

```bat
mountvol
```

* 共有ドライブ情報を列挙

``` bat
powershell -Command "Get-WmiObject -class Win32_Share"
```
