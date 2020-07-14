# 利用 linux 信号量管理 nginx

## linux 信号量

### linux 所有可用信号量

```shell
 kill -l
```

> 输出

> ```shell
> 1) SIGHUP       2) SIGINT       3) SIGQUIT	    4) SIGILL	      5) SIGTRAP
> 6) SIGABRT	    7) SIGBUS	      8) SIGFPE	      9) SIGKILL	    10) SIGUSR1
> 11) SIGSEGV	    12) SIGUSR2	    13) SIGPIPE	    14) SIGALRM	    15) SIGTERM
> 16) SIGSTKFLT	  17) SIGCHLD	    18) SIGCONT	    19) SIGSTOP	    20) SIGTSTP
> 21) SIGTTIN	    22) SIGTTOU	    23) SIGURG	    24) SIGXCPU	    25) SIGXFSZ
> 26) SIGVTALRM	  27) SIGPROF	    28) SIGWINCH	  29) SIGIO	      30) SIGPWR
> 31) SIGSYS	    34) SIGRTMIN	  35) SIGRTMIN+1	36) SIGRTMIN+2	37) SIGRTMIN+3
> 38) SIGRTMIN+4	39) SIGRTMIN+5	40) SIGRTMIN+6	41) SIGRTMIN+7	42) SIGRTMIN+8
> 43) SIGRTMIN+9	44) SIGRTMIN+10	45) SIGRTMIN+11	46) SIGRTMIN+12	47) SIGRTMIN+13
> 48) SIGRTMIN+14	49) SIGRTMIN+15	50) SIGRTMAX-14	51) SIGRTMAX-13	52) SIGRTMAX-12
> 53) SIGRTMAX-11	54) SIGRTMAX-10	55) SIGRTMAX-9	56) SIGRTMAX-8	57) SIGRTMAX-7
> 58) SIGRTMAX-6	59) SIGRTMAX-5	60) SIGRTMAX-4	61) SIGRTMAX-3	62) SIGRTMAX-2
> 63) SIGRTMAX-1	64) SIGRTMAX
> ```

### 常见信号量

- SIGCHLD 父子进程通信信号量

```shell
    kill -17 $PID
```

- SIGQUIT 等价于 ctrl+\

```shell
    kill -3 $PID
```

- SIGTERM 进程终止信号 允许处理完现有数据再关闭进程

```shell
  kill -15 $PID # -15可以省略
```

- SIGKILL 进程立即被终止

```shell
  kill -9 $PID
```

- SIGHUP

```shell 让进程重读配置文件
  kill -1 $PID
```

- SIGUSR1 | SIGUSR2 用户自定义信号量

```shell
  kill -10 $PID | kill -12 $PID
```

- SIGWINCH 窗口大小改变时发出

```shell
  kill -28 $PID
```

## 使用信号量管理 master 和 worker

### Master 接收信号量

#### 监控 worker 进程

- CHLD 子进程挂了 会强制给 master 进程发送 CHLD 启动新的子进程

#### 管理 worker 进程

- TERM INT

```shell
  kill -s SIGTERM 主进程端口号
```

- QUIT
- HUP

```shell
  kill -s SIGHUP 主进程端口号 #重新读取配置文件
```

- USR1
- USR2
- WINCH

### Worker 接收信号量

> 不推荐直接对 woker 进程进行管理

- TERM INT

```shell
  kill -s SIGTERM 子进程端口号 #虽然子进程被杀掉 不过会生成新的子进程补上
```

- QUIT
- UER1
- WINCH

### 命令行

> 本质同前

- reload: HUP 重读配置文件

```shell
  /usr/sbin/nginx -s reload
```

- reopen: USR1 重新打开日志文件
- stop: TERM 停止 nginx
- quit: QUIT 停止 nginx

> nginx worker process 默认启动的子进程个数与 cpu 线程个数相同 可以在/etc/nginx/nginx.conf 配置文件中修改
>
> ```shell
>  ...................
>   # For more information on configuration, see:
> #   * Official English Documentation: http://nginx.org/en/docs/
> #   * Official Russian Documentation: http://nginx.org/ru/docs/
>
> user nginx;
> worker_processes auto; # 修改为需要的子进程数
> error_log /var/log/nginx/error.log;
> pid /run/nginx.pid;
>
> # Load dynamic modules. See /usr/share/doc/nginx/README.dynamic.
> include /usr/share/nginx/modules/*.conf;
> ..............
> ```
