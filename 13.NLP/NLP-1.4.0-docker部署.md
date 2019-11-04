# NLP-1.4.0-docker部署

> **注意：安装 Docker 操作系统（Centos/Redhat）必须是 7.0 以上版本。**

## 准备

### 软件包

```bash
> cd /opt

# 检查
> ll docker-ce-18-local.tar.gz docker-ce-local.repo nlp.zip
-rw-r--r-- 1 root root   72149679 8月  12 11:18 docker-ce-18-local.tar.gz # docker安装软件包
-rw-r--r-- 1 root root         87 8月  12 16:30 docker-ce-local.repo # repo文件
-rw-r--r-- 1 root root 7317676679 8月  12 11:20 nlp.zip # 容器

# 准备软件包数据
> mkdir docker-ce-18-local
> ll -d /opt/docker-ce-local.repo 
-rw-r--r-- 1 root root 87 8月  12 16:30 /opt/docker-ce-local.repo

> mv docker-ce-18-local.tar.gz docker-ce-18-local
> cd /opt/docker-ce-18-local
> pwd
/opt/docker-ce-18-local

# 解压
> tar -zxvf docker-ce-18-local.tar.gz
[...]

# 检查
> ll
总用量 143092
-rw-r--r-- 1 root root   255648 11月 12 2018 audit-2.8.4-4.el7.x86_64.rpm
-rw-r--r-- 1 root root   102448 11月 12 2018 audit-libs-2.8.4-4.el7.x86_64.rpm
-rw-r--r-- 1 root root    78216 11月 12 2018 audit-libs-python-2.8.4-4.el7.x86_64.rpm
-rw-r--r-- 1 root root   302068 11月 12 2018 checkpolicy-2.5-8.el7.x86_64.rpm
-rw-r--r-- 1 root root 23157088 11月  8 2018 containerd.io-1.2.0-3.el7.x86_64.rpm
-rw-r--r-- 1 root root    38436 12月  1 2018 container-selinux-2.74-1.el7.noarch.rpm
-rw-r--r-- 1 root root    95840 8月  10 2017 createrepo-0.9.9-28.el7.noarch.rpm
-rw-r--r-- 1 root root    83984 7月   4 2014 deltarpm-3.6-3.el7.x86_64.rpm
-rw-r--r-- 1 root root   299288 11月 21 2018 device-mapper-1.02.149-10.el7_6.2.x86_64.rpm
-rw-r--r-- 1 root root   192328 11月 21 2018 device-mapper-event-1.02.149-10.el7_6.2.x86_64.rpm
-rw-r--r-- 1 root root   191868 11月 21 2018 device-mapper-event-libs-1.02.149-10.el7_6.2.x86_64.rpm
-rw-r--r-- 1 root root   327236 11月 21 2018 device-mapper-libs-1.02.149-10.el7_6.2.x86_64.rpm
-rw-r--r-- 1 root root   414576 4月  25 2018 device-mapper-persistent-data-0.7.3-3.el7.x86_64.rpm
-rw-r--r-- 1 root root 19603880 11月  8 2018 docker-ce-18.09.0-3.el7.x86_64.rpm
-rw-r--r-- 1 root root 72149679 8月  12 11:18 docker-ce-18-local.tar.gz
-rw-r--r-- 1 root root 14676972 11月  8 2018 docker-ce-cli-18.09.0-3.el7.x86_64.rpm
-rw-r--r-- 1 root root     1627 10月 25 2018 gpg
-rw-r--r-- 1 root root    67652 11月 12 2018 libcgroup-0.41-20.el7.x86_64.rpm
-rw-r--r-- 1 root root    56988 8月  11 2017 libseccomp-2.3.1-3.el7.x86_64.rpm
-rw-r--r-- 1 root root   165932 11月 12 2018 libselinux-2.5-14.1.el7.x86_64.rpm
-rw-r--r-- 1 root root   241132 11月 12 2018 libselinux-python-2.5-14.1.el7.x86_64.rpm
-rw-r--r-- 1 root root   155092 11月 12 2018 libselinux-utils-2.5-14.1.el7.x86_64.rpm
-rw-r--r-- 1 root root   154244 11月 12 2018 libsemanage-2.5-14.el7.x86_64.rpm
-rw-r--r-- 1 root root   115284 11月 12 2018 libsemanage-python-2.5-14.el7.x86_64.rpm
-rw-r--r-- 1 root root   304196 11月 12 2018 libsepol-2.5-10.el7.x86_64.rpm
-rw-r--r-- 1 root root   252528 6月  24 2016 libxml2-python-2.9.1-6.el7_2.3.x86_64.rpm
-rw-r--r-- 1 root root  1366568 11月 21 2018 lvm2-2.02.180-10.el7_6.2.x86_64.rpm
-rw-r--r-- 1 root root  1125716 11月 21 2018 lvm2-libs-2.02.180-10.el7_6.2.x86_64.rpm
-rw-r--r-- 1 root root   937868 11月 12 2018 policycoreutils-2.5-29.el7.x86_64.rpm
-rw-r--r-- 1 root root   466616 11月 12 2018 policycoreutils-python-2.5-29.el7.x86_64.rpm
-rw-r--r-- 1 root root   232224 7月  23 2015 python-chardet-2.2.1-1.el7_1.noarch.rpm
-rw-r--r-- 1 root root    32084 7月   4 2014 python-deltarpm-3.6-3.el7.x86_64.rpm
-rw-r--r-- 1 root root    32880 7月   4 2014 python-IPy-0.75-6.el7.noarch.rpm
-rw-r--r-- 1 root root   273012 7月   4 2014 python-kitchen-1.1.1-5.el7.noarch.rpm
drwxr-xr-x 2 root root     4096 1月   4 2019 repodata
-rw-r--r-- 1 root root   494472 11月 29 2018 selinux-policy-3.13.1-229.el7_6.6.noarch.rpm
-rw-r--r-- 1 root root  7245312 11月 29 2018 selinux-policy-targeted-3.13.1-229.el7_6.6.noarch.rpm
-rw-r--r-- 1 root root   635184 11月 12 2018 setools-libs-3.3.8-4.el7.x86_64.rpm
-rw-r--r-- 1 root root   124108 11月 12 2018 yum-utils-1.1.31-50.el7.noarch.rpm

# 切换目录
> cd /opt/
> mv docker-ce-local.repo /etc/yum.repos.d/

# 清缓存
> yum clean all
已加载插件：fastestmirror
正在清理软件源： docker
Cleaning up list of fastest mirrors
Other repos take up 82 M of disk space (use --verbose for details)

# 加载repo
> yum repolist
已加载插件：fastestmirror
Determining fastest mirrors
docker                                                                                                                                                                                                         | 2.9 kB  00:00:00     
docker/primary_db                                                                                                                                                                                              |  59 kB  00:00:00     
源标识                                                                                                        源名称                                                                                                              状态
docker                                                                                                        docker_local                                                                                                        36
repolist: 36

# 检查
> yum list | grep docker-ce
docker-ce.x86_64                      3:18.09.0-3.el7                  @docker  
docker-ce-cli.x86_64                  1:18.09.0-3.el7                  @docker  
```

