---
title: "docker 搭建SonarQube 并检测项目"
date: 2020-05-07T10:42:56+08:00
author:
  name: "阿金"
comments: true
description: "SonarQube"
keywords: ["SonarQube"]
images:
tags:
  - SonarQube
---
### docker 搭建SonarQube

#### 拉取Sonar镜像
```
docker pull sonarqube:8.3.1-community
```
#### 运行实例
```
docker run --name sonarqube -p 9000:9000 -d sonarqube:8.3.1-community
```

接着访问：http://localhost:9000/ 就可以了，默认管理员用户和密码为：admin/admin


一般可以启动一个数据库如Oracle、MySQL或PostgreSQL。相关系统信息可以在Administration-System查看，我们不指定的话，默认是使用内嵌的H2数据库。如果要指定其它数据库，启动Docker时需要指定。

使用H2数据库有会一些问题：

- 内嵌数据库只能用于测试场景
- 内嵌数据库无法扩展
- 无法升级到新版本的SonarQube，并且不能支持将你的数据迁移至其他数据库引擎

所以建议实际使用时，不要使用内嵌的H2数据库，连接postgres 或 mysql
```
docker pull mysql:5.7.31
```
```
docker run --name mysql-sonar -e MYSQL_ROOT_PASSWORD=mysql -e MYSQL_DATABASE=sonar -e MYSQL_USER=sonar -e MYSQL_PASSWORD=sonar -v /path/to/local/mysql/dir:/var/lib/mysql -p 33066:3306 -d mysql:5.7.31

docker run -d -p 3306:3306 --name mysql-sonarqube -e MYSQL_ROOT_PASSWORD=123456 -e MYSQL_DATABASE=sonar -e MYSQL_USER=admin -e MYSQL_PASSWORD=sonar -v /opt/sonarqube/mysql:/private/var/mysql mysql:5.7.31
```

```
docker run -d --name sonarqube \
    -p 9000:9000 \
    -e SONAR_JDBC_URL=jdbc:postgresql://localhost/sonarqube \
    -e SONAR_JDBC_USERNAME=sonar \
    -e SONAR_JDBC_PASSWORD=sonar \
    -v sonarqube_data:/opt/sonarqube/data \
    -v sonarqube_extensions:/opt/sonarqube/extensions \
    -v sonarqube_logs:/opt/sonarqube/logs \
    sonarqube:latest
```
docker run --rm \
    -p 9000:9000 \
    -v sonarqube_conf:/opt/sonarqube/conf \
    -v sonarqube_extensions:/opt/sonarqube/extensions \
    -v sonarqube_logs:/opt/sonarqube/logs \
    -v sonarqube_data:/opt/sonarqube/data \
    --name sonarqube sonarqube:7.9


$ docker run -d --name sonarqube \
    -p 9000:9000 \
    -e sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube \
    -e sonar.jdbc.username=sonar \
    -e sonar.jdbc.password=sonar \
    -v sonarqube_conf:/opt/sonarqube/conf \
    -v sonarqube_extensions:/opt/sonarqube/extensions \
    -v sonarqube_logs:/opt/sonarqube/logs \
    -v sonarqube_data:/opt/sonarqube/data \
    sonarqube:7.9-community

官网特别详细
https://docs.sonarqube.org/latest/setup/install-server/


#### 安装插件

根据测试项目的语言来下载相应的插件

### 检测项目

如果项目是在Android Studio 或者IntelJ 的 开发工具中，一般都是有相应的SonarQube 插件，下载相应插件，运行docker SonarQube，并且把插件和项目连接起来就直接可以来检测了。