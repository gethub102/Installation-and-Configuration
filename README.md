## 记录一些配置安装的流程，以及遇到的问题和解决方法（Ubuntu)

# 目录

 1. [Shadowsocks服务端 Ubuntu 14.04][1]
 2. [安装配置virtualenv][2]
 3. [Git使用方法][3]
 4. [在Github Pages上部署Hexo][4]
 
# Shadowsocks服务端 Ubuntu 14.04

  1.通过pip安装shadowsocks
  > apt-get install pip
  >
  > pip install shadowsocks
 
  2.新建shadowsocks配置文件
  
  >vi shadowsocks.json
  
  ```
  { 
  "server":"vps的ip", 
  "server_port":2333, #服务器端口，与SSH端口不一样，最好大于1024
  "local_port":1080, 
  "password":"barfoo!", #认证密码 
  "timeout":60, "method":
  "aes-256-cfb" #加密方式，推荐使用aes-256-cfb
  }
  ```
  >ssserver -c shadowsocks.json -d start
  
  除了编写这份文档外没有遇到什么问题....<br>
  顺便推荐一篇不错的文档：[ShadowSocks（影梭）不完全指南](http://www.auooo.com/2015/06/26/shadowsocks%EF%BC%88%E5%BD%B1%E6%A2%AD%EF%BC%89%E4%B8%8D%E5%AE%8C%E5%85%A8%E6%8C%87%E5%8D%97/)

  [*返回目录*](#目录)
  
# 安装配置virtualenv

  1.分别安装pip/pip3
  >apt-get install python-pip<br>
  >apt-get install python3-pip
  
  2.安装virtualenv
  >pip install virtualenv<br>
  >pip3 install virtualenv
  
  3.创建环境
  >virtualenv --no-site-packages --python=python3 test
  
  --no-site-packages 不安装第三方包 --python=x 指定版本
  
  4.激活&退出
  >source test/bin/acitve<br>
  >deactivate   //退出环境
  
  5.其他命令
  >which python<br>
  >which pip<br>
  >virtualenv --distribute  //??
  
  参考文档：
  >[virtualenv -廖雪峰](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001432712108300322c61f256c74803b43bfd65c6f8d0d0000)
  >[用virtualenv建立多个Python独立开发环境](http://www.nowamagic.net/academy/detail/1330228)<br>
  >[virtualenv官方文档](http://virtualenv-chinese-docs.readthedocs.io/en/latest/#id29)
  
  [*返回目录*](#目录)
  
# Git使用方法

  创建仓库：
  >mkdir test<br>
  >cd test<br>
  >git init
  
  添加文件：
  >git add test1.txt test2.txt<br>
  >git commit -m "add 2 txt files."
  
  相关命令：
  >git status<br>
  >git diff test1.txt //查看修改内容
  
  版本回退：
  >git log  //查看提交记录<br>
  >git reset --hard HEAD^
  
  上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100
  
  关联远程库：
  >git remote add origin git@server-name:path/repo-name.git
  
  推送：
  >git push -u origin master  //-u:首次推送master分支的所有内容
  
  参考文档：[Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
  
  [*返回目录*](#目录)
  
# 在Github Pages上部署Hexo

  1.安装nodejs，npm
  
  在腾讯云上试了很久都没有搞定，最后换成美国的VPS才安装成功，原因大家都明白。。
  
  >git clone https://github.com/nodejs/node.git   //用源码安装node花了很长时间，没试过apt-get<br>
  >chmod -R 755 node<br>
  >cd node<br>
  >sudo ./configure<br>
  >sudo make<br>
  >sudo make install  //安装完 node --version
  
  >sudo apt-get install npm
    
  参考文档：[Node.js 安装配置](http://www.runoob.com/nodejs/nodejs-install-setup.html)
  
  2.安装Hexo
  
  >npm install -g hexo<br>
  >hexo init  //新建一个目录后在里面操作<br>
  >hexo g   //生成页面内容<br>
  >hexo s   //执行后可在4000端口预览
  
  3.部署到Github
    
   [Github SSH密钥](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374385852170d9c7adf13c30429b9660d0eb689dd43a000)
     
   修改config.yml配置文件，注意冒号后面有空格
   ```
   # Deployment
   ## Docs: https://hexo.io/docs/deployment.html
   deploy:
   type: git
   repository: git@github.com:Orenoid/orenoid.github.io.git
   branch: master
   ```

   为Hexo安装Git插件
   >npm install hexo-deployer-git --save
   
   部署到Github上
   >hexo deploy    //或 hexo d
    
  4.vim，putty不支持中文
  
  解决方法:<br>
  [ubuntu vim中文乱码问题](http://blog.sina.com.cn/s/blog_45bcb4c30100x0lj.html)<br>
  [putty如何支持中文](https://zhidao.baidu.com/question/495083997.html)
  
  [*返回目录*](#目录)

[1]: #shadowsocks服务端-ubuntu-1404
[2]: #安装配置virtualenv
[3]: #git使用方法
[4]: #在github-pages上部署hexo