## 安装docker

```bash
> yum -y install docker-ce
[...]
已安装:
  docker-ce.x86_64 3:18.09.0-3.el7                                                                                                                                                                                                    

作为依赖被安装:
  audit-libs-python.x86_64 0:2.8.4-4.el7  checkpolicy.x86_64 0:2.5-8.el7       container-selinux.noarch 2:2.74-1.el7       containerd.io.x86_64 0:1.2.0-3.el7  docker-ce-cli.x86_64 1:18.09.0-3.el7  libcgroup.x86_64 0:0.41-20.el7 
  libsemanage-python.x86_64 0:2.5-14.el7  policycoreutils.x86_64 0:2.5-29.el7  policycoreutils-python.x86_64 0:2.5-29.el7  python-IPy.noarch 0:0.75-6.el7      setools-libs.x86_64 0:3.3.8-4.el7    

完毕！

# 启动docker
> systemctl start docker

# 检查
> docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE

# 检查 x 2
> systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; disabled; vendor preset: disabled)
   Active: active (running) since 一 2019-08-12 16:22:20 CST; 21min ago
     Docs: https://docs.docker.com
 Main PID: 28345 (dockerd)
    Tasks: 99
   Memory: 22.3G
   CGroup: /system.slice/docker.service
           ├─28345 /usr/bin/dockerd -H unix://
           └─28372 containerd --config /var/run/docker/containerd/containerd.toml --log-level info

8月 12 16:22:20 zhijian-analysis-2 dockerd[28345]: time="2019-08-12T16:22:20.270041455+08:00" level=info msg="pickfirstBalancer: HandleSubConnStateChange: 0xc4208021e0, READY" module=grpc
8月 12 16:22:20 zhijian-analysis-2 dockerd[28345]: time="2019-08-12T16:22:20.312675426+08:00" level=info msg="Graph migration to content-addressability took 0.00 seconds"
8月 12 16:22:20 zhijian-analysis-2 dockerd[28345]: time="2019-08-12T16:22:20.317205723+08:00" level=info msg="Loading containers: start."
8月 12 16:22:20 zhijian-analysis-2 dockerd[28345]: time="2019-08-12T16:22:20.464684428+08:00" level=info msg="Default bridge (docker0) is assigned with an IP address 172.17.0.0/16. Daemon option --bip can be use...red IP address"
8月 12 16:22:20 zhijian-analysis-2 dockerd[28345]: time="2019-08-12T16:22:20.508263908+08:00" level=info msg="Loading containers: done."
8月 12 16:22:20 zhijian-analysis-2 dockerd[28345]: time="2019-08-12T16:22:20.556957414+08:00" level=info msg="Docker daemon" commit=4d60db4 graphdriver(s)=overlay2 version=18.09.0
8月 12 16:22:20 zhijian-analysis-2 dockerd[28345]: time="2019-08-12T16:22:20.557076857+08:00" level=info msg="Daemon has completed initialization"
8月 12 16:22:20 zhijian-analysis-2 dockerd[28345]: time="2019-08-12T16:22:20.567794860+08:00" level=warning msg="Could not register builder git source: failed to find git binary: exec: \"git\": executable file not found in $PATH"
8月 12 16:22:20 zhijian-analysis-2 dockerd[28345]: time="2019-08-12T16:22:20.575961387+08:00" level=info msg="API listen on /var/run/docker.sock"
8月 12 16:22:20 zhijian-analysis-2 systemd[1]: Started Docker Application Container Engine.
Hint: Some lines were ellipsized, use -l to show in full.
```

## 加载容器

