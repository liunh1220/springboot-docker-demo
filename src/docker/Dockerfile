#表示使用 Jdk8 环境 为基础镜像，如果镜像不是本地的会从 DockerHub 进行下载
FROM java:8

#指定维护者信息
MAINTAINER liunh

#VOLUME 指向了一个/tmp的目录，由于 Spring Boot 使用内置的Tomcat容器，Tomcat 默认使用/tmp作为工作目录。
#这个命令的效果是：在宿主机的/var/lib/docker目录下创建一个临时文件并把它链接到容器中的/tmp目录
VOLUME /tmp

ARG JAR_FILE=./springboot-docker-demo-1.0.0.jar
COPY ${JAR_FILE} /docker-demo-1.0.0.jar

#拷贝文件并且重命名
#ADD ./target/springboot-docker-demo-1.0.0.jar /docker-demo-1.0.0.jar
#RUN sh -c 'touch /docker-demo-1.0.0.jar'

#COPY ./docker-demo-run.sh /usr/bin/docker-demo-run.sh
#RUN chmod +x /usr/bin/docker-demo-run.sh
#CMD ["docker-demo-run.sh"]

EXPOSE 7001

#为了缩短 Tomcat 的启动时间，添加java.security.egd的系统属性指向/dev/urandom作为 ENTRYPOINT
#ENTRYPOINT ["sh", "-c", "exec java -Djava.security.egd=file:/dev/./urandom -jar /docker-demo-1.0.0.jar"]
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom -Dspring.profiles.active=dev","-jar","/docker-demo-1.0.0.jar"]
#ENTRYPOINT ["./docker-demo-run.sh"]
