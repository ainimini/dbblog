# 使用Nginx
FROM nginx:1.15
# FROM hub.c.163.com/library/nginx

# 定义作者
MAINTAINER Aini	 <m18790635989@163.com>

# 将dist文件中的内容复制到 /usr/share/nginx/html/ 这个目录下面
COPY dist/  /usr/share/nginx/html/

## 删除nginx 默认配置
RUN rm /etc/nginx/conf.d/default.conf
## 添加我们自己的配置 default.conf 在下面
ADD default.conf /etc/nginx/conf.d/

#COPY nginx.conf /etc/nginx/nginx.conf
RUN echo 'echo init ok!!'
