# 实例：培训机构网站开发手记


## 基本设计思路

页面主要分为三类：1) 通知页面；2) 新闻页面；3) 其他页面。

通知页面和新闻页面是通过内容管理系统(CMS)生成的，类似[博客系统](../blog_tutorial.md)。


## 创建项目

    $ mkdir -p ~/workspace/sample/

    $ cd ~/workspace/sample/

    $ padrino g project institution -e erb -c sass -s jquery -d activerecord -b

    $ cd institution/


## 管理后台

    $ padrino g admin

    $ bundle

    $ padrino rake ar:create

    $ padrino rake ar:migrate

    $ padrino rake seed

创建管理员帐号密码。

    $ padrino start -h 0.0.0.0

    $ firefox http://localhost:3000/admin/


## 页面布局

跨PC、手机、平板的网站在开发上具有最优的投入产出比，[Bootstrap](../padrino_bootstrap.md)是最常见的解决方案。

准备工作：

    $ cp /path/to/bootstrap.min.css public/stylesheets/

    $ cp /path/to/bootstrap-theme.min.css public/stylesheets/

    $ cp /path/to/bootstrap.min.js public/javascripts/

    $ cp /path/to/html5shiv.min.js public/javascripts/

    $ cp /path/to/respond.min.js public/javascripts/

    $ cp -r /path/to/fonts/ public/

创建全站页面布局文件：

    $ subl app/views/layouts/application.erb

    $ cp /path/to/logo.jpg public/images/


## 网站首页

    $ subl app/app.rb

    $ subl app/views/index.erb

    $ firefox http://localhost:3000/


## 通知和新闻

对于内容管理系统，最基本元素的是文章、分类和标签。

    $ padrino g model article title:string content:text pubdate:date source:string owner:string category_id:integer

    $ padrino g model category name:string

    $ padrino g model tag name:string

    $ padrino g model association article_id tag_id


    $ subl models/article.rb

    $ subl models/category.rb

    $ subl models/tag.rb

    $ subl models/association.rb

    $ padrino rake ar:migrate


    $ padrino g admin_page article

    $ padrino g admin_page category

    $ padrino g admin_page tag

    $ firefox http://localhost:3000/admin/


    $ padrino g controller articles get:index get:show

    $ padrino g controller categories get:show

    $ subl app/controllers/articles.rb

    $ subl app/views/articles/index.erb

    $ subl app/views/articles/show.erb

    $ subl app/controllers/categories.rb

    $ firefox http://localhost:3000/news/


## 边栏

    $ subl app/views/layouts/_sidebar.erb

    $ subl app/views/layouts/application.erb

    $ subl app/app.rb


## 课程价格

    $ subl app/views/layouts/_price.erb

    $ subl app/views/index.erb

    $ subl public/stylesheets/application.css


## 机构介绍

    $ subl app/views/layouts/_intro.erb

    $ subl app/views/index.erb

    $ subl public/stylesheets/application.css


## 分支机构

    $ subl app/views/layouts/_branch.erb

    $ subl app/views/index.erb


## 图片新闻


## 网站部署


参考[把Padrino应用部署到服务器](https://github.com/chinakr/padrino-note/blob/master/deployment.md)。


## 添加百度统计代码

    $ subl app/views/layouts/application.erb

    $ subl app/views/layouts/_tongji.erb

    $ scp -r app/views/layouts/* user@www.example.com:/var/www/www.example.com/public/


## 百度网站验证

    $ cp ~/Downloads/baidu_verify_xxx.html public/
    $ scp public/baidu_verify_xxx.html user@www.example.com:/var/www/www.example.com/public/


## 添加百度Sitemap

    $ subl public/sitemap.txt

    $ scp public/sitemap.txt user@www.example.com:/var/www/www.example.com/public/