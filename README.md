## DockerPHP

这是一个 docker 化 PHP 的项目，目标是从简单起一步步改成可以作为开发以及生成环境的项目。

## install guide

1. git clone this
2. install docker,docker compose
3. start docker deamon
4. cd dockerphp 
5. Modify the. Env file , be ensure that the two options, RUN_USER_UID and RUN_USER_GID are consistent with the uid and gid of your working directory.
6. run docker-compose up -d nginx
