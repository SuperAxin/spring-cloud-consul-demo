# 透過 Docker 啟動 Consul
```
docker run \
  --name=consul-server \
  -d \
  -p 8500:8500 \
  -p 8600:8600/udp \
  hashicorp/consul \
  consul agent \
    -server \
    -ui \
    -node=server-1 \
    -bootstrap-expect=1 \
    -client=0.0.0.0 \
    -data-dir=/consul/data
```

# 配置 pom.xml
```
<!-- Spring Cloud -->
<properties>
    <java.version>21</java.version>
    <spring-cloud.version>2025.1.3</spring-cloud.version>
</properties>

<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>2025.1.3</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>

<!-- Spring Boot actuator -->
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>

<!-- Spring Cloud Consul -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-consul-discovery</artifactId>
</dependency>
```

#  配置 .properties
```
// 配置 properties
server.port=8081

spring.cloud.consul.host=localhost
spring.cloud.consul.port=8500
spring.cloud.consul.discovery.register=true
spring.cloud.consul.discovery.instance-id=${spring.application.name}:${server.port}
```
