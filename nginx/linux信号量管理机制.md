# linux 信号量管理机制

## 列出 linux 所有可用信号量

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

## 常见信号量

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
