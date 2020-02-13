---
title: Docker Compose-3
date: 2020-02-08 16:51:05
tags: Docker
categories: 软件
---

### Compose内的YML指令参考

* 接[Docker Compose-2](https://unit-serow.github.io/2020/02/08/Docker-Compose-2/)

1. **devices**
* 用于指定设备映射列表
* 实现语法:
```
devices:
  - "/dev/ttyUSB0:/dev/ttyUSB0"
```

---

2. **dns**
* 用于自定义 DNS 服务器，可以是单个值或列表的多个值
* 实现语法:
```
dns: 8.8.8.8

dns:
  - 8.8.8.8
  - 9.9.9.9
```

---

3. **dns_search**
* 用于自定义 DNS 搜索域
* 可以是单个值或列表
* 实现语法:
```
dns_search: example.com

dns_search:
  - dc1.example.com
  - dc2.example.com
```

---

4. **entrypoint**
* 用于覆盖容器默认的`entrypoint`
* 实现语法:
> `entrypoint: /code/entrypoint.sh`
* 或以下的列表格式:
```
entrypoint:
    - php
    - -d
    - zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20100525/xdebug.so
    - -d
    - memory_limit=-1
    - vendor/bin/phpunit
```

---

5. **env_file**
* 用于从文件添加环境变量
* 可以是单个值或列表的多个值
* 实现语法:
> `env_file: .env`
* 也可以是列表格式：
```
env_file:
  - ./common.env
  - ./apps/web.env
  - /opt/secrets.env
```

---

6. **environment**
* 用于添加环境变量
* 可以使用数组或字典，任何布尔值，布尔值需要用引号引起来，以确保`YML解析器`不会将其转换为`True`或`False`
* 实现语法:
```
environment:
  RACK_ENV: development
  SHOW: 'true'
```

---

7. **expose**
* 用于暴露端口，但不映射到宿主机，只被连接的服务访问
* 实现语法(仅可以指定内部端口为参数)：
```
expose:
 - "3000"
 - "8000"
```

---

8. **extra_hosts**
* 用于添加主机名映射
* 类似`docker client --add-host`
* 实现语法:
```
extra_hosts:
 - "somehost:162.242.195.82"
 - "otherhost:50.31.209.229"
```
* 以上会在此服务的内部容器中`/etc/hosts`创建一个具有`ip地址`和主机名的映射关系:
```
162.242.195.82  somehost
50.31.209.229   otherhost
```

---

9. **healthcheck**
* 用于检测 docker 服务是否健康运行
* 实现语法:
```
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost"] # 设置检测程序
  interval: 1m30s # 设置检测间隔
  timeout: 10s # 设置检测超时时间
  retries: 3 # 设置重试次数
  start_period: 40s # 启动后，多少秒开始启动检测程序
```

---

10. **image**
* 用于指定容器运行的镜像
* 以下格式都可以:
```
image: redis
image: ubuntu:14.04
image: tutum/influxdb
image: example-registry.com:4000/postgresql
image: a4bc65fd # 镜像id
```

---

11. **logging**
* 服务的日志记录配置
* `driver:`用于指定服务容器的日志记录驱动程序，默认值为`json-file`
* 可以有以下这三种选项
```
driver: "json-file"
driver: "syslog"
driver: "none"
```

* 仅在`json-file`驱动程序下，可以使用以下参数，限制日志得数量和大小
```
logging:
  driver: json-file
  options:
    max-size: "200k" # 单个文件大小为200k
    max-file: "10" # 最多10个文件
```

* 当达到文件限制上限，会自动删除旧得文件
* `syslog`驱动程序下，可以使用`syslog-address`指定日志接收地址
```
logging:
  driver: syslog
  options:
    syslog-address: "tcp://192.168.0.42:123"
```

---

12. **network_mode**
* 用于设置网络模式
* 实现语法:
```
network_mode: "bridge"
network_mode: "host"
network_mode: "none"
network_mode: "service:[service name]"
network_mode: "container:[container name/id]"
```

* networks
> 配置容器连接的网络，引用顶级`networks`下的条目
```
services:
  some-service:
    networks:
      some-network:
        aliases:
         - alias1
      other-network:
        aliases:
         - alias2
networks:
  some-network:
    # Use a custom driver
    driver: custom-driver-1
  other-network:
    # Use a custom driver which takes special options
    driver: custom-driver-2
```

* `aliases:`同一网络上的其他容器可以使用服务名称或此别名来连接到对应容器的服务

---

13. **restart**
* 使用示例:
```
restart: "no"
restart: always
restart: on-failure
restart: unless-stopped
```
* 参数说明:
> `no`:是默认的重启策略，在任何情况下都不会重启容器
> `always`:容器总是重新启动
> `on-failure`:在容器非正常退出时(退出状态非0)，才会重启容器
> `unless-stopped`:在容器退出时总是重启容器，但是不考虑在Docker守护进程启动时就已经停止了的容器

* `swarm集群`模式下，必须改用`restart_policy`

---

14. **secrets**
* 用于存储敏感数据
* 例如密码：
```
version: "3.1"
services:

mysql:
  image: mysql
  environment:
    MYSQL_ROOT_PASSWORD_FILE: /run/secrets/my_secret
  secrets:
    - my_secret

secrets:
  my_secret:
    file: ./my_secret.txt
```

---

15. **security_opt**
* 修改容器默认的`schema`标签
* 使用说明:
```
security-opt：
  - label:user:USER   # 设置容器的用户标签
  - label:role:ROLE   # 设置容器的角色标签
  - label:type:TYPE   # 设置容器的安全策略标签
  - label:level:LEVEL  # 设置容器的安全等级标签
```

---

16. **stop_grace_period**
* 指定在容器无法处理`SIGTERM`(或者任何`stop_signal`的信号)，等待多久后发送`SIGKILL`信号关闭容器
* 实现语法:
```
stop_grace_period: 1s # 等待 1 秒
stop_grace_period: 1m30s # 等待 1 分 30 秒 
```
* 默认的等待时间是 10 秒

---

17. **stop_signal**
* 设置停止容器的替代信号
* 默认情况下使用`SIGTERM`
* 以下示例，使用`SIGUSR1`替代信号`SIGTERM`来停止容器
> `stop_signal: SIGUSR1`

---

18. **sysctls**
* 设置容器中的内核参数，可以使用数组或字典格式
* 实现语法:
```
sysctls:
  net.core.somaxconn: 1024
  net.ipv4.tcp_syncookies: 0

sysctls:
  - net.core.somaxconn=1024
  - net.ipv4.tcp_syncookies=0
```

---

19. **tmpfs**
* 在容器内安装一个临时文件系统
* 可以是单个值或列表的多个值
* 实现语法:
```
tmpfs: /run

tmpfs:
  - /run
  - /tmp
```

---

20. **ulimits**
* 覆盖容器默认的`ulimit`
* 实现语法:
```
ulimits:
  nproc: 65535
  nofile:
    soft: 20000
    hard: 40000
```

---

21. **volumes**
* 将主机的数据卷或着文件挂载到容器里
* 实现语法:
```
version: "3.7"
services:
  db:
    image: postgres:latest
    volumes:
      - "/localhost/postgres.sock:/var/run/postgres/postgres.sock"
      - "/localhost/data:/var/lib/postgresql/data"
```
