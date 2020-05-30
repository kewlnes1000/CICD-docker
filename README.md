# CICD-docker

### 演示圖片

[![Traefik](https://i.imgur.com/ogJ7QDk.png "Traefik")](https://i.imgur.com/ogJ7QDk.png "Traefik")

[![Drone](https://i.imgur.com/mhnLo1t.png "Drone")](https://i.imgur.com/mhnLo1t.png "Drone")

### Features

- Docker 建立，快速更換環境
- Traefik 取代 Nginx，自動化申請憑證
- DroneCI，支援 Github、GitLab、Gitea、Bitbucket
- 更快、更方便、更容易

### Pre-operation & Tools

- 熟悉 Docker 跟一點點 shell 指令
- used Traefik v2.2
- used Drone v1.0

### Step By Step

#### Git Clone

```shell
git clone https://github.com/kewlnes1000/CICD-docker.git
```

#### Run Traefik

```shell
cd ./CICD-docker/traefik
sudo chmod 600 ./acme.json
sudo docker network create web
sudo docker-compose up -d
```

#### Run Drone

生成密鑰

```shell
openssl rand -hex 16
```

update .env

```shell
cd ../drone
sudo cp -f .env.example .env
sudo nano .env
```

```
DRONE_SERVER_HOST=<你的Drone域名>
DRONE_SERVER_PROTO=https
DRONE_GITHUB_CLIENT_ID=<From Github OAuth Apps>
DRONE_GITHUB_CLIENT_SECRET=<From Github OAuth Apps>

DRONE_RPC_HOST=drone-server
DRONE_RPC_PROTO=http
DRONE_RPC_SECRET=<剛剛生成的密鑰>
```

run docker

```shell
sudo docker-compose up -d
```

#### Congratulations! Open your website

**See Traefik Dashboard :** [http://<your default host or ip>:8080/dashboard/#/](https://ip:8080/dashboard/#/)  
  
**See Drone Dashboard :** [https://<你的Drone域名>](https://drone.demo.com)
