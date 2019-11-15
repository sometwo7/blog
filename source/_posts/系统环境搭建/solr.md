---
title: Linux 环境搭建 - Solr 8.3.0
tags:
  - Linux
  - 环境搭建
  - solr
categories:
  - Linux环境搭建
comments: true
abbrlink: 46fcdcd9
date: 2019-11-13 16:18:19
---

# 下载 solr
- 官网下载地址
[https://lucene.apache.org/solr/downloads.html](https://lucene.apache.org/solr/downloads.html)
- 文件链接(2019-11-12可以访问)
[solr-8.3.0.zip](https://mirrors.tuna.tsinghua.edu.cn/apache/lucene/solr/8.3.0/solr-8.3.0.zip)

<!-- more -->

# 解压文件
上传 solr 至 Linux 用户文件夹
```
# 解压
unzip ~/solr-8.3.0.zip -d  /opt/
# 设置软连接，方便以后升级 solr
ln -s /opt/solr-8.3.0 /opt/solr
```

# 准备目录
```
mkdir -p /opt/data/solr
mkdir -p /opt/logs/solr
```

# 准备参数文件
## solr.in.sh
```
vim /opt/solr/bin/solr.in.sh
```
修改内容为
```
ZK_HOST="127.0.0.1:2181"
SOLR_JAVA_HOME="/opt/openjdk/"
SOLR_JAVA_MEM="-Xms1024m -Xmx1024m"
ZK_CLIENT_TIMEOUT="15000"
ENABLE_REMOTE_JMX_OPTS="true"
SOLR_PORT=8983
RMI_PORT=18983
SOLR_DATA_HOME=/opt/data/solr
SOLR_HOME=/opt/solr/server/solr
SOLR_LOG_LEVEL=INFO
SOLR_LOGS_DIR=/opt/logs/solr
```
其中 <b>ZK_HOST</b> 有值则以 cloud 模式启动
> 输出脚本
```
echo "ZK_HOST=127.0.0.1:2181" >> /opt/solr/bin/solr.in.sh
echo "SOLR_JAVA_HOME=\"/opt/openjdk/\"" >> /opt/solr/bin/solr.in.sh
echo "SOLR_JAVA_MEM=\"-Xms1024m -Xmx1024m\"" >> /opt/solr/bin/solr.in.sh
echo "ZK_CLIENT_TIMEOUT=\"15000\"" >> /opt/solr/bin/solr.in.sh
echo "ENABLE_REMOTE_JMX_OPTS=\"true\"" >> /opt/solr/bin/solr.in.sh
echo "SOLR_PORT=8983" >> /opt/solr/bin/solr.in.sh
echo "RMI_PORT=18983" >> /opt/solr/bin/solr.in.sh
echo "SOLR_DATA_HOME=/opt/data/solr" >> /opt/solr/bin/solr.in.sh
echo "SOLR_HOME=/opt/solr/server/solr" >> /opt/solr/bin/solr.in.sh
echo "SOLR_LOG_LEVEL=INFO" >> /opt/solr/bin/solr.in.sh
echo "SOLR_LOGS_DIR=/opt/logs/solr" >> /opt/solr/bin/solr.in.sh
```


# 启动 solr
```
/opt/solr/bin/solr start
```

# 查看 solr 状态

```
/opt/solr/bin/solr status
```

# 附录
## 权限问题(修改文件属组)
- 修改属主
```
chown -R admin /opt/solr
```
- 修改用户组
```
chown -R :admin /opt/solr
```
- 根据文件属组，调整目标文件属组
```
chown -R --reference=/opt/solr-8.3.0.zip /opt/solr
```

## 复制粘贴
上传文件至用户文件夹
```
sudo unzip ~/solr-8.3.0.zip -d  /opt/
sudo su root

ln -s /opt/wildfly/openjdk/openjdk-1.8.0_92 /opt/openjdk
ln -s /opt/solr-8.3.0 /opt/solr

echo "ZK_HOST=10.27.25.67:2181" >> /opt/solr/bin/solr.in.sh
echo "SOLR_JAVA_HOME=\"/opt/openjdk/\"" >> /opt/solr/bin/solr.in.sh
echo "SOLR_JAVA_MEM=\"-Xms1024m -Xmx1024m\"" >> /opt/solr/bin/solr.in.sh
echo "ZK_CLIENT_TIMEOUT=\"15000\"" >> /opt/solr/bin/solr.in.sh
echo "ENABLE_REMOTE_JMX_OPTS=\"true\"" >> /opt/solr/bin/solr.in.sh
echo "SOLR_PORT=8983" >> /opt/solr/bin/solr.in.sh
echo "RMI_PORT=18983" >> /opt/solr/bin/solr.in.sh
echo "SOLR_DATA_HOME=/opt/data/solr" >> /opt/solr/bin/solr.in.sh
echo "SOLR_HOME=/opt/solr/server/solr" >> /opt/solr/bin/solr.in.sh
echo "SOLR_LOG_LEVEL=INFO" >> /opt/solr/bin/solr.in.sh
echo "SOLR_LOGS_DIR=/opt/logs/solr" >> /opt/solr/bin/solr.in.sh

mkdir -p /opt/data/solr
mkdir -p /opt/logs/solr

chown -R --reference=/opt/logs /opt/solr
chown -R --reference=/opt/logs /opt/solr-8.3.0
chown -R --reference=/opt/logs /opt/openjdk
chown -R --reference=/opt/logs /opt/data
chown -R --reference=/opt/logs /opt/logs/solr

sudo su jbossuser
/opt/solr/bin/solr start

```
