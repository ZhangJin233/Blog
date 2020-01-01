---
title: "TensorFlow mac anaconda 安装"
date: 2020-01-01T18:25:45+08:00
author:
  name: "Jane"
comments: true
description: "TensorFlow mac anaconda 安装"
keywords:
images:
tags:
  - TensorFlow
---

#### **环境**####

Mac：MacOS Catalina 10.15.2

anaconda：anaconda3-2019.10

pip:19.0 (如果系统pip小于19，则需要更新至最新)

Python：2.7 

TensorFlow:14.0

#### 安装步骤####

1、下载anaconda3

地址：https://www.anaconda.com/distribution/

安装完成后在终端输入:conda,会显示相关提示

2、更新pip

```
pip install --upgrade pip
```
3、用一下命令在终端新建一个名字叫 tensorflow 的 conda 环境来运行某一版本的 Python
```
conda create -n tensorflow pip python=2.7 
```
4、激活 conda 环境：
```
source activate tensorflow
```

使用conda环境前必须激活环境，激活环境后，命令行会进入已经创建的环境（tensorflow）

5、conda 环境中安装 TensorFlow

```
pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.14.0-py2-none-any.whl

```
本文使用14.0版本TensorFlow，因为14.0版本是1.X版本中最稳定最成熟的版本。

#### 验证安装####

1、以上步骤完成，在TensorFlow环境下输入python,查看Python版本

{{<figure src="/images/tf-python.png" alt="python">}}


2、查看TensorFlow版本

{{<figure src="/images/tf.png" alt="python">}}

#### 关闭环境####
```
conda deactivate
```

#### **遇到的问题**####
在安装到这一步骤时，出现了错误

```
pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.14.0-py2-none-any.whl

```

**错误提示如下：**
```
ERROR:root:code for hash md5 was not found.
Traceback (most recent call last):
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 139, in <module>
    globals()[__func_name] = __get_hash(__func_name)
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 103, in __get_openssl_constructor
    return __get_builtin_constructor(name)
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 91, in __get_builtin_constructor
    raise ValueError('unsupported hash type ' + name)
ValueError: unsupported hash type md5
ERROR:root:code for hash sha1 was not found.
Traceback (most recent call last):
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 139, in <module>
    globals()[__func_name] = __get_hash(__func_name)
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 103, in __get_openssl_constructor
    return __get_builtin_constructor(name)
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 91, in __get_builtin_constructor
    raise ValueError('unsupported hash type ' + name)
ValueError: unsupported hash type sha1
ERROR:root:code for hash sha224 was not found.
Traceback (most recent call last):
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 139, in <module>
    globals()[__func_name] = __get_hash(__func_name)
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 103, in __get_openssl_constructor
    return __get_builtin_constructor(name)
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 91, in __get_builtin_constructor
    raise ValueError('unsupported hash type ' + name)
ValueError: unsupported hash type sha224
ERROR:root:code for hash sha256 was not found.
Traceback (most recent call last):
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 139, in <module>
    globals()[__func_name] = __get_hash(__func_name)
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 103, in __get_openssl_constructor
    return __get_builtin_constructor(name)
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 91, in __get_builtin_constructor
    raise ValueError('unsupported hash type ' + name)
ValueError: unsupported hash type sha256
ERROR:root:code for hash sha384 was not found.
Traceback (most recent call last):
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 139, in <module>
    globals()[__func_name] = __get_hash(__func_name)
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 103, in __get_openssl_constructor
    return __get_builtin_constructor(name)
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 91, in __get_builtin_constructor
    raise ValueError('unsupported hash type ' + name)
ValueError: unsupported hash type sha384
ERROR:root:code for hash sha512 was not found.
Traceback (most recent call last):
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 139, in <module>
    globals()[__func_name] = __get_hash(__func_name)
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 103, in __get_openssl_constructor
    return __get_builtin_constructor(name)
  File "/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/python2.7/hashlib.py", line 91, in __get_builtin_constructor
    raise ValueError('unsupported hash type ' + name)
ValueError: unsupported hash type sha512

```

**解决办法：**
```
brew install openssl
brew link openssl --force
brew uninstall python （卸载后去Python官网重新下载安装Python2.7）
brew install python --with-brewed-openssl
```


详细参见：
https://github.com/Homebrew/legacy-homebrew/issues/22816

#### 参考文章####
1、https://tensorflow.juejin.im/install/install_mac.html

2、https://www.tensorflow.org/install/source
