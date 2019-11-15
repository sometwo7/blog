---
title: Linux 环境搭建 - Zookeeper 3.5.6
tags:
  - Linux
  - 环境搭建
  - zookeeper
categories:
  - Linux环境搭建
comments: true
abbrlink: f889c743
date: 2019-11-13 14:08:19
---

# 下载 zookeeper
- 官网下载地址
[https://zookeeper.apache.org/releases.html](https://zookeeper.apache.org/releases.html)
- 文件链接(2019-11-12可以访问)
[apache-zookeeper-3.5.6-bin.tar.gz](https://mirrors.tuna.tsinghua.edu.cn/apache/zookeeper/stable/apache-zookeeper-3.5.6-bin.tar.gz)

<!-- more -->

# 解压文件
上传 zookeeper 至 Linux 用户文件夹
```
# 解压
tar -zxvf ~/apache-zookeeper-3.5.6-bin.tar.gz -C /opt/
# 设置软连接，方便以后升级 zookeeper
ln -s /opt/apache-zookeeper-3.5.6-bin /opt/zookeeper
```

# 准备参数文件
- zookeeper 配置文件
zoo.cfg
```
echo "tickTime=2000" >> /opt/zookeeper/conf/zoo.cfg
echo "initLimit=10" >> /opt/zookeeper/conf/zoo.cfg
echo "syncLimit=5" >> /opt/zookeeper/conf/zoo.cfg
echo "dataDir=/opt/data/zookeeper" >> /opt/zookeeper/conf/zoo.cfg
echo "clientPort=2181" >> /opt/zookeeper/conf/zoo.cfg
echo "admin.serverPort=8081" >> /opt/zookeeper/conf/zoo.cfg
echo "4lw.commands.whitelist=*" >> /opt/zookeeper/conf/zoo.cfg
```

- java 配置文件
请自行下载安装 openjdk1.8 至 /opt/openjdk 文件夹下
```
echo "export JAVA_HOME=/opt/openjdk" >> /opt/zookeeper/conf/java.env
```

# 创建目录
```
mkdir -p /opt/data/zookeeper
```

# 启动 zookeeper
```
/opt/zookeeper/bin/zkServer.sh start /opt/zookeeper/conf/zoo.cfg
```

# 查看 zookeeper 状态

```
/opt/zookeeper/bin/zkServer.sh status /opt/zookeeper/conf/zoo.cfg
```

# 集群模式
- zoo.cfg 文件需要增加配置
> server.[myid] = hostname:节点同步数据端口:zk选举接口
```
echo "server.1=node1:2888:3888" >> /opt/zookeeper/conf/zoo.cfg
echo "server.2=node2:2888:3888" >> /opt/zookeeper/conf/zoo.cfg
echo "server.3=node3:2888:3888" >> /opt/zookeeper/conf/zoo.cfg
```

- 增加 myid
node1、node2、node3 分别执行 1、2、3
```
echo 1 >> opt/data/zookeeper/myid
```

# 附录
## 权限问题(修改文件属组)
- 修改属主
```
chown -R admin /opt/apache-zookeeper-3.5.6-bin
```
- 修改用户组
```
chown -R :admin /opt/apache-zookeeper-3.5.6-bin
```
- 根据文件属组，调整目标文件属组
```
chown -R --reference=/opt/apache-zookeeper-3.5.6-bin.tar.gz /opt/apache-zookeeper-3.5.6-bin
```

## 复制粘贴
上传文件至用户文件夹
```
sudo tar -zxvf ~/apache-zookeeper-3.5.6-bin.tar.gz -C /opt/
sudo su root

ln -s /opt/wildfly/openjdk/openjdk-1.8.0_92 /opt/openjdk
ln -s /opt/apache-zookeeper-3.5.6-bin /opt/zookeeper

echo "tickTime=2000" >> /opt/zookeeper/conf/zoo.cfg
echo "initLimit=10" >> /opt/zookeeper/conf/zoo.cfg
echo "syncLimit=5" >> /opt/zookeeper/conf/zoo.cfg
echo "dataDir=/opt/data/zookeeper" >> /opt/zookeeper/conf/zoo.cfg
echo "clientPort=2181" >> /opt/zookeeper/conf/zoo.cfg
echo "admin.serverPort=8081" >> /opt/zookeeper/conf/zoo.cfg
echo "4lw.commands.whitelist=*" >> /opt/zookeeper/conf/zoo.cfg

echo "export JAVA_HOME=/opt/openjdk" >> /opt/zookeeper/conf/java.env

mkdir -p /opt/data/zookeeper

chown -R --reference=/opt/logs /opt/zookeeper
chown -R --reference=/opt/logs /opt/apache-zookeeper-3.5.6-bin
chown -R --reference=/opt/logs /opt/openjdk
chown -R --reference=/opt/logs /opt/data

/opt/zookeeper/bin/zkServer.sh start /opt/zookeeper/conf/zoo.cfg

exit
exit


```