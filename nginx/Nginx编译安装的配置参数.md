# Nginx 编译安装的配置参数

## 常用配置参数

|       参数       |                 含义                 |
| :--------------: | :----------------------------------: |
|     --prefix     |             指定安装目录             |
|      --user      |  运行 nginx 的 worker 子进程的属主   |
|     --group      |  运行 nginx 的 worker 子进程的属组   |
|    --pid-path    |     存放进程运行 pid 文件的路径      |
|   --conf-path    |    配置文件 nginx.conf 的存放路径    |
| --error-log-path |    错误日志 error.log 的存放路径     |
| --http-log-path  |    访问日志 access.log 的存放路径    |
|   --with-pcre    | pcre 库的存放路径 正则表达式可以用到 |
|   --with-zlib    |  zlib 库的存放路径 gzip 模块会用到   |

## 内置参数默认原则

- 显示加上 默认不内置 --with
- 显示去掉，默认内置 --without
