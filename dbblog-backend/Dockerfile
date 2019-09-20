FROM java:8

MAINTAINER Aini m18790635989@163.com

VOLUME /tmp

ADD dbblog.jar dbblog-search.jar

RUN bash -c 'touch /dbblog-search.jar'

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/dbblog-search.jar"]
