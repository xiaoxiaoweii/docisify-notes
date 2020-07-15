# Nginx 配置文件重载的原理真相

## reload 重载配置文件的流程

1. 向 master 主进程发送 HUP 信号(reload 命令)
2. master 主进程检查配置语法是否正确
3. master 主进程打开监听端口
4. master 主进程使用新的配置文件启动新的 worker 子进程

> 此时会存在新旧 worker 子进程共存的情况

5. master 主进程向老的 worker 子进程发送 QUIT 信号
6. 旧的 worker 进程关闭监听句柄,处理完当前连接后关闭进程

---

> 整个过程 Nginx 始终处于平稳运行中,实现了平滑升级,用户无感知_
