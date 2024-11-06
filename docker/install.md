# docker install 写経用

## kali linux

1. dockerインストール
    * `sudo apt update`
    * `sudo apt install -y docker.io`
2. docker を有効化
    * `sudo syst化mctl enable docker --now`
3. ユーザーをグループに追加
    * `sudo usermod -aG docker $USER`
4. docker-ceインストール
    * `echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian bookworm stable" | sudo tee /etc/apt/sources.list.d/docker.list`
    * `curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg`
    * `sudo apt update`
    * `sudo apt install -y docker-ce docker-ce-cli containerd.io`