```bash
# 切换目录
> cd /opt/

# 检查
> ll nlp.zip 
-rw-r--r-- 1 root root 7317676679 8月  12 11:20 nlp.zip

# 解压
> unzip nlp.zip
[...]

# 检查
> ll nlp_v1.3.tar 
-rw------- 1 root root 27831134720 7月  18 17:51 nlp_v1.3.tar

# 加载容器
> docker load < nlp_v1.3.tar 
d69483a6face: Loading layer [==================================================>]  209.5MB/209.5MB
6aa6bc996276: Loading layer [==================================================>]  210.4MB/210.4MB
4ff7ec73f4b7: Loading layer [==================================================>]  111.2MB/111.2MB
db6ada7048a4: Loading layer [==================================================>]  15.87kB/15.87kB
62dff5c424f9: Loading layer [==================================================>]  2.048kB/2.048kB
91ddd01cafd4: Loading layer [==================================================>]  2.048kB/2.048kB
17d0314eac06: Loading layer [==================================================>]  6.144kB/6.144kB
178dbe989ad8: Loading layer [==================================================>]  14.01GB/14.01GB
b79fb244286a: Loading layer [==================================================>]  108.6MB/108.6MB
b25e73b80031: Loading layer [==================================================>]  107.8MB/107.8MB
9f7a904bb37e: Loading layer [==================================================>]  3.327MB/3.327MB
7e37f9d25709: Loading layer [==================================================>]  3.021GB/3.021GB
c0288c0d193c: Loading layer [==================================================>]  1.051GB/1.051GB
52657f2ab0f6: Loading layer [==================================================>]  107.6MB/107.6MB
85d8286603a6: Loading layer [==================================================>]  107.8MB/107.8MB
0285cd1c9a44: Loading layer [==================================================>]  3.327MB/3.327MB
34f91eafe7fa: Loading layer [==================================================>]    7.8GB/7.8GB
512c3d1dd967: Loading layer [==================================================>]    981MB/981MB
Loaded image: nlp_v1.3:1.0

# 检查
> docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nlp_v1.3            1.0                 3b3ada467561        3 weeks ago         27.5GB
```

## 启动容器

```bash
# 查看现有容器
# 记住 IMAGE ID 之后会用到
> docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nlp_v1.3            1.0                 3b3ada467561        3 weeks ago         27.5GB

# 查看现有运行容器
> docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

# 创建容器
# 参数说明
# --name 容器名称
# -d 后台启动
# -p 端口映射
# --privileged=true 将系统所有能力都开放给容器
# 3b3ada467561 之前 docker images 出的 nlp_v1.3 的 IMAGE ID 
# 端口说明
# 3306 mysql 数据库
# 8088 java tomcat
# 8000 python django
# 22 ssh
# 7474 neo4j 接口
# 7687 neo4j 页面
> docker run --name=cwtap_poc -d -p 13306:3306 -p 18088:8088 -p 18000:8000 -p 822:22 -p 17474:7474 -p 17687:7687 --privileged=true 3b3ada467561 /usr/sbin/init
8b39a2d1169f3835c2d3aa95e3db3d324bcdc3b4c48f9ab9d304527580f83097

# 检查
> docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                                                                                                                                              NAMES
8b39a2d1169f        3b3ada467561        "/usr/sbin/init"    19 seconds ago      Up 18 seconds       0.0.0.0:822->22/tcp, 0.0.0.0:13306->3306/tcp, 0.0.0.0:17474->7474/tcp, 0.0.0.0:17687->7687/tcp, 0.0.0.0:18000->8000/tcp, 0.0.0.0:18088->8088/tcp   cwtap_poc

# 进入容器
# 8b39a2d1169f 为 docker ps 出来的 CONTAINER ID
> docker exec -it 8b39a2d1169f /bin/bash
[root@8b39a2d1169f /] > ll /opt/
total 3835648
drwxr-xr-x  1 root root       4096 7月  18 06:37 CWTAP
-rw-r--r--  1 root root 1969471125 7月  10 01:59 CWTAP_25.zip
drwxr-xr-x  4 root root       4096 1月   9  2019 hanlp_datas
-rw-r--r--  1 root root  702351480 7月  10 02:08 hanlp_datas.zip
drwxr-xr-x  8 root root       4096 6月  23  2016 jdk1.8.0_102
-rw-r--r--  1 root root  181435897 7月  10 02:08 jdk-8u102-linux-x64.gz
drwxr-xr-x 10 root root       4096 7月  10 01:34 mysql-5.7.17-linux-glibc2.5-x86_64
-rw-r--r--  1 root root  654007697 7月  10 01:32 mysql-5.7.17-linux-glibc2.5-x86_64.tar.gz
drwxr-xr-x  2 root root       4096 7月  15 03:47 packages
-rw-r--r--  1 root root  397452303 7月  15 03:41 package.zip
drwxr-xr-x  1 root root       4096 7月  18 09:03 proconfig
drwxr-xr-x 18 root root       4096 7月  10 01:20 Python-3.6.6
-rw-r--r--  1 root root   22930752 7月   9 06:55 Python-3.6.6.tgz
drwxrwxrwx  1 root root       4096 7月  11 06:11 tomcat7
```

## 修改配置

> **注意：下述命令均在docker容器中执行。**

### 修改 java 部分相关配置

