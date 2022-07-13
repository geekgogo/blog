---
title: "源码安装ngnix并将命令添加systemctl"
date: 2019-06-17T13:54:57+08:00
draft: false
tags: ["linux"]
---
# 编译安装前所需的环境

### 1. gcc安装

> 安装 nginx 需要先将官网下载的源码进行编译，编译依赖 gcc 环境，如果没有 gcc 环境，则需要安装

```
yum install gcc-c++
```

### 2. PCRE pcre-devel 安装

> PCRE(Perl Compatible Regular Expressions) 是一个Perl库，包括 perl 兼容的正则表达式库。nginx 的 http 模块使用 pcre 来解析正则表达式，所以需要在 linux 上安装 pcre 库，pcre-devel 是使用 pcre 开发的一个二次开发库。nginx也需要此库

```
yum install -y pcre pcre-devel
```

### 3. zlib 安装

> zlib 库提供了很多种压缩和解压缩的方式， nginx 使用 zlib 对 http 包的内容进行 gzip ，所以需要在 Centos 上安装 zlib 库

```
yum install -y zlib zlib-devel
```

### 4. OpenSSL 安装 

> OpenSSL 是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及 SSL 协议，并提供丰富的应用程序供测试或其它目的使用。 
nginx 不仅支持 http 协议，还支持 https（即在ssl协议上传输http），所以需要在 Centos 安装 OpenSSL 库

```
yum install -y openssl openssl-devel
```

# 编译安装nginx

### 5. 下载源码nginx

```
wget -c https://nginx.org/download/nginx-1.12.1.tar.gz
```

### 6. 解压编译

> 编译完成后nginx的各种文件路径为/usr/local/nginx

```
tar -xzvf nginx-1.12.1.tar.gz
cd nginx-1.12.1
./configure
make && make install
```

# 将nginx启动和查看版本命令添加到系统中

### 7. 原始启动停止命令

```
/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf  # 启动
/usr/local/nginx/sbin/nginx -s stop  # 停止
```

### 8. 添加到systemctl中

> 在/usr/lib/systemd/system目录下新建nginx.service文件内容如下

```
[Unit]
Description=nginx - high performance web server
Documentation=http://nginx.org/en/docs/
After=network.target remote-fs.target nss-lookup.target
[Service]
Type=forking
PIDFile=/var/run/nginx.pid  # 在nginx配置文件中将pid文件路径改为此处
ExecStartPre=/usr/local/nginx/sbin/nginx -t -c /usr/local/nginx/conf/nginx.conf  # 此处文件路径需与源码安装路径保持一致
ExecStart=/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf  # 同上
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true
[Install]
WantedBy=multi-user.target
```

> 完成后即可使用

```
systemctl start | stop nginx
```

### 9. 将nginx命令添加到系统中

```
cp /usr/local/nginx/sbin/nginx /usr/bin/nginx
```

> 完成后可以使用**nginx -t** 或者 **nginx -V**
