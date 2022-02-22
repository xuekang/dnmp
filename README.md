## 安装Docker
(1) 开启hyper_v（硬件虚拟化技术(Hardware Virtualization Technology)）
* 在<控制面板-程序和功能-启用或关闭Windows功能>中，勾选Hyper-V和Internet Explorer11

(2) [下载安装 the Linux kernel update package](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

(3) [下载安装Docker的windows客户端](https://docs.docker.com/desktop/windows/release-notes/)

(4) [下载安装 Cmder客户端](https://cmder.net/)（使用Docker命令更加友好，非必须）

## 搭建集成环境
(1) 下载项目
```
git clone git@github.com:xuekang/dnmp.git
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
- 可调整docker-compose.yml配置，按需安装所需环境
  
(4) 启动服务
```
docker-compose up -d 
//docker-compose up -d --build  //重新构建,丢弃缓存
```
(5) 查看服务运行状态(State均为Up表示所有服务都正常启动)
```
docker-compose ps 
```
