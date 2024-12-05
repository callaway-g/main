# Docker コマンド

## イメージ関連

### DockerFileのビルド

``` shell
    # 普通 
    docker build -t <image_name>

    # キャッシュなし
    docker build -t <image_name> . –no-cache

    # イメージ一覧
    docker images
```

### イメージの削除

``` shell
    docker rmi <image_name>

    # 未使用イメージの削除
    docker image prune
```

## コンテナー関連

### コンテナー起動

``` shell

    # よく使う
    docker run -d --name <container_name> -p <host_port>:<container_port> <image_name>

    # コンテナ停止時に削除
    docker --rm <container_name>
```

### 起動中のコンテナで実行

``` shell
    # ステータス
    docker container stats
```

### コンテナの停止

``` shell
    docker stop <container_name> (or <container-id>)
```

### コンテナの削除

``` shell
    docker rm <container_name>
```

### コンテナの開始

``` shell
    docker start <container_name> (or <container-id>)
```

### コンテナ一覧の表示

```shell
  # 起動中のみ
    docker ps

   # 全部
    docker ps -a
```
  
## レジストリ関連

### レジストリ起動

```shell
    docker run -d -p 5000:5000 --name [レジストリ名] registry:latest
```

### タグ付け

``` shell
    docker image tag [イメージ名] localhost:5000/[タグ名]
```

### プッシュ

``` shell
    docker push localhost:5000/[タグ名]
```

### プル

``` shell
    docker pull localhost:5000/[タグ名]
```

### レジストリを停止して全データを削除

``` shell
    docker container stop [レジストリ名] && docker container rm -v [レジストリ名]
```

## 全般

``` shell
# help表示
    docker --help
# 情報表示
    docker info
```
