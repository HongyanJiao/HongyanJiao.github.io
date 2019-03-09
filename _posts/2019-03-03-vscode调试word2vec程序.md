---
layout:     post
title:      vscode调试word2vec程序
subtitle:   Ubuntu 18.04.2 LTS使用vscode对google发布的word2vec程序进行调试
date:       2019-03-03
author:     矫红岩
header-img: img/go-bg.png
catalog: true
tags:
    - c
    - word2vec
---
## ubuntu桌面安装vscode
Ubuntu软件商店下载的vscode不支持中文，在vscode官网下载.deb格式，双击安装即可。
## 配置C环境
vscode添加C/C++扩展：C/C++ IntelliSense, debugging, and code browsing.
![image](https://github.com/HongyanJiao/HongyanJiao.github.io/blob/master/img/cextention.png?raw=true)<br />
## google发布的word2vec程序
[下载地址:http://word2vec.googlecode.com/svn/trunk/](http://word2vec.googlecode.com/svn/trunk/)
## 关于makefile
google官网给出的makefile文件
```
CC = gcc
#Using -Ofast instead of -O3 might result in faster code, but is supported only by newer GCC versions
CFLAGS = -lm -pthread -O3 -march=native -Wall -funroll-loops -Wno-unused-result

all: word2vec word2phrase distance word-analogy compute-accuracy

word2vec : word2vec.c
	$(CC) word2vec.c -o word2vec $(CFLAGS)
word2phrase : word2phrase.c
	$(CC) word2phrase.c -o word2phrase $(CFLAGS)
distance : distance.c
	$(CC) distance.c -o distance $(CFLAGS)
word-analogy : word-analogy.c
	$(CC) word-analogy.c -o word-analogy $(CFLAGS)
compute-accuracy : compute-accuracy.c
	$(CC) compute-accuracy.c -o compute-accuracy $(CFLAGS)
	chmod +x *.sh

clean:
	rm -rf word2vec word2phrase distance word-analogy compute-accuracy
```
makefile文件内容：
1. Project Structure：即工程结构；
2. Instruction for files creation：编译指令；


makefile文件格式：
1. 目标项：word2vec
2. 依赖项：word2vec.c
3. 编译指令：gcc

在终端输入make执行makefile即可
## 配置launch.json
![image](https://github.com/HongyanJiao/HongyanJiao.github.io/blob/master/img/launch.png?raw=true)<br />
vscode打开word2vec.c所在文件夹，选择Debug->Open Configurations，在这里改动launch.json文件，改动三个地方：

1. program：将要调试的程序。<br />
在windows下添加/path/xxx.exe文件，在linux环境下添加目标文件，即makefile中编译word2vec.c生成的word2vec目标文件；
2. args参数：参考demo-word.sh文件或word2vec.c文件main函数的使用说明
```
//demo-word.sh
make
if [ ! -e text8 ]; then
  wget http://mattmahoney.net/dc/text8.zip -O text8.gz
  gzip -d text8.gz -f
fi
time ./word2vec -train text8 -output vectors.bin -cbow 1 -size 200 -window 8 -negative 25 -hs 0 -sample 1e-4 -threads 20 -binary 1 -iter 15
./distance vectors.bin
```

为了测试指定输入输出和debug三个参数；
3. "preLaunchTask": "gcc"，若为.c文件使用gcc，若为.cpp文件使用g++
## F5调试
配置好launch.json文件后可以设置断点，F5进行调试
![image](https://github.com/HongyanJiao/HongyanJiao.github.io/blob/master/img/vscode-debug.png?raw=true)<br />
