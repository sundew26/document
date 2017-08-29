新建项目: hexo init <folder>
进入: cd <folder>
安装包: npm install
新建一篇文章: hexo new iOS-APIs (文件会在/source/_posts下)
启动: hexo server
浏览器打开: http://localhost:4000/document/

新加的assert可以放在public下, 访问路径为: /document/assert/

语法手册: http://localhost:4000/document/2017/08/24/Manual/

添加css: 在/public/css/目录下新建new.css供使用, 直接在html中添加css链接不起作用, 需要到/themes/landscape/layout/_partial/head.ejs中的第35行添加```<%-
 css('css/new') %>```


github上部署:
1. 安装 hexo-deployer-git npm install hexo-deployer-git --save
2. _config.yml 中配置
  ```
  # 部署部分的设置
  deploy:
    type: git
    repo: https://github.com/stardew516/document
    branch: master
    message: hexo + css
  ```
3. 终端进入目录 运行 hexo deploy