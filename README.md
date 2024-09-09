![Huginn](https://raw.github.com/huginn/huginn/master/media/huginn-logo.png)
# Huginn ——  您的代理待命中。
-----

## 什么是 Huginn？

Huginn 是一个为你在线执行自动化任务的代理构建系统。它们可以读取网页、监控事件，并代表你采取行动。Huginn 的代理通过创建和消费事件，将它们沿着有向图传播。你可以将其视为一种可以在你自己服务器上修改的 IFTTT 或 Zapier。你始终知道谁掌握了你的数据——是你自己。

![名字的由来](https://raw.githubusercontent.com/huginn/huginn/master/doc/imgs/the-name.png)

#### 使用 Huginn 可以做以下事情：

* 追踪天气并在明天要下雨（或下雪）时收到邮件提醒（"别忘了带伞！"）
* 列出你关心的术语，当这些术语在 Twitter 上的出现频率发生变化时收到邮件通知。（例如，想知道机器学习领域有趣的事情发生了吗？Huginn 会监控“machine learning”在 Twitter 上的讨论，当讨论量激增时告诉你。）
* 监控航空旅行或购物优惠信息
* 关注项目名称在 Twitter 上的提及情况，并获得相关更新
* 抓取网页，当网页发生变化时接收邮件通知
* 连接到 Adioso、HipChat、FTP、IMAP、Jabber、JIRA、MQTT、nextbus、Pushbullet、Pushover、RSS、Bash、Slack、StubHub、翻译 API、Twilio、Twitter 和微博等平台
* 在一天中特定时间发送你关心内容的汇总邮件
* 追踪高频事件的计数，当出现激增时（例如“旧金山紧急情况”），几分钟内发送短信
* 发送和接收 WebHooks
* 运行自定义的 JavaScript 或 CoffeeScript 函数
* 追踪你随时间的地理位置
* 将亚马逊 Mechanical Turk 工作流程作为代理的输入或输出（亚马逊 Turk 代理被称为 "HumanTaskAgent"）。例如：每天请求 5 个人提供搞笑的猫照片；将结果发送给 5 个人进行评分；将评分最高的照片发送给 5 个人添加搞笑的标题；最后将最佳标题的照片发布在我的博客上。

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/huginn/huginn?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) [![Changelog #199](https://img.shields.io/badge/changelog-%23199-lightgrey.svg)](https://changelog.com/podcast/199)

加入我们的 [Gitter 聊天室](https://gitter.im/huginn/huginn) 一起讨论这个项目。

### 加入我们！

想为 Huginn 做出贡献吗？我们鼓励所有形式的贡献！你可以改善 UI、[添加新代理](https://github.com/huginn/huginn/wiki/Creating-a-new-agent)、撰写[文档和教程](https://github.com/huginn/huginn/wiki)，或者尝试解决 [标记为 "help wanted" 的问题](https://github.com/huginn/huginn/issues?direction=desc&labels=help+wanted&page=1&sort=created&state=open)。请 fork、添加测试，并提交 pull request！

真的很想解决某个问题或添加新功能吗？想通过解决社区问题赚点零花钱？请查看 [Bountysource 上的当前悬赏](https://www.bountysource.com/trackers/282580-huginn)。

有一个很棒的想法但还不准备贡献代码？可以前往我们的 [官方“建议代理”讨论帖](https://github.com/huginn/huginn/issues/353) 提出你的建议！

## 示例

请查看 [Huginn 入门视频](http://vimeo.com/61976251)！

接下来是一些示例截图，下面还附有操作指南，帮助你快速入门。

![代理列表示例](https://raw.githubusercontent.com/huginn/huginn/master/doc/imgs/your-agents.png)

![事件流程图](https://raw.githubusercontent.com/huginn/huginn/master/doc/imgs/diagram.png)

![监测 Twitter 上的讨论高峰](https://raw.githubusercontent.com/huginn/huginn/master/doc/imgs/peaks.png)

![记录你的位置信息](https://raw.githubusercontent.com/huginn/huginn/master/doc/imgs/my-locations.png)

![创建新代理](https://raw.githubusercontent.com/huginn/huginn/master/doc/imgs/new-agent.png)

## 部署 Huginn

### 通过 Docker 部署（[官方文档](https://github.com/huginn/huginn/blob/master/doc/docker/install.md)）

#### 运行容器

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

***

### 在 Heroku 上部署

尝试在 Heroku 上使用 Huginn：[![部署](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)（设置需要几分钟时间。在等待过程中，请阅读 [文档](https://github.com/huginn/huginn/blob/master/doc/heroku/install.md)，并确保在启动后点击“查看”！）

Huginn 可以在 Heroku 的免费版本上运行，[但存在显著的限制](https://github.com/huginn/huginn/blob/master/doc/heroku/install.md)。对于非实验性用途，我们强烈建议使用 Heroku 的 1GB 付费计划或我们的 Docker 容器。

### 本地部署 （说明 / [视频教程](http://www.youtube.com/watch?v=xJTwaRl2_Iw)）

1. 克隆仓库

        $ git clone git@github.com:cantino/huginn.git
        $ cd huginn

2. 安装 [Ruby](http://www.ruby-lang.org/en/downloads/) 和 [Ruby Gems](https://rubygems.org/pages/download)（如果尚未安装）
3. 安装 rake 和 bundle（如果尚未安装）：

        $ gem install rake bundle

4. 安装 Huginn 的依赖项

        $ bundle install

5. 安装 [MySQL](http://dev.mysql.com/downloads/)
6. 启动 MySQL 服务器：

        $ mysql.server start

6. 将 *.env.example* 文件复制为 *.env*：

        $ cp .env.example .env

8. 创建 `APP_SECRET_TOKEN`：

        $ rake secret

7. 编辑 *.env* 文件，至少更新我们刚刚创建的 `APP_SECRET_TOKEN` 变量。
8. 使用一些示例数据创建开发环境的 MySQL 数据库：

        $ rake db:create
        $ rake db:migrate
        $ rake db:seed

8. 完成所有步骤后，启动本地服务器：

        $ foreman start  

    打开浏览器，访问 [http://localhost:3000/](http://localhost:3000/)，使用用户名 "admin" 和密码 "password" 登录。
   
### 开发

所有代理都有规格说明！还有模拟在无头浏览器中运行 Huginn 的验收测试。

* 安装 PhantomJS 2.1.1 或更新版本：
  * 使用 [Node Package Manager](https://www.npmjs.com/)：`npm install phantomjs`
  * 在 OSX 上使用 [Homebrew](http://brew.sh/)：`brew install phantomjs`
* 使用 `bundle exec rspec` 运行所有规格测试
* 使用 `bundle exec rspec path/to/specific/test_spec.rb` 运行特定的规格测试
* 更多关于 rspec for rails 的内容请查看 [这里](https://github.com/rspec/rspec-rails)

## 使用 Huginn Agent gems

现在，Huginn 代理可以作为外部 gems 编写，并通过 `ADDITIONAL_GEMS` 环境变量添加到你的 Huginn 安装中。更多信息请参阅 `.env.example` 中的 `Additional Agent gems` 部分。

如果你想编写自己的 Huginn Agent gem，请参阅 [huginn_agent](https://github.com/huginn/huginn_agent)。

我们的总体目标是鼓励复杂和特定用途的代理作为 Gems 编写，同时继续将新的一般用途代理添加到 Huginn 核心库中。

### 可选设置

#### 为私有开发进行设置

请参阅维基中的 [私有开发说明](https://github.com/huginn/huginn/wiki/Private-development-instructions)。

#### 启用 WeatherAgent

为了使用 WeatherAgent，你需要从 [Pirate Weather 获取 Weather Data API 密钥](https://pirate-weather.apiable.io/products/weather-data)。注册一个密钥后，在你的种子 WeatherAgent 中将 `api_key` 的值更改为你的密钥。

#### 禁用 SSL

我们假设你的部署将通过 SSL 运行。这是个非常好的做法！但是，如果你希望禁用 SSL，你可能需要编辑 `config/initializers/devise.rb` 并修改包含 `config.rememberable_options = { :secure => true }` 的那一行。你还需要编辑 `config/environments/production.rb` 并修改 `config.force_ssl` 的值。

## 许可协议

Huginn 是在 MIT 许可下提供的。

Huginn 最早由 [@cantino](https://github.com/cantino) 在 2013 年创建。从那时起，许多人的奉献使它发展到今天的模样。

[![构建状态](https://travis-ci.org/huginn/huginn.svg)](https://travis-ci.org/huginn/huginn) [![覆盖率状态](https://coveralls.io/repos/huginn/huginn/badge.svg)](https://coveralls.io/r/huginn/huginn) [![依赖状态](https://gemnasium.com/huginn/huginn.svg)](https://gemnasium.com/huginn/huginn) [![Bountysource](https://www.bountysource.com/badge/tracker?tracker_id=282580)](https://www.bountysource.com/trackers/282580-huginn?utm_source=282580&utm_medium=shield&utm_campaign=TRACKER_BADGE)