```bash
#!# 注意：下述命令均在docker容器中执行
[root@8b39a2d1169f /] > cd /opt/CWTAP/webroot/WEB-INF/classes/

# 检查
[root@8b39a2d1169f classes] > ll
total 3932
-rw-r--r--  1 root root     568 6月  28 09:11 antonym.dic
-rw-r--r--  1 root root    8798 6月  28 09:11 bank.dic
-rw-r--r--  1 root root     151 6月  28 09:11 characterwords.dic
drwxr-xr-x  3 root root    4096 6月  28 09:11 cn
drwxr-xr-x  1 root root    4096 7月  15 08:34 com
-rw-r--r--  1 root root    3642 7月  18 07:02 common.properties
-rw-r--r--  1 root root    3606 7月  15 08:30 common.properties.0715
-rw-r--r--  1 root root    1762 6月  28 09:11 degreewords.txt
-rw-r--r--  1 root root 1784579 6月  28 09:11 emotionwords.dic
-rw-r--r--  1 root root    2406 6月  28 09:11 hanlp.properties
-rw-r--r--  1 root root     406 6月  28 09:11 IKAnalyzer.cfg.xml
-rw-r--r--  1 root root     802 7月  17 08:32 jdbc.properties
-rw-r--r--  1 root root     271 6月  28 09:11 log4j.properties
drwxr-xr-x  3 root root    4096 6月  28 09:11 META-INF
-rw-r--r--  1 root root  127581 6月  28 09:11 negativewords.txt
-rw-r--r--  1 root root     622 6月  28 09:11 nopolite.dic
drwxr-xr-x 12 root root    4096 6月  28 09:11 org
-rw-r--r--  1 root root   70310 6月  28 09:11 positivewords.txt
-rw-r--r--  1 root root   64011 6月  28 09:11 stopword.dic
-rw-r--r--  1 root root  200595 6月  28 09:11 synonyms.dic
-rw-r--r--  1 root root    1078 6月  28 09:11 talkSummaryRule.txt
-rw-r--r--  1 root root 1694830 6月  28 09:11 words.dic

# 修改 java 部分相关配置
# :%s/10.0.3.24/10.242.1.110/g # 替换所有IP（10.0.3.24）地址到本机IP
[root@8b39a2d1169f classes] > vim common.properties
```

### 修改 js 部分相关配置

```bash
#!# 注意：下述命令均在docker容器中执行
# 切换目录
[root@8b39a2d1169f classes] > cd /opt/CWTAP/webroot/js/pages

# 检查
[root@8b39a2d1169f pages] > ll common.js
-rw-r--r-- 1 root root 74884 9月   3 09:05 common.js

# 修改 js 部分相关配置
# :%s/10.0.3.24/10.242.1.110/g # 替换所有IP（10.0.3.24）地址到本机IP
[root@8b39a2d1169f pages] > vim common.js
```

### 修改 python 部分相关配置

```bash
#!# 注意：下述命令均在docker容器中执行
# 切换目录
[root@8b39a2d1169f pages] > cd /opt/CWTAP/cwtap

# 检查
[root@8b39a2d1169f pages] > ll settings.py 
-rw-r--r-- 1 root root 33921 9月   3 10:03 settings.py

# 修改 python 部分相关配置
# :%s/10.0.3.24/10.242.1.110/g # 替换所有IP（10.0.3.24）地址到本机IP
[root@8b39a2d1169f pages] > vim settings.py
```

## 启动服务

> **注意：下述命令均在docker容器中执行。**


### 启动bert服务

```bash
# 进入bert启动目录
[root@8b39a2d1169f pages] > cd /opt/bert/chinese_L-12_H-768_A-12
[root@8b39a2d1169f pages] > nohup bert-serving-start -num_worker 8 -model_dir /opt/bert/chinese_L-12_H-768_A-12 &
# 启动bert服务
# 参数说明
# --num_worker 启动bert的work数量
# -model_dir 指定bert模型路径

# 检查bert服务是否启动
[root@8b39a2d1169f pages] > ps -ef |grep bert
root     15240     1  0 10月30 ?      00:00:14 /root/.venvs/cwtap/bin/python3.6 /root/.venvs/cwtap/bin/bert-serving-start -model_dir /opt/bert/chinese_L-12_H-768_A-12 -num_worker 8
root     17043 15240  0 10月30 ?      00:00:10 /root/.venvs/cwtap/bin/python3.6 /root/.venvs/cwtap/bin/bert-serving-start -model_dir /opt/bert/chinese_L-12_H-768_A-12 -num_worker 8
root     17048 15240  3 10月30 ?      04:09:40 /root/.venvs/cwtap/bin/python3.6 /root/.venvs/cwtap/bin/bert-serving-start -model_dir /opt/bert/chinese_L-12_H-768_A-12 -num_worker 8
root     17051 15240  3 10月30 ?      04:07:48 /root/.venvs/cwtap/bin/python3.6 /root/.venvs/cwtap/bin/bert-serving-start -model_dir /opt/bert/chinese_L-12_H-768_A-12 -num_worker 8
root     17054 15240  3 10月30 ?      04:14:32 /root/.venvs/cwtap/bin/python3.6 /root/.venvs/cwtap/bin/bert-serving-start -model_dir /opt/bert/chinese_L-12_H-768_A-12 -num_worker 8
root     17057 15240  3 10月30 ?      04:21:57 /root/.venvs/cwtap/bin/python3.6 /root/.venvs/cwtap/bin/bert-serving-start -model_dir /opt/bert/chinese_L-12_H-768_A-12 -num_worker 8
root     17060 15240  3 10月30 ?      04:25:09 /root/.venvs/cwtap/bin/python3.6 /root/.venvs/cwtap/bin/bert-serving-start -model_dir /opt/bert/chinese_L-12_H-768_A-12 -num_worker 8
root     17063 15240  3 10月30 ?      04:14:40 /root/.venvs/cwtap/bin/python3.6 /root/.venvs/cwtap/bin/bert-serving-start -model_dir /opt/bert/chinese_L-12_H-768_A-12 -num_worker 8
root     17067 15240  3 10月30 ?      04:10:34 /root/.venvs/cwtap/bin/python3.6 /root/.venvs/cwtap/bin/bert-serving-start -model_dir /opt/bert/chinese_L-12_H-768_A-12 -num_worker 8
root     17072 15240  3 10月30 ?      04:07:08 /root/.venvs/cwtap/bin/python3.6 /root/.venvs/cwtap/bin/bert-serving-start -model_dir /opt/bert/chinese_L-12_H-768_A-12 -num_worker 8
root     29796 29672  0 08:34 pts/58   00:00:00 grep --color=auto bert
```

