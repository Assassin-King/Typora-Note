

# 目录

[toc]

## 安装

### Linux wget 安装

```shell
#下载
wget https://github.com/alibaba/nacos/releases/download/1.3.2/nacos-server-1.3.2.tar.gz

#解压完成后，进入nacos文件夹里修改startup.sh中jvm的内存大小
cd nacos/bin

# 设置的是最小堆内存128m，最大堆内存256m
if [[ "${MODE}" == "standalone" ]]; then
    JAVA_OPT="${JAVA_OPT} -Xms128m -Xmx256m -Xmn256m"
    JAVA_OPT="${JAVA_OPT} -Dnacos.standalone=true"
else
    if [[ "${EMBEDDED_STORAGE}" == "embedded" ]]; then
        JAVA_OPT="${JAVA_OPT} -DembeddedStorage=true"
    fi
    JAVA_OPT="${JAVA_OPT} -server -Xms256m -Xmx512m -Xmn128m -XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=320m"
    JAVA_OPT="${JAVA_OPT} -XX:-OmitStackTraceInFastThrow -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=${BASE_DIR}/logs/java_heapdump.hprof"
    JAVA_OPT="${JAVA_OPT} -XX:-UseLargePages"
```



### Mysql持久化配置中心

```xml
vim nacos/conf/application.properties

#添加mysql的配置信息
spring.datasource.platform=mysql
db.num=1
db.url.0=jdbc:mysql://127.0.0.1:3306/nacos_config?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useUnicode=true&useSSL=false&serverTimezone=UTC
db.user=root
db.password=root
```

### 启动和登录

```shell
# 启动命令standalone代表着单机模式运行，非集群模式
sh startup.sh -m standalone

#登陆
http://118.24.221.85:8848/nacos
用户名：nacos 密码：nacos
```



## 服务注册与发现



![](http://markdown.wangyingbo.site/20201230101921.png)





### 版本对应

<table role="table">
<colgroup>
<col>
<col>
<col>
</colgroup>
<thead>
<tr>
<th>Spring Cloud Version</th>
<th>Spring Cloud Alibaba Version</th>
<th>Spring Boot Version</th>
</tr>
</thead>
<tbody>
<tr>
<td><p>Spring Cloud Hoxton.SR8</p></td>
<td><p>2.2.3.RELEASE</p></td>
<td><p>2.3.2.RELEASE</p></td>
</tr>
<tr>
<td><p>Spring Cloud Greenwich.SR6</p></td>
<td><p>2.1.3.RELEASE</p></td>
<td><p>2.1.13.RELEASE</p></td>
</tr>
<tr>
<td><p>Spring Cloud Hoxton.SR3</p></td>
<td><p>2.2.1.RELEASE</p></td>
<td><p>2.2.5.RELEASE</p></td>
</tr>
<tr>
<td><p>Spring Cloud Hoxton.RELEASE</p></td>
<td><p>2.2.0.RELEASE</p></td>
<td><p>2.2.X.RELEASE</p></td>
</tr>
<tr>
<td><p>Spring Cloud Greenwich</p></td>
<td><p>2.1.2.RELEASE</p></td>
<td><p>2.1.X.RELEASE</p></td>
</tr>
<tr>
<td><p>Spring Cloud Finchley</p></td>
<td><p>2.0.3.RELEASE</p></td>
<td><p>2.0.X.RELEASE</p></td>
</tr>
<tr>
<td><p>Spring Cloud Edgware</p></td>
<td><p>1.5.1.RELEASE(停止维护，建议升级)</p></td>
<td><p>1.5.X.RELEASE</p></td>
</tr>
</tbody>
</table>



<table role="table">
<colgroup>
<col>
<col>
<col>
<col>
<col>
<col>
</colgroup>
<thead>
<tr>
<th>Spring Cloud Alibaba Version</th>
<th>Sentinel Version</th>
<th>Nacos Version</th>
<th>RocketMQ Version</th>
<th>Dubbo Version</th>
<th>Seata Version</th>
</tr>
</thead>
<tbody>
<tr>
<td><p>2.2.3.RELEASE or 2.1.3.RELEASE or 2.0.3.RELEASE</p></td>
<td><p>1.8.0</p></td>
<td><p>1.3.3</p></td>
<td><p>4.4.0</p></td>
<td><p>2.7.8</p></td>
<td><p>1.3.0</p></td>
</tr>
<tr>
<td><p>2.2.1.RELEASE or 2.1.2.RELEASE or 2.0.2.RELEASE</p></td>
<td><p>1.7.1</p></td>
<td><p>1.2.1</p></td>
<td><p>4.4.0</p></td>
<td><p>2.7.6</p></td>
<td><p>1.2.0</p></td>
</tr>
<tr>
<td><p>2.2.0.RELEASE</p></td>
<td><p>1.7.1</p></td>
<td><p>1.1.4</p></td>
<td><p>4.4.0</p></td>
<td><p>2.7.4.1</p></td>
<td><p>1.0.0</p></td>
</tr>
<tr>
<td><p>2.1.1.RELEASE or 2.0.1.RELEASE or 1.5.1.RELEASE</p></td>
<td><p>1.7.0</p></td>
<td><p>1.1.4</p></td>
<td><p>4.4.0</p></td>
<td><p>2.7.3</p></td>
<td><p>0.9.0</p></td>
</tr>
<tr>
<td><p>2.1.0.RELEASE or 2.0.0.RELEASE or 1.5.0.RELEASE</p></td>
<td><p>1.6.3</p></td>
<td><p>1.1.1</p></td>
<td><p>4.4.0</p></td>
<td><p>2.7.3</p></td>
<td><p>0.7.1</p></td>
</tr>
</tbody>
</table>



### pom 引入

```java
<dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring-cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>${spring-boot.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-alibaba-dependencies</artifactId>
                <version>${nacos.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
```



```java
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
    </dependencies>
```



### 无缝替换Eureka

```java
server:
  port: 9528
spring:
  application:
    name: nacos-consumer
  cloud:
    nacos:
      discovery:
        server-addr: 127.0.0.1:8848

```

