

## 简介
这是一个基于Springboot2.x，vue2.x的前后端分离的开源博客系统，提供 前端界面+管理界面+后台服务 的整套系统源码。响应式设计，手机、平板、PC，都有良好的视觉效果！

- 你可以拿它作为前端Vue2.x学习的练手教程；
- 你也可以把它作为springboot2.x技术的学习项目；
- 你也可以拿它作为当下火热的ElasticSearch和RabbitMQ的学习Demo;
- 你也可以将其视为一个前后端分离的项目实践；
- 你还可以作为SpringCloud服务化思想的学习理解；
- ...
## 使用技术
- SpringBoot 2.x 后台基本框架
- Vue 2.x 前端基本框架
- ElementUI：后台管理页面UI库
- IView：前端UI库
- ElasticSearch 搜索层
- RabbitMQ 消息队列
- Shiro 鉴权层
- Redis 缓存层
- Swagger 文档
- Mybaits-Plus 好用的mybatis框架
- lombox getter setter插件
- druid 数据库连接池
- jasypt 加密
- 七牛云 图床

## 站点演示
[www.dblearn.cn](www.dblearn.cn)

## 模块分层
### 后端模块
```shell
dbblog
├── dbblog-auth   # 鉴权模块：shiro
│   ├── pom.xml
│   └── src
├── dbblog-core   # 核心模块：配置文件，Entity类，mapper类，工具类，异常过滤等
│   ├── pom.xml
│   └── src
├── dbblog-manage # 后台管理界面Service
│   ├── pom.xml
│   └── src
├── dbblog-portal # 前端界面Service
│   ├── pom.xml
│   └── src
├── dbblog-search # 搜索模块：elasticSearch
│   ├── pom.xml
└── └── src
```
### 后台依赖关系

dbblog-core -> dbblog-auth -> dbblog-manage -> dbblog-portal -> dbblog-search
- 采用多模块的形式，便于后续SpringCloud微服务的改造升级

### 前端模块
#### 后台管理页面
```shell
├── assets
├── components # 公共组件
├── element-ui
├── element-ui-theme # elementUI主题
├── icons   
├── router  # 路由
├── store   # vuex
├── utils   # js工具类
└── views   
    ├── common # 公共模块
    └── modules
        ├── article    # 文章模块
        ├── book       # 阅读模块
        ├── operation  # 运维模块
        └── sys        # 系统模块


```
#### 前台页面
```shell
├── assets
├── common
├── components
│   ├── content # 页面
│   │   ├── ArticleContent.vue      # 文章详情页
│   │   ├── ArticleListContent.vue  # 文章列表页
│   │   ├── BookContent.vue         # 图书详情页
│   │   ├── BookListContent.vue     # 图书列表页
│   │   ├── BookNoteContent.vue     # 笔记详情页
│   │   ├── HomeContent.vue         # 首页
│   │   ├── SearchResult.vue        # 搜索结果页
│   │   └── TimeLineContent.vue     # 归档页
│   ├── footer
│   ├── header
│   ├── index
│   ├── utils
│   └── views # 页面组件库
│       ├── Archive 
│       ├── Article
│       ├── Book
│       ├── BookNote
│       ├── Classify
│       └── TimeLine
├── router # 路由
├── store  # Vuex
└── utils  # js工具类

```
## 项目部署
### 服务端
项目后端环境
- JDK1.8
- Mysql5.7
- Redis
- IDEA编译器
- Lombox插件（百度一下）
- ElasticSearch 6.x
- RabbitMQ
- IDEA编译器

部署步骤：
1. 创建数据库dbblog，并导入dbblog-backend -> db里的所有sql文件
2. 修改dbblog-backend -> dbblog-> dbblog-core里的application-*.yml的数据库连接、redis连接、ElasticSearch连接、RabbitMQ连接
3. 导入项目，并且运行dbblog-backend -> dbblog-search -> BlogApplication里的main方法

### 前端
前端环境：
- Node.js 8.0+
- WebStorm编辑器

部署步骤：
1. 导入项目，运行 npm install（如果失败，清空包后试试cnpm install）
2. 启动项目：npm run dev
3. 前端地址：localhost:8002 管理界面地址：localhost:8888  账号admin，密码123456

## 界面预览

