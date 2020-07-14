# 安装地一个 rpm 包 Nginx

> [nginx 中文文档](https://www.nginx.cn/doc/) > [linux 命令在线查询网站](https://www.linuxcool.com/)

## 安装 epel 源

```shell
  yum install epel-release -y
```

> 权限不够可以使用
>
> ```shell
>  sudo yum install epel-release -y
> ```

## 查看可安装的 Nginx 程序包

```shell
  yum list all | grep nginx
```

> 显示 名称 版本 源
>
> ```shell
> collectd-nginx.x86_64              5.9.0-5.el8                                 epel
> munin-nginx.noarch                 2.0.54-2.el8                                epel
> nginx.x86_64                       1:1.14.1-9.module_el8.0.0+184+e34fea82      AppStream
> nginx-all-modules.noarch           1:1.14.1-9.module_el8.0.0+184+e34fea82      AppStream
> nginx-filesystem.noarch            1:1.14.1-9.module_el8.0.0+184+e34fea82      AppStream
> nginx-mod-http-image-filter.x86_64 1:1.14.1-9.module_el8.0.0+184+e34fea82      AppStream
> nginx-mod-http-perl.x86_64         1:1.14.1-9.module_el8.0.0+184+e34fea82      AppStream
> nginx-mod-http-xslt-filter.x86_64  1:1.14.1-9.module_el8.0.0+184+e34fea82      AppStream
> nginx-mod-mail.x86_64              1:1.14.1-9.module_el8.0.0+184+e34fea82      AppStream
> nginx-mod-stream.x86_64            1:1.14.1-9.module_el8.0.0+184+e34fea82      AppStream
> pagure-web-nginx.noarch            5.10.0-11.el8                               epel
> pcp-pmda-nginx.x86_64              5.0.2-5.el8                                 AppStream
> python3-certbot-nginx.noarch       1.5.0-1.el8                                 epel
> ```

## 安装 Nginx

```shell
  yum install nginx -y
```

## 查询安装 Nginx 目录的所有文件

```shell
  rpm -ql nginx
```

> 输出内容
>
> ```shell
> # /etc/  程序的配置文件信息
> /etc/logrotate.d/nginx
> /etc/nginx/fastcgi.conf
> /etc/nginx/fastcgi.conf.default
> /etc/nginx/fastcgi_params
> /etc/nginx/fastcgi_params.default
> /etc/nginx/koi-utf
> /etc/nginx/koi-win
> /etc/nginx/mime.types
> /etc/nginx/mime.types.default
> # /etc/nginx/nginx.conf 主配置文件
> /etc/nginx/nginx.conf
> /etc/nginx/nginx.conf.default
> /etc/nginx/scgi_params
> /etc/nginx/scgi_params.default
> /etc/nginx/uwsgi_params
> /etc/nginx/uwsgi_params.default
> /etc/nginx/win-utf
> # /usr/bin 程序文件
> /usr/bin/nginx-upgrade
> # lib nginx 包以及库文件
> /usr/lib/.build-id
> /usr/lib/.build-id/2d
> /usr/lib/.build-id/2d/da6018ae12edb856ad3d2cf61bf586b6b4873c
> /usr/lib/systemd/system/nginx.service
> /usr/lib64/nginx/modules
> # /usr/sbin 程序文件
> /usr/sbin/nginx
> # /usr/share/doc 帮助文档
> /usr/share/doc/nginx
> /usr/share/doc/nginx/CHANGES
> /usr/share/doc/nginx/README
> /usr/share/doc/nginx/README.dynamic
> /usr/share/licenses/nginx
> /usr/share/licenses/nginx/LICENSE
> /usr/share/man/man3/nginx.3pm.gz
> /usr/share/man/man8/nginx-upgrade.8.gz
> /usr/share/man/man8/nginx.8.gz
> /usr/share/nginx/html/404.html
> /usr/share/nginx/html/50x.html
> /usr/share/nginx/html/index.html
> /usr/share/nginx/html/nginx-logo.png
> /usr/share/nginx/html/poweredby.png
> /usr/share/vim/vimfiles/ftdetect/nginx.vim
> /usr/share/vim/vimfiles/indent/nginx.vim
> /usr/share/vim/vimfiles/syntax/nginx.vim
> /var/lib/nginx
> /var/lib/nginx/tmp
> # /var/log/nginx 放置的就为nginx
> /var/log/nginx
> ```

## 启动 nginx

### 查看主程序目录

```shell
  rpm -ql nginx | grep bin
```

> 输出

```shell
  /usr/bin/nginx-upgrade
  /usr/sbin/nginx # 主程序文件目录
```

### 查看 nginx 帮助

```shell
  /usr/sbin/nginx -h
```

> 输出
>
> ```shell
> nginx version: nginx/1.14.1
> Usage: nginx [-?hvVtTq] [-s signal] [-c filename] [-p prefix] [-g directives] # 中括号都可选
> -?,-h         : this help
>   -v            : show version and exit
>   -V            : show version and configure options then exit
>   -t            : test configuration and exit
>   -T            : test configuration, dump it and exit
>   -q            : suppress non-error messages during configuration testing
>   -s signal     : send signal to a master process: stop, quit, reopen, reload
>   -p prefix     : set prefix path (default: /usr/share/nginx/)
>   -c filename   : set configuration file (default: /etc/nginx/nginx.conf)
>  -g directives : set global directives out of configuration file
> ```

### 查看 80 端口占用情况

```shell
  netstat -tnlp | grep :80
```

> 没有任何提示则没有任何应用占用端口

### 启动 nginx

```shell
 /usr/sbin/nginx
```

### 查看 nginx 运行状态

```shell
  ps -ef | grep nginx
```

> 输出
>
> ```shell
> root       35864    1794  0 23:50 ?        00:00:00 nginx: master process /usr/sbin/nginx #主程序
> nginx      35865   35864  0 23:50 ?        00:00:00 nginx: worker process #子进程 处理用户请求
> nginx      35866   35864  0 23:50 ?        00:00:00 nginx: worker process
> nginx      35867   35864  0 23:50 ?        00:00:00 nginx: worker process
> nginx      35868   35864  0 23:50 ?        00:00:00 nginx: worker process
> xiaoxia+   35885    2553  0 23:51 pts/0    00:00:00 grep --color=auto nginx
> ```

### 杀掉进程

```shell
 kill -9 35864 35865 35866 35867 35868
```

### 指定配置文件执行 nginx

```shell
 /usr/sbin/nginx -c /etc/nginx/nginx.conf
```

## 查看日志文件

```shell
cd /var/log/nginx/
ll
```

> 输出
>
> ```shell
> -rw-r--r--. 1 root root 0 7月  13 23:50 access.log
> -rw-r--r--. 1 root root 0 7月  13 23:50 error.log
> ```

## 网页查看

### 本地 ip 查看

```shell
 ip a
```

> 直接浏览器输入 ip 访问 nginx 默认网页

访问默认网页以后 access.log 中即会存在访问记录