### 使用 Supervisor 启动服务

```bash
#!# 注意：下述命令均在docker容器中执行
# 切换目录
[root@8b39a2d1169f pages] > cd ~
# 检查 supervisor 服务是否启动
[root@8b39a2d1169f ~] > ps aux | grep supervisor
root      1459  0.0  0.0  12364   980 pts/0    S+   07:55   0:00 grep --color=auto supervisor

# 启动 supervisor 
[root@8b39a2d1169f ~] > supervisord -c /etc/supervisord.conf

# 检查
[root@8b39a2d1169f ~] > ps aux | grep supervisor
root      1485  0.2  0.0 142512 14396 ?        Ss   07:57   0:00 /usr/bin/python /usr/bin/supervisord -c /etcsupervisord.conf
root      1850  0.0  0.0  12364   976 pts/0    S+   07:57   0:00 grep --color=auto supervisor

# 检查服务是否启动
[root@8b39a2d1169f ~] > echo "exit" | supervisorctl 
cwtap                            RUNNING   pid 1488, uptime 0:01:02
mysql                            RUNNING   pid 1589, uptime 0:01:01
neo4j                            RUNNING   pid 1486, uptime 0:01:02
redis                            RUNNING   pid 1487, uptime 0:01:02
tomcat                           RUNNING   pid 1491, uptime 0:01:02
supervisor> 

# 重启服务可执行如下命令
# 下面以 cwtap 为例，具体服务重启如下：
# supervisorctl restart cwtap # 重启 python 服务
# supervisorctl restart mysql # 重启 mysql 服务
# supervisorctl restart neo4j # 重启 neo4j 服务
# supervisorctl restart redis # 重启 redis 服务
# supervisorctl restart tomcat # 重启 tomcat 服务
[root@8b39a2d1169f ~] > supervisorctl restart cwtap
cwtap: stopped
cwtap: started
```

### 手动启动服务

> **注意：若已经执行 使用 Supervisor 启动服务 则该步骤可以省略，可直接跳到 退出容器 章节继续执行。**

#### 启动 Mysql 服务

```bash
# 切换目录
[root@8b39a2d1169f ~] > cd /usr/local/mysql/support-files/
[root@8b39a2d1169f support-files] > ll
total 28
-rw-r--r-- 1 7161 31415   773 11月 28  2016 magic
-rw-r--r-- 1 7161 31415  1126 11月 28  2016 my-default.cnf
-rwxr-xr-x 1 7161 31415  1061 11月 28  2016 mysqld_multi.server
-rwxr-xr-x 1 7161 31415   894 11月 28  2016 mysql-log-rotate
-rwxr-xr-x 1 7161 31415 10886 11月 28  2016 mysql.server

# 启动服务
[root@8b39a2d1169f support-files] > /usr/local/mysql/support-files/mysql.server start
Starting MySQL. SUCCESS! 

# 检查
[root@8b39a2d1169f support-files] > ps aux | grep mysql
root      1318  0.0  0.0  15092  1728 pts/0    S    09:22   0:00 /bin/sh /usr/local/mysql/bin/mysqld_safe --datadir=/var/lib/mysql --pid-file=/var/lib/mysql/8b39a2d1169f.pid
mysql     1547  1.3  0.3 1181740 186400 pts/0  Sl   09:22   0:00 /usr/local/mysql/bin/mysqld --basedir=/usr/local/mysql --datadir=/var/lib/mysql --plugin-dir=/usr/local/mysql/lib/plugin --user=mysql --log-error=/var/log/mysqld.log --pid-file=/var/lib/mysql/8b39a2d1169f.pid --socket=/var/lib/mysql/mysql.sock
root      1578  0.0  0.0  12364   980 pts/0    S+   09:23   0:00 grep --color=auto mysql

# 检查 x 2
mysql -uroot -proot123 -e "show databases;"
mysql: [Warning] Using a password on the command line interface can be insecure.
+--------------------+
| Database           |
+--------------------+
| information_schema |
| cenlp              |
| cwtap              |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
```

#### 启动 Neo4j（图数据库） 服务

