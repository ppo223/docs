# 创建python虚拟环境

## 安装virtualenv

```bash
# 切换目录
> cd /opt/xbrain/depolys

# 解压文件
> tar -zxvf virtualenv-16.0.0.tar.gz 
[...]

# 进入安装目录
> cd virtualenv-16.0.0
> ll
total 156
-rw-r--r-- 1 ftpuser games  1224 May 17 07:36 AUTHORS.txt
drwxr-xr-x 2 ftpuser games  4096 May 17 07:36 bin
drwxr-xr-x 2 ftpuser games  4096 May 17 07:36 docs
-rw-r--r-- 1 ftpuser games  1180 May 17 07:36 LICENSE.txt
-rw-r--r-- 1 ftpuser games   345 May 17 07:36 MANIFEST.in
-rw-r--r-- 1 ftpuser games  3240 May 17 07:36 PKG-INFO
-rw-r--r-- 1 ftpuser games  1135 May 17 07:36 README.rst
drwxr-xr-x 2 ftpuser games  4096 May 17 07:36 scripts
-rw-r--r-- 1 ftpuser games    67 May 17 07:36 setup.cfg
-rw-r--r-- 1 ftpuser games  4047 May 17 07:36 setup.py
drwxr-xr-x 2 ftpuser games  4096 May 17 07:36 tests
drwxr-xr-x 2 ftpuser games  4096 May 17 07:36 virtualenv.egg-info
drwxr-xr-x 2 ftpuser games  4096 May 17 07:36 virtualenv_embedded
-rwxr-xr-x 1 ftpuser games 99548 May 17 07:36 virtualenv.py
drwxr-xr-x 2 ftpuser games  4096 May 17 07:36 virtualenv_support

# 执行安装命令
> python3 setup.py install
[...] 
Installing virtualenv script to /usr/local/python3/bin

Installed /usr/local/python3/lib/python3.6/site-packages/virtualenv-16.0.0-py3.6.egg
Processing dependencies for virtualenv==16.0.0
Finished processing dependencies for virtualenv==16.0.0

# 检查安装版本
> virtualenv --version
16.0.0
```

## 创建虚拟化环境

```bash
# 创建虚拟化环境目录
> mkdir ~/.venvs

# 检查
> ll -d ~/.venvs/
drwxr-xr-x 2 root root 4096 Oct 17 11:13 /root/.venvs/

# 创建项目虚拟化环境目录
> mkdir ~/.venvs/xbrain

# 检查
> ll -d ~/.venvs/xbrain/
drwxr-xr-x 2 root root 4096 Oct 17 11:14 /root/.venvs/xbrain/

# 创建虚拟化环境
> virtualenv -p /usr/local/python3/bin/python3 ~/.venvs/xbrain/
Running virtualenv with interpreter /usr/local/python3/bin/python3
Using base prefix '/usr/local/python3'
New python executable in /root/.venvs/xbrain/bin/python3
Also creating executable in /root/.venvs/xbrain/bin/python
Installing setuptools, pip, wheel...done.

# 检查
> source ~/.venvs/xbrain/bin/activate
(xbrain) > python -V
Python 3.6.6

# 退出虚拟化环境
(xbrain) > deactivate
> python -V
Python 2.6.6
```
