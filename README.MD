### hexo 配置
1.nodeJS环境  
2.npm install -g hexo //全局安装hexo  
3.hexo init     //初始化配置（注意：需要在空目录下初始化）  
4.hexo generate //（hexo g也可以）生成静态页面到public目录  
5.hexo server   //（hexo s）启动服务，http://localhost:4000 访问  
6._config.yml   //配置git发布
```
deploy:
    type: git
    repo: https://github.com/yourname/yourname.github.io.git
    branch: master
```
7.npm install hexo-deployer-git --save  //安装hexo git部署服务  
8.hexo deploy   //（hexo d）执行配置命令  
9.其他

        每次部署的步骤，可按以下三步来进行。
        hexo clean
        hexo generate
        hexo deploy

    一些常用命令：

    hexo new"postName" #新建文章

    hexo new page"pageName" #新建页面

    hexo generate #生成静态页面至public目录

    hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）

    hexo deploy #将.deploy目录部署到GitHub

    hexo help # 查看帮助

    hexo version #查看Hexo的版本

---
配置yilia主题
---
1.$ git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia   //下载主题
2.hexo g , hexo s //打开本地服务调试