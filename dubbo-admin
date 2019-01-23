## 使用版本：dubbo-admin-2.0.0.war

Dockerfile:
```
FROM 192.168.88.249/library/tomcat:8-alpine
MAINTAINER caozg007
ENV DIR_WEBAPP /usr/local/tomcat/webapps/
ENV JAVA_OPTS -server -Xms500M -Xmx500M -Xss512k -Djava.security.egd=file:/dev/./urandom -Dfile.encoding=UTF8 -Duser.timezone=GMT+08
RUN  rm -rf $DIR_WEBAPP/*
COPY entrypoint.sh  entrypoint.sh
COPY dubbo-admin $DIR_WEBAPP/ROOT
ENTRYPOINT ["/bin/sh","entrypoint.sh"]
HEALTHCHECK --interval=5s --timeout=3s CMD curl --fail -u root:$psw http://127.0.0.1:8080/ || exit 1
```

entrypoint.sh:
```
sed -i "s/127.0.0.1/$ip/g" $DIR_WEBAPP/ROOT/WEB-INF/dubbo.properties
sed -i "s/dubbo.admin.root.password=root/dubbo.admin.root.password=$psw/g" $DIR_WEBAPP/ROOT/WEB-INF/dubbo.properties
catalina.sh run
```

start.sh:
```
docker run -d  --name dubbo-admin  -p 3305:8080  --restart always -v /etc/localtime:/etc/localtime:ro -v /etc/hosts:/etc/hosts:ro -e ip="192.168.88.248" -e psw="3306" -h dubbo-admin  192.168.88.249/library/dubbo-admin:alpine
```

