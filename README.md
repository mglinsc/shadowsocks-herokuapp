到目前还能用，us比eu的要快，本人PC系统是opensuse,配合privoxy可以实现全局代理，手机为安卓6.0,也可以配合privoxy,然后设置wifi代理，或者设置手机网络的接受点（APN），同样也可以实现全局代理，一定要先运行node项目,再运行privoxy.

shadowsocks-heroku
==================

shadowsocks-heroku is a lightweight tunnel proxy which can help you get through firewalls. It is a port of [shadowsocks](https://github.com/clowwindy/shadowsocks), but through a different protocol.

shadowsocks-heroku uses WebSocket instead of raw sockets, so it can be deployed on [Heroku](https://www.heroku.com/).

Notice that the protocol is INCOMPATIBLE with the origin shadowsocks.

## Windows下运行环境的准备
**安装git** [Git installation](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)  
  根据系统版本选择Git安装包下载并安装  
**安装Heroku CLI** [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)  
  根据系统版本选择Heroku CLI安装包下载并安装  
**安装Nodejs**  [Node.js官网](https://nodejs.org/)  
  根据系统版本选择下载[Nodejs安装包](https://nodejs.org/en/download/)  
	*在Windows上安装时务必选择全部组件*  
	

Heroku
------

### Usage

```
首先将本项目下载(通过Clone or download选择Download Zip下载到本地)并解压(假如解压到E:\shadowsocks-herokuapp)
cd shadowsocks-herokuapp    //打开命令提示符，进入项目目录
本地上传
heroku login  //登录你的heroku账号，执行后在打开的网页上登录帐号，登录成功后命令提示符窗口显示: Logged in as XXX(XXX为你的Heroku帐号)  
heroku create  yourappname  //或者直接在heroku 的网页后台创建app
git init   //初始化本地版本库
heroku git:remote -a yourappname
git add .
git config --global user.email "you@example.com" //配置git 邮箱(Heroku帐号)
git config --global user.name "Your Name"        //配置git 用户名(Heroku帐号)
git commit -am "make it better"  //如果未提示"Please tell me who you are" 则前两步配置git邮箱、用户名的步骤可不做
git push heroku master
heroku config:set METHOD=rc4 KEY=password    //配置加密方式和密码

Supported Ciphers //支持以下几种加密方式
-----------------

- rc4
- rc4-md5
- table
- bf-cfb
- des-cfb
- rc2-cfb
- idea-cfb
- seed-cfb
- cast5-cfb
- aes-128-cfb
- aes-192-cfb
- aes-256-cfb
- camellia-256-cfb
- camellia-192-cfb
- camellia-128-cfb

在开始菜单中打开"Node.js command prompt"，而后继续执行下列命令：
npm install //本地安装Node模块(第一次时运行，安装后不用再运行)
node local.js -s yorappname.herokuapp.com -l 1080 -m rc4 -k password -r 80
server listening at { address: '127.0.0.1', family: 'IPv4', port: 1080 }
```

浏览器代理设置Change proxy settings of your browser into:

```
SOCKS5 127.0.0.1:1080
```

### Troubleshooting

If there is something wrong, you can check the logs by:

```
$ heroku logs -t --app yourappname
```

