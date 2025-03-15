# Hashcat

- help

ヘルプとハッシュタイプの一覧を表示できる。

``` shell
    hashcat -h
```

- 攻撃モード

``` shell
    # Wordlist
    hashcat -a 0
    # combinator　２つ以上の辞書を使用
    hashcat -a 1
    # Brute-force (mask attack) マスク指定
    hashcat -a 2
    # Hybrid Wordlist + Mask 辞書とマスク
    hashcat -a 6 
    # Hybird Mask + Wordlist　ワードリストの各単語にマスクを前置
    hashcat -a 7
```

- ハッシュタイプの特定

``` shell
    hashcat --identify hash.txt
```

- クラック

``` shell
    # 一度クラックしたハッシュはpotfileに保存される。
    # 通常は ~/.hashcat　~/.local/share/hashcat またはインストールされている場所

    # ハッシュタイプがわかる場合は手動で選択
    hashcat -m <hash_type_number> -a 0 hash.txt <word_list>
    # -mを省略すると自動でハッシュタイプを推測する
    hashcat -a 0 hash.txt <word_list>

    # クラックされたパスワードの確認
    hashcat -m <hash_type_number> hash.txt <word_list>　--show --user
    # まだクラックされていないパスワードの確認
    hashcat -m <hash_type_number> hash.txt <word_list> --left --user
```

- ルールファイル
  
```shell
    # hashcatのrulesディレクトリにルールの例がある
    # /opt/hashcat/rules
    hashcat -m <hash_type_number> -a 0 hash.txt <word_list> -r <ruleファイル>
```