![博文图片1.png](http://oss.dblearn.cn/dbblog/20190310/34c7f3a92bae478c882caaed586042dc.png)

![博文图片2.png](http://oss.dblearn.cn/dbblog/20190310/2403f9585bf64dd2a90b180314a93403.png)

![博文图片3.png](http://oss.dblearn.cn/dbblog/20190310/c1af8818cbac486394eb083463c3c2d7.png)

![博文图片6.png](http://oss.dblearn.cn/dbblog/20190310/558c14cbdee84be99f32c267033df276.png)

![博文图片7.png](http://oss.dblearn.cn/dbblog/20190310/9289e11d4e2b489885246c6023924458.png)

![1.png](http://oss.dblearn.cn/dbblog/20190310/61b8efb183144323b4138b2b9eecdfb7.png)

![2.png](http://oss.dblearn.cn/dbblog/20190310/4e0874dc164e44028e500769f829d7e1.png)

![3.png](http://oss.dblearn.cn/dbblog/20190310/7c641e6681ef468599dbe152bc0ea02a.png)

![4.png](http://oss.dblearn.cn/dbblog/20190310/ee69937e2bd9494f882da788932123ca.png)


## 项目上线
>项目上线需要自己的服务器，可以在网上搜索教程，我用的是阿里云服务器，`docker`部署上线

### `docker`部署上线（后端）
>创建Dockerfile文件内容如下：
```
FROM java:8

VOLUME /tmp

ADD mystory-1.0.0-SNAPSHOT.jar app.jar

RUN bash -c 'touch /app.jar'

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```

介绍一下：

FROM ：表示使用 Jdk8 环境 为基础镜像，如果镜像不是本地的会从 DockerHub 进行下载

MAINTAINER ：指定维护者的信息

VOLUME ：VOLUME 指向了一个/tmp的目录，由于 Spring Boot 使用内置的Tomcat容器，Tomcat 默认使用/tmp作为工作目录。这个命令的效果是：在宿主机的/var/lib/docker目录下创建一个临时文件并把它链接到容器中的/tmp目录

ADD ：拷贝文件并且重命名(前面是上传jar包的名字，后面是重命名)

RUN ：每条run指令在当前基础镜像执行，并且提交新镜像

ENTRYPOINT ：为了缩短 Tomcat 的启动时间，添加java.security.egd的系统属性指向/dev/urandom作为 ENTRYPOINT
>将创建好的Dockerfile文件和jar包上传到服务器

>运行如下命令，注意不要少了最后的“ . ” 运行命令要进入到文件内在执行

`docker build -t dbblog-backend .`
>运行生成成功的镜像

`docker run -d -p 8080:8080 dbblog-backend`

### `docker`部署上线（前端）
>将前端build系统，生成dist

>创建Dockerfile文件内容如下：
```
# 使用Nginx
FROM nginx:1.15
# FROM hub.c.163.com/library/nginx 

# 定义作者
MAINTAINER yaosiyuan <yaosiyuanmail@163.com>

# 将dist文件中的内容复制到 /usr/share/nginx/html/ 这个目录下面
COPY dist/  /usr/share/nginx/html/

## 删除nginx 默认配置
RUN rm /etc/nginx/conf.d/default.conf
## 添加我们自己的配置 default.conf 在下面
ADD default.conf /etc/nginx/conf.d/ 

#COPY nginx.conf /etc/nginx/nginx.conf
RUN echo 'echo init ok!!'
```
ADD 添加的配置文件 要与自己创建的default.conf文件的路径匹配，否则访问页面会报404
>创建 nginx配置文件

在每个项目的文件下新建文件default.conf
```
server {
    listen       80;
    server_name  localhost;

    #charset koi8-r;
    access_log  /var/log/nginx/host.access.log  main;
    error_log  /var/log/nginx/error.log  error;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
        try_files $uri $uri/ /index.html;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
```
>将dist、default.conf和Dockerfile上传到服务器上

>运行如下命令，注意不要少了最后的“ . ” 运行命令要进入到文件内在执行

`docker build -t dbblog-frontend .`
-t 是给镜像命名 ，test是生成镜像的名字，. 是基于当前目录的Dockerfile来构建镜像。
>运行生成成功的镜像

docker run -p 3000:80 -d --name dbblog-frontend 镜像id
>访问

`http://47.240.48.172:3000/`

```前端的后台管理，操作跟前端部署一样```
