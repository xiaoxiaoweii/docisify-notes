# Nginx 热部署完整步骤演示

## 查看 Nginx 状态

```shell
  ps -ef | grep nginx
```

> 输出
>
> ```shell
> root        3079    1836  0 20:49 ?        00:00:00 nginx: master process /usr/sbin/nginx
> nginx       3130    3079  0 20:52 ?        00:00:00 nginx: worker process
> nginx       3131    3079  0 20:52 ?        00:00:00 nginx: worker process
> nginx       3132    3079  0 20:52 ?        00:00:00 nginx: worker process
> nginx       3133    3079  0 20:52 ?        00:00:00 nginx: worker process
> xiaoxia+    3628    2611  0 21:14 pts/0    00:00:00 grep --color=auto nginx
>
> ```

## 查看 Nginx 目录内容

```shell
 cd /opt/nginx
 ll
```

> 输出
>
> ```shell
> drwxr-xr-x. 2 root root    6 10月  8 2019 conf.d
> drwxr-xr-x. 2 root root    6 10月  8 2019 default.d
> -rw-r--r--. 1 root root 1077 10月  8 2019 fastcgi.conf
> -rw-r--r--. 1 root root 1077 10月  8 2019 fastcgi.conf.default
> -rw-r--r--. 1 root root 1007 10月  8 2019 fastcgi_params
> -rw-r--r--. 1 root root 1007 10月  8 2019 fastcgi_params.default
> -rw-r--r--. 1 root root 2837 10月  8 2019 koi-utf
> -rw-r--r--. 1 root root 2223 10月  8 2019 koi-win
> -rw-r--r--. 1 root root 5170 10月  8 2019 mime.types
> -rw-r--r--. 1 root root 5170 10月  8 2019 mime.types.default
> -rw-r--r--. 1 root root 2469 10月  8 2019 nginx.conf
> -rw-r--r--. 1 root root 2656 10月  8 2019 nginx.conf.default
> -rw-r--r--. 1 root root  636 10月  8 2019 scgi_params
> -rw-r--r--. 1 root root  636 10月  8 2019 scgi_params.default
> -rw-r--r--. 1 root root  664 10月  8 2019 uwsgi_params
> -rw-r--r--. 1 root root  664 10月  8 2019 uwsgi_params.default
> -rw-r--r--. 1 root root 3610 10月  8 2019 win-utf
>
> ```

## 查看 Nginx 安装版本以及安装时的编译参数

```shell

```

> 输出
>
> ```shell
> nginx version: nginx/1.14.1 # 版本
> built by gcc 8.2.1 20180905 (Red Hat 8.2.1-3) (GCC)
> built with OpenSSL 1.1.1 FIPS  11 Sep 2018 (running with OpenSSL 1.1.1c FIPS  28 May 2019)
> TLS SNI support enabled
> configure arguments: --prefix=/usr/share/nginx --sbin-path=/usr/sbin/nginx --modules-path=/usr/lib64/nginx/modules --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --http-client-body-temp-path=/var/lib/nginx/tmp/client_body --http-proxy-temp-path=/var/lib/nginx/tmp/proxy --http-fastcgi-temp-path=/var/lib/nginx/tmp/fastcgi --http-uwsgi-temp-path=/var/lib/nginx/tmp/uwsgi --http-scgi-temp-path=/var/lib/nginx/tmp/scgi --pid-path=/run/nginx.pid --lock-path=/run/lock/subsys/nginx --user=nginx --group=nginx --with-file-aio --with-ipv6 --with-http_ssl_module --with-http_v2_module --with-http_realip_module --with-http_addition_module --with-http_xslt_module=dynamic --with-http_image_filter_module=dynamic --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_mp4_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_random_index_module --with-http_secure_link_module --with-http_degradation_module --with-http_slice_module --with-http_stub_status_module --with-http_perl_module=dynamic --with-http_auth_request_module --with-mail=dynamic --with-mail_ssl_module --with-pcre --with-pcre-jit --with-stream=dynamic --with-stream_ssl_module --with-debug --with-cc-opt='-O2 -g -pipe -Wall -Werror=format-security -Wp,-D_FORTIFY_SOURCE=2 -Wp,-D_GLIBCXX_ASSERTIONS -fexceptions -fstack-protector-strong -grecord-gcc-switches -specs=/usr/lib/rpm/redhat/redhat-hardened-cc1 -specs=/usr/lib/rpm/redhat/redhat-annobin-cc1 -m64 -mtune=generic -fasynchronous-unwind-tables -fstack-clash-protection -fcf-protection' --with-ld-opt='-Wl,-z,relro -Wl,-z,now -specs=/usr/lib/rpm/redhat/redhat-hardened-ld -Wl,-E'
> #安装时的配置
> ```

## 备份当前 Nginx 文件并替换

```shell
cp nginx nginx.bak #将nginx文件备份到nginx.bak
```

## 平滑升级

### 查询 Nginx 进程

```shell
  ps -ef | grep nginx
```

> 查到主进程的端口号为 3079

### 启动新版本 Nginx 子进程

```shell
  kill -s SIGUSR2 3079 # 旧版程序的主进程号或进程文件名
```

> 此时旧的 Nginx 主进程将会把自己的进程文件改名为.oldbin，然后执行新版 Nginx。新旧 Nginx 会同时运行，共同处理请求。

> 查询 Nginx 进程状态 新旧进程同时运行
>
> ```shell
> root        3079    1836  0 20:49 ?        00:00:00 nginx: master process /usr/sbin/nginx
> nginx       3130    3079  0 20:52 ?        00:00:00 nginx: worker process
> nginx       3131    3079  0 20:52 ?        00:00:00 nginx: worker process
> nginx       3132    3079  0 20:52 ?        00:00:00 nginx: worker process
> nginx       3133    3079  0 20:52 ?        00:00:00 nginx: worker process
> root        4851    3079  0 22:18 ?        00:00:00 nginx: master process /usr/sbin/nginx
> nginx       4858    4851  0 22:18 ?        00:00:00 nginx: worker process
> nginx       4859    4851  0 22:18 ?        00:00:00 nginx: worker process
> nginx       4860    4851  0 22:18 ?        00:00:00 nginx: worker process
> nginx       4861    4851  0 22:18 ?        00:00:00 nginx: worker process
> xiaoxia+    4869    2611  0 22:19 pts/0    00:00:00 grep --color=auto nginx
> ```

### 停止旧子进程

```shell
  kill -s SIGWINCH 3079
```

> 查询 Nginx 进程状态

> ```shell
> root        3079    1836  0 20:49 ?        00:00:00 nginx: master process /usr/sbin/nginx
> root        4851    3079  0 22:18 ?        00:00:00 nginx: master process /usr/sbin/nginx
> nginx       4858    4851  0 22:18 ?        00:00:00 nginx: worker process
> nginx       4859    4851  0 22:18 ?        00:00:00 nginx: worker process
> nginx       4860    4851  0 22:18 ?        00:00:00 nginx: worker process
> nginx       4861    4851  0 22:18 ?        00:00:00 nginx: worker process
> xiaoxia+    4966    2611  0 22:23 pts/0    00:00:00 grep --color=auto nginx
> ```
>
> 旧子进程退出 不过旧主进程存在

### 停止旧主进程

如果测试新版本 Nginx 没问题则可以退出旧主进程

```shell
 kill -s SIGQUIT 3079 # 旧主进程
```

## 回滚旧版本

如果发现旧版本Nginx有问题可以回滚旧版本

```shell
  kill -s SIGHUP 3079 # 旧主进程 读取旧配置文件 拉起旧的子进程
```