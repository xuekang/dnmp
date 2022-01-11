## 安装Docker客户端
(1) [下载安装 Docker客户端](https://docs.docker.com/desktop/windows/release-notes/)

(2) 开启hyper_v（硬件虚拟化技术(Hardware Virtualization Technology)）

(3) 启用或关闭Windows功能勾选Hyper-V和Internet Explorer11

(4) [下载安装 the Linux kernel update package](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)
(5) 安装Docker客户端

(6) [下载安装 Cmder客户端](https://cmder.net/)（使用Docker命令更加友好，非必须）

## 部署Swoole集成环境
(1) 下载项目
```
git clone http://172.16.26.197:15566/common/dnmp.git
```
(2) 初始化配置
```
cd dnmp
cp example.env .env
cp example.docker-compose.yml docker-compose.yml
cp -r services/nginx/example.conf.d/ services/nginx/conf.d
cp services/nginx/example.fastcgi_params  services/nginx/fastcgi_params 
```
(3) 修改配置

- 修改nginx配置：在services/nginx/conf.d中设置域名（server_name）和项目目录(root)
  
(4) 启动服务
```
docker-compose up -d
(docker-compose up -d --build  重新构建,丢弃缓存)
```
(5) 查看服务运行状态(State均为Up表示所有服务都正常启动)
```
docker-compose ps 
```

## 部署项目（以oa3为例，其他项目部署同理）
(1) 下载项目
```
# 进入dnmp\www目录拉取项目
cd www
git clone http://172.16.26.197:15566/houduan/oa3.git 
```
(2) 安装姓名依赖
```
docker exec dnmp-php /bin/sh -c 'cd oa3 && composer install'
```
(3) 修改项目配置(.env)
- swoole配置
```
[SWOOLE]
HOST = 0.0.0.0
RPC_HOST_MODEL = dnmp-php
RPC_HOST_API = dnmp-php
```
- redis配置(连线上可忽略)
```
[REDIS]
HOST = dnmp-redis
```
- mysql配置(连线上可忽略)
```
[DATABASE]
HOSTNAME = dnmp-mysql
```
(4) 启动Swoole服务
```
docker exec -it dnmp-php /bin/sh
cd oa3
php think swoole
```