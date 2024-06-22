# 3B(64bit) にDocker

## Dockerインストール
```sh
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
docker -v
sudo usermod -aG docker ユーザ名
sudo shutdown -r now
```

## docker-composeインストール
※pip3は失敗...
```sh
sudo apt update
sudo apt install docker-compose
docker-compose -v
```
