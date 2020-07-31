# pip 使用国内镜像源

## 国内源

- 清华 https://pypi.tuna.tsinghua.edu.cn/simple
- 阿里云 http://mirrors.aliyun.com/pypi/simple/
- 中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/
- 华中理工大学 http://pypi.hustunique.com/
- 山东理工大学 http://pypi.sdutlinux.org/
- 豆瓣 http://pypi.douban.com/simple/

## 临时使用

- 使用 pip 的时候加参数 -i 源

```shell
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pyspider
```

## 永久修改

windows 下，在 user 目录中创建一个 pip 目录，如：C:\Users\xx\pip，新建文件 pip.ini。

内容

> [global]
> index-url = https://pypi.tuna.tsinghua.edu.cn/simple >[install]
> trusted-host=mirrors.aliyun.com