```bash
# 切换目录
[root@8b39a2d1169f support-files] > cd /usr/local/neo4j/bin/
[root@8b39a2d1169f bin] > ll
total 48
-rwxr-xr-x 1 root root  1991 1月  15  2019 cypher-shell
-rwxr-xr-x 1 root root 14351 7月  18 03:32 neo4j
-rwxr-xr-x 1 root root  5650 1月  15  2019 neo4j-admin
-rwxr-xr-x 1 root root  5631 1月  15  2019 neo4j-import
-rwxr-xr-x 1 root root  5629 1月  15  2019 neo4j-shell
drwxrwxrwx 2 root root  4096 1月  15  2019 tools

# 启动服务
[root@8b39a2d1169f bin] > /usr/local/neo4j/bin/neo4j start
Active database: db_gd
Directories in use:
  home:         /usr/local/neo4j
  config:       /usr/local/neo4j/conf
  logs:         /usr/local/neo4j/logs
  plugins:      /usr/local/neo4j/plugins
  import:       /usr/local/neo4j/import
  data:         /usr/local/neo4j/data
  certificates: /usr/local/neo4j/certificates
  run:          /usr/local/neo4j/run
Starting Neo4j.
Started neo4j (pid 1685). It is available at http://0.0.0.0:7474/
There may be a short delay until the server is ready.
See /usr/local/neo4j/logs/neo4j.log for current status.

# 检查
[root@8b39a2d1169f bin] > ps aux | grep neo4j
root      1685 31.1  2.3 20544540 1170304 pts/0 Sl  09:26   0:16 /opt/jdk1.8.0_102/bin/java -cp /usr/local/neo4j/plugins:/usr/local/neo4j/conf:/usr/local/neo4j/lib/*:/usr/local/neo4j/plugins/* -server -XX:+UseG1GC -XX:-OmitStackTraceInFastThrow -XX:+AlwaysPreTouch -XX:+UnlockExperimentalVMOptions -XX:+TrustFinalNonStaticFields -XX:+DisableExplicitGC -Djdk.tls.ephemeralDHKeySize=2048 -Djdk.tls.rejectClientInitiatedRenegotiation=true -Dunsupported.dbms.udc.source=tarball -Dfile.encoding=UTF-8 org.neo4j.server.CommunityEntryPoint --home-dir=/usr/local/neo4j --config-dir=/usr/local/neo4j/conf
root      1804  0.0  0.0  12364   980 pts/0    S+   09:27   0:00 grep --color=auto neo4j

```

#### 启动 Redis 服务

```bash
# 切换目录
[root@8b39a2d1169f bin] > cd ~

# 启动服务
[root@8b39a2d1169f ~] > redis-server /etc/redis/6379.conf

# 检查
[root@8b39a2d1169f ~] > ps aux | grep redis
root     13535  0.0  0.0  12364   980 pts/10   S+   01:29   0:00 grep --color=auto redis
root     30495  0.0  0.0  30852  2192 ?        Sl   9月03   0:31 /usr/local/redis/bin/redis-server *:6379
```

#### 启动 Java 服务

```bash
# 切换目录
[root@8b39a2d1169f ~] > cd /opt/tomcat7/
[root@8b39a2d1169f tomcat7] > ll
total 156
drwxrwxrwx 1 root root  4096 7月  15 08:25 bin
drwxrwxrwx 1 root root  4096 7月  15 08:26 conf
-rwxrwxrwx 1 root root   218 7月  10 01:50 correctWords.txt
drwxrwxrwx 1 root root 12288 7月  10 01:50 extlib
drwxrwxrwx 1 root root  4096 7月  10 01:50 lib
-rwxrwxrwx 1 root root 56812 7月  10 01:50 LICENSE
drwxrwxrwx 1 root root  4096 7月  18 06:39 logs
-rwxrwxrwx 1 root root  1192 7月  10 01:50 NOTICE
-rwxrwxrwx 1 root root  8974 7月  10 01:50 RELEASE-NOTES
-rwxrwxrwx 1 root root 16204 7月  10 01:50 RUNNING.txt
drwxrwxrwx 1 root root  4096 7月  10 01:50 spark-warehouse
-rwxrwxrwx 1 root root     0 7月  10 01:50 stopWords.txt
drwxrwxrwx 1 root root 20480 7月  10 01:50 temp
drwxrwxrwx 1 root root  4096 7月  10 01:50 webapps
drwxrwxrwx 1 root root  4096 7月  10 01:50 work
drwxrwxrwx 1 root root  4096 7月  10 01:50 上传语音文件地址Logs

# 启动服务
[root@8b39a2d1169f tomcat7] > /opt/tomcat7/bin/startup.sh 
Using CATALINA_BASE:   /opt/tomcat7
Using CATALINA_HOME:   /opt/tomcat7
Using CATALINA_TMPDIR: /opt/tomcat7/temp
Using JRE_HOME:        /opt/jdk1.8.0_102/jre
Using CLASSPATH:       /opt/tomcat7/bin/bootstrap.jar:/opt/tomcat7/bin/tomcat-juli.jar
Tomcat started.

# 检查
[root@8b39a2d1169f tomcat7] > ps aux | grep tomcat
root      1815  285  6.3 39204232 3136136 pts/0 Sl  09:29   1:28 /opt/jdk1.8.0_102/jre/bin/java -Djava.util.logging.config.file=/opt/tomcat7/conf/logging.properties -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager -Xms1024m -Xmx32768m -XX:MaxPermSize=1024m -Djava.endorsed.dirs=/opt/tomcat7/endorsed -classpath /opt/tomcat7/bin/bootstrap.jar:/opt/tomcat7/bin/tomcat-juli.jar -Dcatalina.base=/opt/tomcat7 -Dcatalina.home=/opt/tomcat7 -Djava.io.tmpdir=/opt/tomcat7/temp org.apache.catalina.startup.Bootstrap start
root      1877  0.0  0.0  12364   980 pts/0    S+   09:30   0:00 grep --color=auto tomcat
```

#### 启动 Python 服务

