---
#frontmatter属性示例 详见:https://theme.sugarat.top/config/frontmatter.html
title: GitHub SSH密钥配置   #标题 ,不指定默认去文章的一级标题
description: github SSH密钥配置教程 #描述 text  不指定默认取文章内容前100字
sticky: 2 #用于设置在首页展示的 精选文章，值越大展示越靠前
top: 2 #用于设置在首页置顶展示的文章，从 1 开始，值越小越靠前
recommend: 1 #可用于配置左侧推荐列表数据表现，默认只展示同级目录下的文章
# publish: false #用于控制文章是否发布  等价于hidden: true recommend: false
---


# GitHub密钥配置

## 前言
昨天在搭建个人博客站点时,遇到github推送时出现ssh相关错误,折腾了几个小时才解决,所以在本文记录记录一下解决过程,以便后续再遇到此类问题时可以快速解决

## 错误及解决方法
### 错误
错误提示：`ssh: connect to host github.com port 22: Connection timed out fatal: Could not read from`  连接到主机github.com端口22：连接超时 致命错误：无法读取

### 解决方法
#### 1、检查网络连接
出现此问题先检查网络连接,如果有vpn代理检查一下vpn连接是否正常
#### 2、检查本机ssh配置是否正确
检查本机是否存在密钥

```shell
$ ls ~/.ssh
```

输入检查命令后如果本机存在ssh密钥对 id_rsa (私钥)、id_rsa.pub(公钥)那就代表之前生成过了,可以直接用之前生成过的,不想用可以删除之前的

```shell
$ ls ~/.ssh 
config  id_ed25519      id_rsa      known_hosts
csb/    id_ed25519.pub  id_rsa.pub  known_hosts.old
```

不想使用之前生成的命令可以删除

```shell
$ rm -rf ~/.ssh/id_rsa
$ rm -rf ~/.ssh/id_rsa.pub
```

如果不存在ssh密钥对,需要生成一个

```shell
$ ssh-keygen -t rsa -C "youremail@example.com"
```

```shell
#执行命令,将邮箱换为自己的
$ ssh-keygen -t rsa -C "youremail@example.com"
#执行命令后会弹出以下内容,这里输入回车就行
Enter file in which to save the key (/Users/dengzemiao/.ssh/id_rsa): 
# 输入验证密码，如果不想每次都输入验证密码，则直接回车，不进行输入
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

生成后可以再输入检查命令,检查命令是否存在,存在的话可以执行以下命令复制公钥或者手动打开id_rsa.pub复制
```shell
$ cat ~/.ssh/id_rsa.pub
```

3、检查Github配置
github中打开【设置】-【SSH与GPG公钥】检查github ssh认证密钥是否存在,不存在的话点击新建,将本机生成的ssh 公钥也就是上面复制的公钥粘贴进去
![github ssh配置](./image/ssh.png)

[github ssh配置文档](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)


## 本地存在多个密钥时，如何根据目标平台自动选择用于认证的密钥？
当本地存在多个密钥，如果不设置认证规则，本机将随机选择一个密钥用于认证，可能造成认证失败。

因此，在如下场景中，需要自行定义认证密钥的路径：

本地存在多个密钥对应云效的不同账号。

本地存在多个密钥对应不同的代码平台（GitLab，GitHub，云效等）。

### 定义认证密钥路径规则

打开本地终端，按如下格式编辑~/.ssh/config文件，如 Windows 平台请使用WSL（Windows10或以上）或 Git Bash：

``` bash

# Codeup 示例用户1
HostName codeup.aliyun.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_ed25519
  
# Codeup 示例用户2，设置别名 codeup-user-2
Host codeup-user-2
HostName codeup.aliyun.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/codeup_user_2_ed25519

# GitLab 平台
HostName gitlab.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/gitlab_ed25519

```

按照上述配置，使用SSH协议访问时，SSH 客户端会使用文件指定的密钥进行认证，实现访问不同平台或同一平台的不同账号使用本地不同的 SSH 密钥进行认证。

- 访问 Codeup ，由于 HostName 一致，使用别名进行区分使用不同的密钥。
- 访问 GitLab，根据 HostName 进行区分使用不同的密钥。

```bash
# 访问 Codeup，将使用 ~/.ssh/id_ed25519.pub 密钥
git clone gi*@codeup.aliyun.com:example/repo.com

# 以 codeup-user-2 别名访问 Codeup 时，将使用 ~/.ssh/codeup_user_2_ed25519 密钥 
git clone git@codeup-user-2:example/repo.com

# 访问 GitLab 平台，将使用 ~/.ssh/gitlab_ed25519 密钥
git clone gi*@gitlab.com:example/repo.com
```

## SSH 配置规则

SSH 配置文件（通常是 `.ssh/config`）用于定义连接到不同主机时的设置。以下是一些常见的配置规则和选项：

### 基本格式

```plaintext
Host <alias>
    HostName <hostname>
    User <username>
    Port <port>
    IdentityFile <path_to_private_key>
    PreferredAuthentications <authentication_methods>
```

### 详细说明

1. **Host**: 
   - 用于定义一个连接的别名。
   - 可以使用通配符，例如 `Host *.example.com`。

2. **HostName**:
   - 实际的主机名或 IP 地址。

3. **User**:
   - 登录时使用的用户名。

4. **Port**:
   - SSH 服务的端口号，默认是 `22`。

5. **IdentityFile**:
   - 指定用于认证的私钥文件路径。

6. **PreferredAuthentications**:
   - 指定首选的认证方法，例如 `publickey`。

### 常见配置示例

```plaintext
Host github
    HostName ssh.github.com
    User git
    Port 443
    IdentityFile ~/.ssh/id_rsa
    PreferredAuthentications publickey

Host aliyun
    HostName codeup.aliyun.com
    User your_username
    IdentityFile ~/.ssh/id_ed25519
```

### 其他常用选项

- **ProxyCommand**: 用于通过代理连接。
- **ServerAliveInterval**: 设置保持连接的时间间隔。
- **StrictHostKeyChecking**: 控制是否自动接受新主机的公钥。

### 注意事项

- 确保文件权限设置正确，通常 `.ssh/config` 的权限应为 `600`。
- 使用注释（`#`）来记录配置的目的或说明。

这些规则可以帮助你更好地管理 SSH 连接。如果有任何具体问题，欢迎随时询问！









