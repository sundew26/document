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
1. 安装 hexo-deployer-git: npm install hexo-deployer-git --save
2. 新建仓库: stardew516.github.io.git
3. _config.yml 中配置
  ```
  # 部署部分的设置
  deploy:
    type: git
    repo: https://github.com/stardew516/stardew516.github.io.git
    branch: master
    message: hexo + css
  ```
4. 生成文件: hexo generate
5. 部署: hexo deploy
6. 访问: https://stardew516.github.io/

注意:
1. 标签比如a标签, 直接尖括号会解析成html, 无法显示, 需要用`&lt;` 和 `&gt;` 代替
2. hexo的博客是按时间顺序排列的,如果想要调整博客的显示顺序,可以在生成页面后修改_post文件夹下的.md文件中的date参数.