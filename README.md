## 快速使用

**下载项目**

```
git clone git@github.com:mfei58/dnmp.git
```

**初始化配置**

```
cd dnmp 
cp env.sample .env
cp docker-compose.sample.yml docker-compose.yml
cp -r services/nginx/conf.d.sample/ services/nginx/conf.d
cp services/nginx/fastcgi_params.sample  services/nginx/fastcgi_params
```

**启动**

```
docker-compose up -d 
```

**Go to [http://localhost](http://localhost)**