```bash
# 切换目录
[root@8b39a2d1169f tomcat7] > cd ~
[root@8b39a2d1169f ~] > ll -a
total 68
dr-xr-x--- 1 root root 4096 8月  12 09:13 .
drwxr-xr-x 1 root root 4096 8月  12 08:54 ..
-rw------- 1 root root 3415 3月   5 17:36 anaconda-ks.cfg
-rw------- 1 root root 4021 7月  15 14:05 .bash_history
-rw-r--r-- 1 root root   18 12月 29  2013 .bash_logout
-rw-r--r-- 1 root root  176 12月 29  2013 .bash_profile
-rw-r--r-- 1 root root  176 12月 29  2013 .bashrc
drwx------ 3 root root 4096 7月  15 03:08 .cache
-rw-r--r-- 1 root root  100 12月 29  2013 .cshrc
drwxr-xr-x 2 root root 4096 7月  15 03:53 .keras
-rw------- 1 root root  153 7月  17 11:21 .mysql_history
drwxr-xr-x 1 root root 4096 7月  10 02:10 .oracle_jre_usage
drwx------ 2 root root 4096 7月  10 01:32 .ssh
-rw-r--r-- 1 root root  129 12月 29  2013 .tcshrc
drwxr-xr-x 3 root root 4096 7月  15 03:12 .venvs
-rw------- 1 root root 7050 8月  12 09:13 .viminfo
-rw-r--r-- 1 root root    0 7月  11 06:09 测试

# 启动 python 虚拟化环境
[root@8b39a2d1169f ~] > source ~/.venvs/cwtap/bin/activate
(cwtap) [root@8b39a2d1169f ~] > cd /opt/CWTAP
(cwtap) [root@8b39a2d1169f CWTAP] > ll
total 243976
drwxr-xr-x 6 root root      4096 7月   2 11:23 algorithm_implements
drwxr-xr-x 6 root root      4096 6月  28 09:11 algorithm_models
drwxr-xr-x 1 root root      4096 7月  15 11:11 algorithm_result
drwxr-xr-x 5 root root      4096 6月  28 09:11 algorithms
drwxr-xr-x 5 root root      4096 7月   3 06:34 annotate_export_report
drwxr-xr-x 5 root root      4096 6月  28 09:11 annotate_tasks
drwxr-xr-x 6 root root      4096 6月  28 11:41 area_of_jobs
drwxr-xr-x 7 root root      4096 6月  28 09:11 assets
drwxr-xr-x 2 root root      4096 6月  28 09:11 bin
drwxr-xr-x 1 root root      4096 7月  15 11:21 business_types
drwxr-xr-x 4 root root      4096 6月  28 09:11 classify_import
drwxr-xr-x 1 root root      4096 7月  15 11:31 corpus
drwxr-xr-x 1 root root      4096 8月  12 09:13 cwtap
drwxr-xr-x 1 root root      4096 6月  28 12:18 data_import
drwxr-xr-x 5 root root      4096 6月  28 09:11 datasets
drwxr-xr-x 4 root root      4096 6月  28 09:11 functional_tests
drwxr-xr-x 5 root root      4096 6月  28 09:11 import_tasks
drwxr-xr-x 1 root root      4096 6月  28 09:11 intent_import
drwxr-xr-x 7 root root      4096 6月  28 09:11 keywords
drwxr-xr-x 5 root root      4096 6月  28 09:11 knowledge_graphs
drwxr-xr-x 1 root root      4096 7月  15 11:24 labels
drwxr-xr-x 1 root root      4096 7月  17 10:25 logs
-rwxr-xr-x 1 root root       537 6月  28 09:11 manage.py
drwxr-xr-x 5 root root      4096 6月  28 09:11 metas
-rw------- 1 root root    245948 7月  18 09:15 nohup.out
drwxr-xr-x 1 root root      4096 7月  18 09:03 query_result
-rw-r--r-- 1 root root      1157 6月  28 09:11 requirements.txt
drwxr-xr-x 6 root root      4096 6月  28 15:12 rules
drwxr-xr-x 1 root root      4096 7月  17 08:41 sbin
drwxr-xr-x 4 root root      4096 6月  28 09:11 sdks
drwxr-xr-x 1 root root      4096 7月  16 00:58 tasks
drwxr-xr-x 1 root root      4096 6月  28 12:47 tasks_directory
drwxr-xr-x 1 root root      4096 6月  28 10:29 users
drwxr-xr-x 1 root root      4096 6月  28 09:11 webroot
-rw-r--r-- 1 root root 249436592 6月  28 09:11 webroot.tar.gz
-rw-r--r-- 1 root root       387 6月  28 09:11 wsgi.py

# 检查 python 版本
(cwtap) [root@8b39a2d1169f CWTAP] > python -V
Python 3.6.6

# 检查 python 组件
(cwtap) [root@8b39a2d1169f CWTAP] > pip list
Package                  Version   
------------------------ ----------
absl-py                  0.7.0     
alabaster                0.7.12    
astor                    0.7.1     
Babel                    2.6.0     
boto                     2.49.0    
boto3                    1.9.62    
botocore                 1.12.62   
bz2file                  0.98      
certifi                  2018.10.15
chardet                  3.0.4     
colorama                 0.4.1     
coreapi                  2.3.3     
coreschema               0.0.4     
Django                   2.1.2     
django-oauth-toolkit     1.2.0     
djangorestframework      3.9.0     
docutils                 0.14      
drf-yasg                 1.11.0    
gast                     0.2.2     
gensim                   3.6.0     
grpcio                   1.18.0    
h5py                     2.9.0     
idna                     2.7       
imagesize                1.1.0     
inflection               0.3.1     
itypes                   1.1.0     
jieba                    0.39      
Jinja2                   2.10      
jmespath                 0.9.3     
Keras                    2.2.4     
Keras-Applications       1.0.6     
Keras-Preprocessing      1.0.5     
Markdown                 3.0.1     
MarkupSafe               1.1.0     
numpy                    1.15.4    
oauthlib                 2.1.0     
packaging                18.0      
pandas                   0.23.4    
pip                      19.1.1    
pkuseg                   0.0.10    
protobuf                 3.6.1     
Pygments                 2.3.1     
PyMySQL                  0.9.3     
pyparsing                2.3.0     
python-dateutil          2.7.5     
pytz                     2018.6    
PyYAML                   3.13      
requests                 2.20.1    
ruamel.yaml              0.15.77   
s3transfer               0.1.13    
scikit-learn             0.20.2    
scipy                    1.1.0     
setuptools               41.0.1    
six                      1.11.0    
sklearn                  0.0       
smart-open               1.7.1     
snowballstemmer          1.2.1     
Sphinx                   1.8.3     
sphinx-rtd-theme         0.4.2     
sphinxcontrib-websupport 1.1.0     
tensorboard              1.12.2    
tensorflow               1.12.0    
termcolor                1.1.0     
uritemplate              3.0.0     
urllib3                  1.24.1    
Werkzeug                 0.14.1    
wheel                    0.33.4    
xgboost                  0.82  

(cwtap) [root@8b39a2d1169f CWTAP] > nohup python manage.py runserver 0:8000 &
[1] 1881

# 检查
(cwtap) [root@8b39a2d1169f CWTAP] > ps aux | grep python
root      1881  1.5  0.0 156680 38720 pts/0    S    09:31   0:00 python manage.py runserver 0:8000
root      1885 23.1  0.4 4304928 234836 pts/0  Sl   09:31   0:09 /root/.venvs/cwtap/bin/python manage.py runserver 0:8000
root      1936  0.0  0.0  43700  8360 pts/0    S    09:31   0:00 /root/.venvs/cwtap/bin/python -c from multiprocessing.semaphore_tracker import main;main(6)
root      1961  0.0  0.0  12364   984 pts/0    S+   09:32   0:00 grep --color=auto python
```

