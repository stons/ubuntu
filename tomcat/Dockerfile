# ubuntu + tomcat
FROM sxzt/jdk8:latest
MAINTAINER sxzt "sjzt2513@163.com"

ENV TOMCAT_NAME apache-tomcat-8.5.34
ENV TOMCAT_TAR_NAME $TOMCAT_NAME.tar.gz
ENV TOMCAT_DOWNLOAD_URL http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.5.34/bin/$TOMCAT_TAR_NAME
COPY ./tomcat /etc/rc.d/init.d/tomcat
RUN  mkdir /web
WORKDIR /etc/rc.d/init.d
RUN  chmod 777 tomcat && \
     update-rc.d tomcat defaults

WORKDIR /usr/local/


RUN apt -y update && \
	apt -y upgrade && \
	apt -y install wget && \
	apt -y clean && \
    apt -y autoclean && \
    apt -y autoremove 

RUN  wget $TOMCAT_DOWNLOAD_URL && \
     tar -zxvf $TOMCAT_TAR_NAME && \
     mv $TOMCAT_NAME tomcat && \
     rm $TOMCAT_TAR_NAME && \
     rm -rf /usr/local/tomcat/webapps/*

ENV JAVA_OPTS JAVA_OPTS='-Dfile.encoding=utf-8 -Djava.awt.headless=true -Xms8000m -Xmx12000m -XX:PermSize=256M -XX:MaxPermSize=512m';

RUN echo $JAVA_OPTS >> /usr/local/tomcat/bin/catalina.sh





EXPOSE 8080

# docker run -dti -p 8080:8080 --name xxx -v /home/dev/xxx:/web -v /home/dev/xxx/tomcat/conf/:/usr/local/tomcat/conf/ -v /home/dev/xxx/tomcat/bin/catalina.sh:/usr/local/tomcat/bin/catalina.sh sxzt/tomcat