# Docker コマンド

* イメージ関連
    1. DockerFileのビルド
       * 普通

            `docker build -t <image_name>`
       * キャッシュなし

            `docker build -t <image_name> . –no-cache`
    2. イメージ一覧

        `docker images`
    3. イメージの削除

        `docker rmi <image_name>`
    4. 未使用のイメージ削除

        `docker image prune`
* コンテナー関連
    1. 起動
       * よく使う

            `docker run -d --name <container_name> -p <host_port>:<container_port> <image_name>`
       * コンテナ停止時に削除

            `docker --rm <container_name>`
    2. 起動中のコンテナで実行
       * ステータス

            `docker container stats`
    3. コンテナの停止

        `docker stop <container_name> (or <container-id>)`
    4. コンテナの削除

        `docker rm <container_name>`
    5. コンテナの開始

        `docker start <container_name> (or <container-id>)`
    6. コンテナ一覧の表示
       * 起動中のみ

            `docker ps`
       * 全部

            `docker ps -a`
* 全般

    1. help表示

        `docker --help`
    2. 情報表示

        `docker info`