## 退出容器

```bash
(cwtap) [root@8b39a2d1169f CWTAP] > exit
exit
>
```

## 检查

```bash
# 检查容器服务是否启动成功
> docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                                                                                                                                              NAMES
8b39a2d1169f        3b3ada467561        "/usr/sbin/init"    43 minutes ago      Up 43 minutes       0.0.0.0:822->22/tcp, 0.0.0.0:13306->3306/tcp, 0.0.0.0:17474->7474/tcp, 0.0.0.0:17687->7687/tcp, 0.0.0.0:18000->8000/tcp, 0.0.0.0:18088->8088/tcp   cwtap_poc

# 请求接口地址
> wget http://10.242.1.110:18000/tenant/
--2019-08-12 17:39:30--  http://10.242.1.110:18000/tenant/
正在连接 10.242.1.110:18000... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度：256 [application/json]
正在保存至: “index.html”

100%[============================================================================================================================================================================================>] 256         --.-K/s 用时 0s      

2019-08-12 17:39:30 (64.0 MB/s) - 已保存 “index.html” [256/256])

# 检查请求结果
> cat index.html 
[{"id":1,"name":"中金智汇科技有限责任公司","code":"CWELL","status":1,"type":"人工智能","details":"智能客户经营，智汇服务体验","created":"2018-12-10T14:19:44.167000","modified":"2018-12-10T14:19:44.167000","owner":0,"tenant":0}]
```

## 端口修改

```bash
# 查看现有容器
> docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                                                                                                                                                                                                NAMES
2c7b9fe2b44f        d172d54781c5        "/usr/sbin/init"    5 days ago          Up 5 days           0.0.0.0:822->22/tcp, 0.0.0.0:13306->3306/tcp, 0.0.0.0:18011->7000/tcp, 0.0.0.0:18012->7001/tcp, 0.0.0.0:17474->7474/tcp, 0.0.0.0:17687->7687/tcp, 0.0.0.0:18000->8000/tcp, 0.0.0.0:18088->8088/tcp   cwtap_poc

# 提交修改
> docker commit 2c7b9fe2b44f nlp_v1.3:3.0
sha256:494ea889f589a34317d5115646c6b653b05fee8d4097b9fee87f73a5573d5fd6

# 检查
> docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nlp_v1.3            3.0                 494ea889f589        5 minutes ago       29.8GB
nlp_v1.3            2.0                 d172d54781c5        5 days ago          28.8GB
nlp_v1.3            1.0                 3b3ada467561        5 weeks ago         27.5GB

# 删除现有容器
> docker kill 2c7b9fe2b44f
2c7b9fe2b44f

# 检查
> docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

# 检查所有（在现在的情况下，容器端口还未被释放）
> docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                        PORTS               NAMES
2c7b9fe2b44f        d172d54781c5        "/usr/sbin/init"    5 days ago          Exited (137) 17 seconds ago                       cwtap_poc

# 完全删除
> docker rm 2c7b9fe2b44f
2c7b9fe2b44f

# 检查
> docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

# 启动容器
> docker run --name=cwtap_poc -d -p 8080:7000 -p 13306:3306 -p 18088:8088 -p 18000:8000 -p 822:22 -p 17474:7474 -p 17687:7687 --privileged=true 494ea889f589 /usr/sbin/init
a140e5617d57458de5519a2ab25ee27a725ba3fed8bad62b3f8bcef640b50f61

# 进入容器重新启动任务
```

> **注意：需要重新进入容器启动任务。**
