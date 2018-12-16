npm私有仓库搭建
目的： Node.js开发本地项目，有时不同项目之间存在依赖，如果不想把项目发布到npm社区的仓库，则需要有自己本地的仓库。  
构建工具：verdaccio（主流）https://github.com/verdaccio/verdaccio
sinopia是一个用来做npm的registry的私有+缓存镜像的开源组件，但是这个项目现在已经不在维护了，需要移步到verdaccio这个fork。



安装命令：
npm install -g Verdaccio 或者 yarn global add Verdaccio
 
启动：verdaccio
danielwu > NPM私服 > image2018-11-22 10:54:20.png

配置文件路径：/home/.config/verdaccio/config.yaml
修改配置文件，在最后加上一行 “listen: 0.0.0.0:4873”，目的是为了可以从别的机器远程上也能访问verdaccio仓库，修改完成后再次启动verdaccio服务。
用node进程管理工具pm2启动：
pm2 start verdaccio


任意需要从本地NPM仓库进行操作的命令，只需要加入—registry即可
配置了全局的 NPM 库之后，可以省略 --registry 参数；在添加了 .npmrc 配置文件后，在其目录及其子目录下，也可以省略这一参数。以下命令相同，不再进行说明。

注册一个新用户

 npm adduser --registry=http://nexus-oss.lagou.com/repository/npm-hosted/
命令执行后，按照要求输入用户名、密码和邮箱，即可注册成功。注意密码是不显示的，输入完成后回车即可。
登录到服务器
npm login --registry=http://nexus-oss.lagou.com/repository/npm-hosted/

按照提示信息输入完成后，当前控制台窗口即是成功登录的状态。需要注意的是，登录成功的状态只在当前控制台窗口有效。如果需要在另一个窗口中操作，还需要执行一遍登录命令。

发布／更新包
在项目目录下，登录成功后，使用如下命令就可以发布包：

npm publish --registry=http://nexus-oss.lagou.com/repository/npm-hosted/


推荐项目中使用.npmrc 
danielwu > NPM私服 > image2018-11-21 19:11:42.png

官方解释：npm gets its config settings from the command line, environment variables, and npmrc files.

命令行模式会自动设置注册源，方便测试同学，Jinkens管理。

更多 NPM 命令行的参数，可以查看 NPM 官方文档。
