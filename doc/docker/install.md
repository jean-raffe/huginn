## 通过 Docker 部署（[官方文档](https://github.com/huginn/huginn/blob/master/doc/docker/install.md)）

1. 按照 [部署说明](https://docs.docker.com/get-docker/) 部署 Docker

2. 配置环境变量 root用户密码、端口， docker 部署 mysql，然后进入容器内以命令行配置以下内容

建立数据库 `{Huginn数据库名}`

新增用户 `{USERNAME}` ，设置密码 `'{PASSWORD}'`

提前为数据库的用户 `{USERNAME}` 授予读写权限

3. 使用以下命令配置环境变量并启动 Huginn 容器（国内环境请使用镜像源替代 `ghcr.io/` ）：

```
sudo docker run --name {需设定的Huginn容器名称} --network deployment -p {需映射到的本机端口}:3000 -e HUGINN_DATABASE_ADAPTER={mysql版本} -e HUGINN_DATABASE_HOST={mysql容器名称} -e HUGINN_DATABASE_PORT={mysql容器映射到的本地端口} -e HUGINN_DATABASE_NAME={Huginn数据库名} -e HUGINN_DATABASE_USERNAME={USERNAME} -e HUGINN_DATABASE_PASSWORD='{PASSWORD}' -e TIMEZONE='Beijing' --restart always ghcr.io/huginn/huginn
```

3. 在浏览器中打开 Huginn：http://{host}:3000

4. 使用默认用户名 `admin` 和密码 `password` 登录，修改用户名与密码后配置 Agent
