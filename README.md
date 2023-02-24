# OpenAI ChatGPT接入微信 wechatbot 搭建微信聊天机器人

## 一、准备工作
### 首先是注册ChatGPT， [点此进入注册ChatGPT的视频教程](https://youtu.be/SA5HJxtfHZE)

- 1、获取自己 ChatGPT 的 apikey [获取地址](https://platform.openai.com/account/api-keys) 登入后即可获取

- 2、一台VPS境外服务器（本次演示系统 Debian 10 64）

[Vultr 购买地址，点此进入](https://www.vultr.com/?ref=8941832-8H)：按时计费，最低6$/月。

- 3、一个微信号（建议使用小号测试）

- 4、下载并安装FinalShell SSH工具

Windows版下载地址:[点此下载](http://www.hostbuf.com/downloads/finalshell_install.exe)

macOS版下载地址: [点此下载](http://www.hostbuf.com/downloads/finalshell_install.pkg)


## 二、ChatGPT接入微信

### 开始配置服务器

安装 Node 环境

    sudo apt update && sudo apt upgrade
    
    curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
    
    sudo apt-get install nodejs

安装<code>git</code>命令

    apt install git
    
克隆 Wechat-Chatgpt 项目[点此进入项目地址](https://github.com/fuergaosi233/wechat-chatgpt)

    git clone https://github.com/fuergaosi233/wechat-chatgpt.git
    
### 安装依赖并创建配置文件

切换到new-wechatgpt分支

    git checkout new-wechatgpt


安装依赖

    npm install


创建配置文件

    cp .env.example .env


修改配置文件：API = 就是你在openAI官网上生成的apikey

.env内容如下：

    CHAT_GPT_EMAIL=
    CHAT_GPT_PASSWORD=
    CHAT_GPT_RETRY_TIMES=
    CHAT_PRIVATE_TRIGGER_KEYWORD=
    OPENAI_PROXY=
    NOPECHA_KEY=
    CAPTCHA_TOKEN=
    OPENAI_API_KEY=填写你的API_KEY


修改模型

打开文件：

    cd wechat-chatgpt

找到73行，修改模型为：

    text-davinci-003


### 保存好配置文件后，启动执行下方的启动命令，就可以和机器人聊天了！

    npm run dev


### 如果需要在后台守护进程运行，那么只需运行下面命令

    apt-get install screen

    screen -S chatgpt

运行以后再运行之前的命令就可以了，

启动成功后，按Ctrl +A+D 即可挂起后台服务。

想看运行情况

    screen -R chatgpt

就可以查看了~

这样即使你断开VPS，机器人也会在后台运行。

具体的设置教程：
