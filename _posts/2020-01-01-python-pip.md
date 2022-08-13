---
layout: post
title: Python 切换 pip 镜像源
categories: Python
description: Python 切换 pip 镜像源
keywords: pip
---


## 方法一：临时豆瓣源

使用参数

> -i  https://pypi.doubanio.com/simple/  --trusted-host pypi.doubanio.com 


```
例如：
pip  install django -i  https://pypi.doubanio.com/simple/  --trusted-host pypi.doubanio.com  
```



## 方法二：LInux下永久更换镜像源

```


# python3
cat << EOF > ~/.pip3
[global]
timeout = 6000
index-url = http://pypi.douban.com/simple
trusted-host = pypi.douban.com
EOF

# python2
cat << EOF > ~/.pip
[global]
timeout = 6000
index-url = http://pypi.douban.com/simple
trusted-host = pypi.douban.com
EOF


```

## 方法三：windowns 下永久更换镜像源
[windowns 下永久更换镜像源](https://blog.csdn.net/wls666/article/details/95456309)


