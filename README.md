通过docker来快速编译安装 viabtc_exchange 
同时安装nginx解决websocket连接问题（很多人好像卡在这里）
然后之前有些人发布的版本有些问题，做了fixed


如何安装本项目？
首先你需要一个Ubuntu的环境，我这里直接拿来一个服务器

如果你安装了docker和docker-compose，直接执行以下命令，如果没有请看下文的如何安装docker:
#安装 git（有了就跳过）
sudo apt install git
#clone代码
git clone https://github.com/TaylorWenOne/viabtc_exchange_server_docker_with_nginx.git
#移动到下载目录
cd viabtc_exchange_server_docker_with_nginx
#安装本项目
docker-compose up &

然后进入较长的全自动编译安装过程...
部分人会出现java版本出错的提示，是因为本机的openjava版本号和kafka中的dockerfile的要求版本号不一样导致，修改kafka下的dockerfike改成本机有的java版本号即可

启动成功后，回车
执行查看docker各容器进程
docker ps  
#可以看到,nginx对外监听的是8008端口，然后把请求转发给unix的套接字,http对外暴露的接口是18080端口
这里有需要注意的是，如果你使用的是阿里云服务器或者亚马逊aws，可能会受安全策略影响导致websocket无法工作，解决办法是
登录到你服务器的控制台，在安全策略上放开nginx的监听端口和http监听端口，或者执行ufw在防火墙上放开端口（我这里分别用的是8008和18080）！！

#测试(http在本机)
curl  http://127.0.0.1:18080/ -d '{"method": "market.list", "params": [], "id": 1516681174}'
#测试(ws，可以建立一个js的ws客户端来测试，我是通过一个前端代码来访问的)
ws://机器公网ip:80008

共同讨论？
1.建个QQ群吧：
2.我的QQ：284726777
3.微信群还没开，图片不知道怎么贴上来，原谅我，我也是个菜鸟

其他问题？
1.常见的问题有accessws下的confi.json的auth_url和sign_url是干嘛，这两个主要是用账户授权（不影响via的服务启动），当你建立一个真正拥有账户体系的交易所时（via只是个撮合引擎，完整的交易所还需要前端程序），账户信息需要授权用得上，账户通过via交易挂单、余额等需要token令牌的授权








如何安装docker？

#如果有老版本自带的docker删掉，执行
sudo apt-get remove docker docker-engine docker.io containerd runc

sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
    
#添加Docker的官方GPG密钥（返回ok，说明正常）：
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
#执行
sudo apt-key fingerprint 0EBFCD88
#添加apt下载docker的依赖源（使用x86、amd64）
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
 #更新  
 sudo apt-get update
 #安装CE
 sudo apt-get install docker-ce docker-ce-cli containerd.
 #运行测试，看见docker  hello的显示即安装成功
 sudo docker run hello-world
 
 #开始安装docer-comose
 sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
 #给与可执行的权限
 sudo chmod +x /usr/local/bin/docker-compose
 #测试，成功出现版本号，则准备开始安装本项目
 docker-compose --version
 
