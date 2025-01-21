# elixir 节点一键部署

- 油管频道：https://www.youtube.com/@alchemyfinance/
- 法师社群：https://t.me/ytalchemy/

## 配置要求
- 内存 8G
- 带宽 100M
- 硬盘 100G

## VPS 试用
- 使用 DigitalOcean，新用户可获得 **60 天 $200** 的试用额度

[![DigitalOcean Referral Badge](https://web-platforms.sfo2.cdn.digitaloceanspaces.com/WWW/Badge%201.svg)](https://www.digitalocean.com/?refcode=9de664fa6fad&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge)

## 一键部署代码

```bash
curl -O elixir.sh https://raw.githubusercontent.com/alchemyfinance/Elixir/refs/heads/main/elixir.sh && chmod +x elixir.sh && ./elixir.sh
```

## 手动部署
### 安装 docker 并拉取 docker 镜像
- 使用指令`apt install docker.io`安装 docker
- 测试节点：安装之后使用指令`docker pull elixirprotocol/validator:testnet`获取 docker 镜像
- 主网节点：安装之后使用指令`docker pull elixirprotocol/validator`获取 docker 镜像
### 创建 .env 配置文件
- 使用指令`nano validator.env`创建并输入以下内容
```bash
# 有效环境是“prod”和“testnet”
ENV=testnet

# 允许的字符 A-Z、a-z、0-9、_、-和空格
STRATEGY_EXECUTOR_DISPLAY_NAME=<自定义名字>

# 该验证者接收 ELX 奖励的以太坊地址
STRATEGY_EXECUTOR_BENEFICIARY=<以太坊钱包地址>

# 仅用于此验证器的私钥。注意：不以“0x”开头
SIGNER_PRIVATE_KEY=<对应的私钥>
```
### 运行
```bash
# x86 架构
docker run -d \
  --env-file /root/validator.env \
  --name elixir \
  --restart unless-stopped \
  -p 17690:17690 \
  elixirprotocol/validator

# mac/amd 架构
docker run -d \
  --env-file /root/validator.env \
  --name elixir \
  --restart unless-stopped \
  --platform linux/amd64 \
  -p 17690:17690 \
  elixirprotocol/validator

# testnet
docker run -d \
  --env-file /path/to/validator.env \
  --name elixir \
  --restart unless-stopped \
  -p 17690:17690 \
  elixirprotocol/validator:testnet
```



## docker 指令

```bash
# 显示停止的容器 container
docker ps -a
# 显示当前运行的程序
docker ps
# 显示程序日志（直接使用容易输出过多内容，最好加tail限制）
docker logs <CONTAINER ID>
# 显示程序最近10条日志，可以调整数字
docker logs --tail=10 <CONTAINER ID>
# 实时查看日志
docker logs -f <CONTAINER ID>
# 进入docker配置文件夹
docker exec -it <CONTAINER ID> /bin/bash
# 查看下载的镜像
docker image ls
# 删除镜像
docker rmi <id>
```
