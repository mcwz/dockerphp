## DockerPHP

这是一个 docker 化 PHP 的项目，目标是从简单起一步步改成可以作为开发以及生成环境的项目。

## install guide

1. git clone this
2. install docker,docker compose
3. 运行 docker
4. 进入 dockerphp ，新建 workspace/app 这个目录可以作为默认的根目录，需要有多个站点需求，可以去 nginx/sites 下修改 conf 配置文件
5. 修改 . env , 确保 RUN_USER_UID and RUN_USER_GID 这两个值和 workspace 归属的用户和用户组的ID一致
6. 运行 docker-compose up -d nginx
