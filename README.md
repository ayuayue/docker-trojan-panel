# trojan panel docker-compose 使用指南


# 安装 docker-compose

curl -L https://github.com/docker/compose/releases/download/1.25.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose

docker-compose --version

# 清理历史镜像

docker rm trojan-panel-caddy
docker rm trojan-panel-ui
docker rm trojan-panel-core
docker rm trojan-panel
docker rm trojan-panel-redis
docker rm trojan-panel-mariadb

# 修改配置

根据 .env 中注释，修改配置
注意证书文件名格式为 域名.crt 和 域名.key,放到 /tpdata/cert 目录

修改：tpdata/caddy/config.json tpdata/trojan-panel-ui/nginx/default.conf 这两个文件，把 ${domain} 替换为你的域名


如果项目已经启动后再修改配置文件或者项目文件，最好执行 docker build 重新构建,然后再运行，否则可能会出现配置不生效的情况

# 启动
首次启动可以使用 docker-compose up 这个是直接运行，看看日志输出有没有错误，没有错误后能不能正常访问并添加节点，如果都没有问题，那么可以 ctrl+c 停止运行，

然后使用 docker-compose up -d 后台运行

# 重启
docker-compose restart

# 问题排查
1. 确保安装了 docker-compose
2. 确保在 tpdata/cert 目录放了证书文件，并证书文件名正确及证书可用
3. 确保 .env 中配置正确，以及 caddy、Nginx 域名 配置正确
4. 确保防火墙放通了端口
5. 确保是在当前目录中执行 docker-compose 命令，不要脱离当前目录执行
6. 可以查看日志 docker-compose logs -f
7. 可以查看日志，在 tpdata/caddy/logs、 tpdata/trojan-panel-ui/nginx/logs 目录下
