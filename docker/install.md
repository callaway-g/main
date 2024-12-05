# docker install 写経用

## kali linux

### dockerインストール

``` shell
    sudo apt update
    sudo apt install -y docker.io
```

### docker を有効化

``` shell
    sudo syst化mctl enable docker --now
```

### ユーザーをグループに追加

```shell
    sudo usermod -aG docker $USER
```

### docker-ceインストール

```shell
    echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian bookworm stable" | sudo tee /etc/apt/sources.list.d/docker.list

    curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

    sudo apt update
    sudo apt install -y docker-ce docker-ce-cli containerd.io`
```
