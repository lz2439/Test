	解决了代码托管和版本控制的问题。

### 一、软件安装：
服务端使用github。
客户端安装方式：
- Windows：[**GitForWindows**](https://gitforwindows.org/index.html)
- Mac 系统安装：[**git-osx-installer**](https://sourceforge.net/projects/git-osx-installer/)
- Linux：在终端输入命令行安装
- Debian 系列：apt-get install git
- Fedora 上：yum install git-core

### 二、链接github
1. 申请github账户。
2. 客户端生成公私钥。
```git
ssh-keygen -t ed25519 -C "你的邮箱地址"
#文件生成在.ssh文件夹下，生成的时候会有目录输出
```
3. 将密钥添加到github。
	1. 将.pub的公钥内容复制出来
	2. 在github主页，点击头像，点击设置，点击ssh and gpg keys，添加ssh公钥即可

### 三、使用方式
```git
git clone url    #克隆后要输入yes，url在项目地址获取，克隆到本地的当前文件夹下
git add .    #添加更新到缓冲区，.代表所有文件，有风险，建议跟文件名
git reset .    #取消缓冲区更新
git status    #查看缓冲区状态

git commit -m test    #写更新备注，后面跟文件，同时要设置邮箱和名称
git config --global user.email "you@example.com"    #设置邮箱
git config --global user.name "Your Name"    #设置名称

git config --global core.autocrlf false    #禁止转换换行符

git pull    #将缓冲区推送到github

```

