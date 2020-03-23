# MakeThings-team.blog
MakeThings-team blog Source Code.



## 加入我们

编辑您的**github用户名**和**github邮箱**以及您的**ssh public key**发送到xcc.int3@gmail.com以便邀请您加入我们的组织。



## 准备

- [**nodejs**](https://nodejs.org/en/)：建议下载最新的LTS版
- [**git**](https://git-scm.com/)：建议下载最新版
- **ssh public key**：使用`ssh-keygen`生成或其他方式生成



## 部署

### 安装Hexo

安装好nodejs之后执行以下命令将会在全局npm模块中安装`hexo`命令

```bat
# 配置npm全局代理，也可以手动编辑C:\Users\你的用户名\.npmrc
> npm config set proxy=http://127.0.0.1:10088
> npm config set https-proxy=http://127.0.0.1:10088

# 安装hexo命令到你的系统中
> npm install hexo-cli -g

# 查询hexo命令是否安装成功
> where hexo
# 以下内容将被输出
C:\Users\Administrator\AppData\Roaming\npm\hexo
C:\Users\Administrator\AppData\Roaming\npm\hexo.cmd
```



### 下载博客源码并初始化

```bat
# 配置git全局代理
> git config --global http.proxy http://127.0.0.1:10088
> git config --global https.proxy http://127.0.0.1:10088

# clone仓库并初始化
> git clone https://github.com/MakeThings-team/MakeThings-team.blog.git
> cd MakeThings-team.blog
> git config user.name "你的用户名"
> git config user.email "你的邮箱"
> git submodule init & git submodule update
> npm install

# 启动hexo服务
> hexo s
```



### 发布新帖子

新帖子不建议使用中文名称，将在删除它时带来麻烦

```bat
> cd MakeThings-team.blog

# 将创建"source/_posts/newPost.md"文件 和 "source/_posts/newPost"文件夹
# 文件夹中存放该帖子引用的资源文件，例如图片等等
> hexo new "newPost"
```



### 上传帖子源码并部署帖子，以显示在网站上

以下命令需要登陆您的github账号并且`hexo d`命令需要认证您的`ssh public key`，可以联系xcc.int3@gmail.com以认证您的`ssh public key`

```bat
> cd MakeThings-team.blog

# --global选项是必须的，也可以手动编辑C:\Users\你的用户名\.gitconfig
> git config --global user.name "你的名字"
> git config --global user.email "你的邮箱"

# 同步到博客源码仓库中
> git add source\_posts\newPost source\_posts\newPost.md
> git commit -m "add a new post."
> git push

# 清除缓存
> hexo clean
> rm -rf .deploy_git

# 同步到博客网站仓库中
> hexo g
> hexo d
```



### 删除帖子

```bat
> cd MakeThings-team.blog

> git rm -r source\_posts\newPost
> git rm source\_posts\newPost.md

> git add source\_posts\newPost source\_posts\newPost.md
> git commit -m "delete a post."
> git push

# 清除缓存
> hexo clean
> rm -rf .deploy_git

# 重新部署
> hexo g
> hexo d
```



### 选择是否需要删除npm和git全局代理

```bat
# 删除git全局代理
> git config  --global --unset http.proxy
> git config  --global --unset https.proxy

# 删除npm全局代理
> npm config delete proxy
> npm config delete https-proxy
```