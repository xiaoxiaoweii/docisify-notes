# 定制编译安装第一个 Nginx

## 下载 nginx 以及相关资源包

- nginx 全版本下载地址 | [nginx](http://nginx.org/download/) | [搜狐 Nginx 镜像](http://mirrors.sohu.com/nginx/)
- pcre 下载全版本下载地址 | [pcre](ftp://ftp.pcre.org/pub/pcre/) |
- zlib 下载 | [zlib](http://www.zlib.net/)

```shell
  wget http://nginx.org/download/nginx-1.17.2.tar.gz
```

## 解压资源包

```shell
tar xf nginx-1.19.0.tar.gz
tar xf pcre-8.44.tar.gz
tar xf zlib-1.2.11.tar.gz
```

## 查看 nginx 资源包内容

```shell
  ll
```

> 输出
>
> ```shell
> drwxr-xr-x. 6 1001 1001   4096 7月  15 23:49 auto
> -rw-r--r--. 1 1001 1001 303180 5月  26 23:00 CHANGES
> -rw-r--r--. 1 1001 1001 462738 5月  26 23:00 CHANGES.ru
> drwxr-xr-x. 2 1001 1001    168 7月  15 23:49 conf
> -rwxr-xr-x. 1 1001 1001   2502 5月  26 23:00 configure # 脚本文件
> drwxr-xr-x. 4 1001 1001     72 7月  15 23:49 contrib
> drwxr-xr-x. 2 1001 1001     40 7月  15 23:49 html
> -rw-r--r--. 1 1001 1001   1397 5月  26 23:00 LICENSE
> drwxr-xr-x. 2 1001 1001     21 7月  15 23:49 man
> -rw-r--r--. 1 1001 1001     49 5月  26 23:00 README
> drwxr-xr-x. 9 1001 1001     91 7月  15 23:49 src
>
> ```

## 查看 configue 脚本可配置参数内容

```shell
  less configure  # 查看脚本文件 q退出文本查看
```

> 脚本内容
>
> ```shell
> #!/bin/sh
>
> # Copyright (C) Igor Sysoev
> # Copyright (C) Nginx, Inc.
>
>
> LC_ALL=C
> export LC_ALL
>
> . auto/options
> . auto/init
> . auto/sources
>
> test -d $NGX_OBJS || mkdir -p $NGX_OBJS
>
> echo > $NGX_AUTO_HEADERS_H
> echo > $NGX_AUTOCONF_ERR
>
> echo "#define NGX_CONFIGURE \"$NGX_CONFIGURE\"" > $NGX_AUTO_CONFIG_H
>
>
> if [ $NGX_DEBUG = YES ]; then
>     have=NGX_DEBUG . auto/have
> fi
>
>
> if test -z "$NGX_PLATFORM"; then
>     echo "checking for OS"
>
>     NGX_SYSTEM=`uname -s 2>/dev/null`
>     NGX_RELEASE=`uname -r 2>/dev/null`
>     NGX_MACHINE=`uname -m 2>/dev/null`
>
>     echo " + $NGX_SYSTEM $NGX_RELEASE $NGX_MACHINE"
>
>     NGX_PLATFORM="$NGX_SYSTEM:$NGX_RELEASE:$NGX_MACHINE";
>
>     case "$NGX_SYSTEM" in
>         MINGW32_* | MINGW64_* | MSYS_*)
>             NGX_PLATFORM=win32
>         ;;
>     esac
>
> else
>     echo "building for $NGX_PLATFORM"
>
> ```

```shell
  ./configure --help
```

> 输出

> ```shell
> --help                             print this message
>
>   --prefix=PATH                      set installation prefix
>   --sbin-path=PATH                   set nginx binary pathname
>   --modules-path=PATH                set modules path
>   --conf-path=PATH                   set nginx.conf pathname
>   --error-log-path=PATH              set error log pathname
>   --pid-path=PATH                    set nginx.pid pathname
>   --lock-path=PATH                   set nginx.lock pathname
>
>   --user=USER                        set non-privileged user for
>                                      worker processes
>   --group=GROUP                      set non-privileged group for
>                                      worker processes
>
>   --build=NAME                       set build name
>   --builddir=DIR                     set build directory
>
>   --with-select_module               enable select module
>   --without-select_module            disable select module
>   --with-poll_module                 enable poll module
>   --without-poll_module              disable poll module
>
>   --with-threads                     enable thread pool support
>
>   --with-file-aio                    enable file AIO support
>
>   --with-http_ssl_module             enable ngx_http_ssl_module
>   --with-http_v2_module              enable ngx_http_v2_module
>   --with-http_realip_module          enable ngx_http_realip_module
>   --with-http_addition_module        enable ngx_http_addition_module
>   --with-http_xslt_module            enable ngx_http_xslt_module
>   --with-http_xslt_module=dynamic    enable dynamic ngx_http_xslt_module
>   --with-http_image_filter_module    enable ngx_http_image_filter_module
>   --with-http_image_filter_module=dynamic
>                                      enable dynamic ngx_http_image_filter_module
>   --with-http_geoip_module           enable ngx_http_geoip_module
>   --with-http_geoip_module=dynamic   enable dynamic ngx_http_geoip_module
>   --with-http_sub_module             enable ngx_http_sub_module
>   --with-http_dav_module             enable ngx_http_dav_module
>   --with-http_flv_module             enable ngx_http_flv_module
>   --with-http_mp4_module             enable ngx_http_mp4_module
>   --with-http_gunzip_module          enable ngx_http_gunzip_module
>   --with-http_gzip_static_module     enable ngx_http_gzip_static_module
>   --with-http_auth_request_module    enable ngx_http_auth_request_module
>   --with-http_random_index_module    enable ngx_http_random_index_module
>   --with-http_secure_link_module     enable ngx_http_secure_link_module
>   --with-http_degradation_module     enable ngx_http_degradation_module
>   --with-http_slice_module           enable ngx_http_slice_module
>   --with-http_stub_status_module     enable ngx_http_stub_status_module
>
>   --without-http_charset_module      disable ngx_http_charset_module
>   --without-http_gzip_module         disable ngx_http_gzip_module
>   --without-http_ssi_module          disable ngx_http_ssi_module
>   --without-http_userid_module       disable ngx_http_userid_module
>   --without-http_access_module       disable ngx_http_access_module
>   --without-http_auth_basic_module   disable ngx_http_auth_basic_module
>   --without-http_mirror_module       disable ngx_http_mirror_module
>   --without-http_autoindex_module    disable ngx_http_autoindex_module
>   --without-http_geo_module          disable ngx_http_geo_module
>   --without-http_map_module          disable ngx_http_map_module
>   --without-http_split_clients_module disable ngx_http_split_clients_module
>   --without-http_referer_module      disable ngx_http_referer_module
>   --without-http_rewrite_module      disable ngx_http_rewrite_module
>   --without-http_proxy_module        disable ngx_http_proxy_module
>   --without-http_fastcgi_module      disable ngx_http_fastcgi_module
>   --without-http_uwsgi_module        disable ngx_http_uwsgi_module
>   --without-http_scgi_module         disable ngx_http_scgi_module
>   --without-http_grpc_module         disable ngx_http_grpc_module
>   --without-http_memcached_module    disable ngx_http_memcached_module
>   --without-http_limit_conn_module   disable ngx_http_limit_conn_module
>   --without-http_limit_req_module    disable ngx_http_limit_req_module
>   --without-http_empty_gif_module    disable ngx_http_empty_gif_module
>   --without-http_browser_module      disable ngx_http_browser_module
>   --without-http_upstream_hash_module
>                                      disable ngx_http_upstream_hash_module
>   --without-http_upstream_ip_hash_module
>                                      disable ngx_http_upstream_ip_hash_module
>   --without-http_upstream_least_conn_module
>                                      disable ngx_http_upstream_least_conn_module
>   --without-http_upstream_random_module
>                                      disable ngx_http_upstream_random_module
>   --without-http_upstream_keepalive_module
>                                      disable ngx_http_upstream_keepalive_module
>   --without-http_upstream_zone_module
>                                      disable ngx_http_upstream_zone_module
>
>   --with-http_perl_module            enable ngx_http_perl_module
>   --with-http_perl_module=dynamic    enable dynamic ngx_http_perl_module
>   --with-perl_modules_path=PATH      set Perl modules path
>   --with-perl=PATH                   set perl binary pathname
>
>   --http-log-path=PATH               set http access log pathname
>   --http-client-body-temp-path=PATH  set path to store
>                                      http client request body temporary files
>   --http-proxy-temp-path=PATH        set path to store
>                                      http proxy temporary files
>   --http-fastcgi-temp-path=PATH      set path to store
>                                      http fastcgi temporary files
>   --http-uwsgi-temp-path=PATH        set path to store
>                                      http uwsgi temporary files
>   --http-scgi-temp-path=PATH         set path to store
>                                      http scgi temporary files
>
>   --without-http                     disable HTTP server
>   --without-http-cache               disable HTTP cache
>
>   --with-mail                        enable POP3/IMAP4/SMTP proxy module
>   --with-mail=dynamic                enable dynamic POP3/IMAP4/SMTP proxy module
>   --with-mail_ssl_module             enable ngx_mail_ssl_module
>   --without-mail_pop3_module         disable ngx_mail_pop3_module
>   --without-mail_imap_module         disable ngx_mail_imap_module
>   --without-mail_smtp_module         disable ngx_mail_smtp_module
>
>   --with-stream                      enable TCP/UDP proxy module
>   --with-stream=dynamic              enable dynamic TCP/UDP proxy module
>   --with-stream_ssl_module           enable ngx_stream_ssl_module
>   --with-stream_realip_module        enable ngx_stream_realip_module
>   --with-stream_geoip_module         enable ngx_stream_geoip_module
>   --with-stream_geoip_module=dynamic enable dynamic ngx_stream_geoip_module
>   --with-stream_ssl_preread_module   enable ngx_stream_ssl_preread_module
>   --without-stream_limit_conn_module disable ngx_stream_limit_conn_module
>   --without-stream_access_module     disable ngx_stream_access_module
>   --without-stream_geo_module        disable ngx_stream_geo_module
>   --without-stream_map_module        disable ngx_stream_map_module
>   --without-stream_split_clients_module
>                                      disable ngx_stream_split_clients_module
>   --without-stream_return_module     disable ngx_stream_return_module
>   --without-stream_upstream_hash_module
>                                      disable ngx_stream_upstream_hash_module
>   --without-stream_upstream_least_conn_module
>                                      disable ngx_stream_upstream_least_conn_module
>   --without-stream_upstream_random_module
>                                      disable ngx_stream_upstream_random_module
>   --without-stream_upstream_zone_module
>                                      disable ngx_stream_upstream_zone_module
>
>   --with-google_perftools_module     enable ngx_google_perftools_module
>   --with-cpp_test_module             enable ngx_cpp_test_module
>
>   --add-module=PATH                  enable external module
>   --add-dynamic-module=PATH          enable dynamic external module
>
>   --with-compat                      dynamic modules compatibility
>
>   --with-cc=PATH                     set C compiler pathname
>   --with-cpp=PATH                    set C preprocessor pathname
>   --with-cc-opt=OPTIONS              set additional C compiler options
>   --with-ld-opt=OPTIONS              set additional linker options
>   --with-cpu-opt=CPU                 build for the specified CPU, valid values:
>                                      pentium, pentiumpro, pentium3, pentium4,
>                                      athlon, opteron, sparc32, sparc64, ppc64
>
>   --without-pcre                     disable PCRE library usage
>   --with-pcre                        force PCRE library usage
>   --with-pcre=DIR                    set path to PCRE library sources
>   --with-pcre-opt=OPTIONS            set additional build options for PCRE
>   --with-pcre-jit                    build PCRE with JIT compilation support
>
>   --with-zlib=DIR                    set path to zlib library sources
>   --with-zlib-opt=OPTIONS            set additional build options for zlib
>   --with-zlib-asm=CPU                use zlib assembler sources optimized
>                                      for the specified CPU, valid values:
>                                      pentium, pentiumpro
>
>   --with-libatomic                   force libatomic_ops library usage
>   --with-libatomic=DIR               set path to libatomic_ops library sources
>
>   --with-openssl=DIR                 set path to OpenSSL library sources
>   --with-openssl-opt=OPTIONS         set additional build options for OpenSSL
>
>   --with-debug                       enable debug logging
>
> ```

## 编译 Nginx

根据安装内容检查编译环境

```shell
  sudo ./configure --prefix=/opt/nginx --conf-path=/opt/nginx/conf/nginx.conf --user=nginx --group=nginx --pid-path=/opt/nginx/pid/nginx.pid --error-log-path=/opt/nginx/logs/error.log --with-pcre=/usr/sbin/pcre-8.44 --with-zlib=/usr/sbin/zlib-1.2.11 --with-http_ssl_module --with-http_image_filter_module --with-http_stub_status_module --http-log-path=/opt/nginx/logs/access.log
```

> 根据提示结果 缺啥装啥

提示

```shell
the HTTP image filter module requires the GD library.
You can either do not enable the module or install the libraries.
```

安装所需依赖

```shell
sudo install gd gd-devel -y
```

再次检查

> 输出

```shell
onfiguration summary
  + using PCRE library: /usr/sbin/pcre-8.44
  + using system OpenSSL library
  + using zlib library: /usr/sbin/zlib-1.2.11

  nginx path prefix: "/opt/nginx"
  nginx binary file: "/opt/nginx/sbin/nginx"
  nginx modules path: "/opt/nginx/modules"
  nginx configuration prefix: "/opt/nginx/conf"
  nginx configuration file: "/opt/nginx/conf/nginx.conf"
  nginx pid file: "/opt/nginx/pid/nginx.pid"
  nginx error log file: "/opt/nginx/logs/error.log"
  nginx http access log file: "/opt/nginx/logs/access.log"
  nginx http client request body temporary files: "client_body_temp"
  nginx http proxy temporary files: "proxy_temp"
  nginx http fastcgi temporary files: "fastcgi_temp"
  nginx http uwsgi temporary files: "uwsgi_temp"
  nginx http scgi temporary files: "scgi_temp"
```

进行编译

```shell
make # sudo make
```

查看当前文件目录

```shell
ls -rlt
```

> 输出

```shell
-rw-r--r--. 1 1001 1001     49 5月  26 23:00 README
-rw-r--r--. 1 1001 1001   1397 5月  26 23:00 LICENSE
-rwxr-xr-x. 1 1001 1001   2502 5月  26 23:00 configure
-rw-r--r--. 1 1001 1001 462738 5月  26 23:00 CHANGES.ru
-rw-r--r--. 1 1001 1001 303180 5月  26 23:00 CHANGES
drwxr-xr-x. 2 1001 1001     21 7月  15 23:49 man
drwxr-xr-x. 2 1001 1001     40 7月  15 23:49 html
drwxr-xr-x. 9 1001 1001     91 7月  15 23:49 src
drwxr-xr-x. 4 1001 1001     72 7月  15 23:49 contrib
drwxr-xr-x. 2 1001 1001    168 7月  15 23:49 conf
drwxr-xr-x. 6 1001 1001   4096 7月  15 23:49 auto
-rw-r--r--. 1 root root    349 7月  17 22:33 Makefile
drwxr-xr-x. 3 root root    174 7月  17 22:34 objs
```

````shell
vi Makefile #查看Makegfile内容 :q退出

> 输出
```shell
default:        build

clean:
        rm -rf Makefile objs

build:
        $(MAKE) -f objs/Makefile

install:
        $(MAKE) -f objs/Makefile install

modules:
        $(MAKE) -f objs/Makefile modules

upgrade:
        /opt/nginx/sbin/nginx -t

        kill -USR2 `cat /opt/nginx/pid/nginx.pid`
        sleep 1
        test -f /opt/nginx/pid/nginx.pid.oldbin

        kill -QUIT `cat /opt/nginx/pid/nginx.pid.oldbin`
````

安装

```shell
make install # sudo make install
```

安装完成

进入安装目录 查看安装目录文件列表

```shell
cd /opt/nginx/
ll
```

> 输出

```shell
drwxr-xr-x. 2 root root 4096 7月  17 22:43 conf
drwxr-xr-x. 2 root root   40 7月  17 22:43 html
drwxr-xr-x. 2 root root    6 7月  17 22:43 logs
drwxr-xr-x. 2 root root    6 7月  17 22:43 pid
drwxr-xr-x. 2 root root   19 7月  17 22:43 sbin
```

启动 nginx

```shell
sudo /opt/nginx/sbin/nginx # /opt/nginx/sbin/nginx
```

> 报错

```shell
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] still could not bind()
```

查看配置文件

```shell
cd conf/
vim nginx.conf
```

> 输出

```shell
#user  nobody; # 使用nginx用户
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   html;
            index  index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
#
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}

```

[vim 文本编辑器](https://blog.csdn.net/u013008795/article/details/88757927)

修改 nginx.conf 中

> user nginx; # 使用 nginx 用户

尝试启动 nginx 发现还是不行 原因是没有 nginx 用户 要手动创建 nginx 用户
添加 nginx 用户
重新启动 发现成功 nginx

```shell
ps -ef | grep nginx
```

> 输出

```shell
oot       43838   43080  0 23:30 ?        00:00:00 nginx: master process /opt/nginx/sbin/nginx
nginx      43839   43838  0 23:30 ?        00:00:00 nginx: worker process
xiaoxia+   43852   43759  0 23:31 pts/0    00:00:00 grep --color=auto nginx
```

关闭 centos8.0 防火墙

```shell
systemctl stop firewalld
ystemctl disable firewalld
```

```shell
getenforce
```

> 输出

```shell
Enforcing
```

永久关闭 SELinux 修改 selinux 内容

```shell
vim /etc/sysconfig/selinux
```

```shell
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=enforcing # 改为disabled
# SELINUXTYPE= can take one of these three values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted

```

查看编译时的配置参数

```shell
/opt/nginx/sbin/nginx -V
```

> 输出

```shell
nginx version: nginx/1.19.0
built by gcc 8.3.1 20191121 (Red Hat 8.3.1-5) (GCC)
built with OpenSSL 1.1.1c FIPS  28 May 2019
TLS SNI support enabled
configure arguments: --prefix=/opt/nginx --conf-path=/opt/nginx/conf/nginx.conf --user=nginx --group=nginx --pid-path=/opt/nginx/pid/nginx.pid --error-log-path=/opt/nginx/logs/error.log --with-pcre=/usr/sbin/pcre-8.44 --with-zlib=/usr/sbin/zlib-1.2.11 --with-http_ssl_module --with-http_image_filter_module --with-http_stub_status_module --http-log-path=/opt/nginx/logs/access.log
```

检查配置文件语法是否正确

```shell
/opt/nginx/sbin/nginx -t
```
