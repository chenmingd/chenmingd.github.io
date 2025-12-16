---
title: 通过hexo免费在github中自动部署个人网站
date: 2025-12-16 16:24:42
tags:
---
描述如何使用hexo,创建个人博客。如何将个人的博客免费自动的部署在github。

第一步先在本地电脑中安装好hexo

1.本地电脑中需要提前安装好git
2.本地电脑中需要提前安装好nodejs
3.使用npm安装hexo

第二部运行hexo,选择风格，确定自己的博客排面

1.可以到市场中选择自己喜欢的风格。这里我们选择butterfly.butterfly文档全面，好看。
2.使用git直接下载butterfly
3.修改_config.xml中的模版为butterfly
4.将模版中的_config.xml复制一份到_config.xml同级目录中，并将名称修改为_config.butterfly.xml。后续我们所有的hexo页面的配字都可以直接在配置文件中修改
5.安装butterfly的渲染包
6.启动hexo

第三部将hexo部署至github
1:在github中创建一个公开的空仓库
2:删除本地电脑中刚刚生成的hexo文件中所有的.git目录
3:上传hexo到github刚刚新建的空仓库
4:github仓库中选择pages服务，并设置为action触发模式
5:在hexo中创建github action文件
6:再次上传修改的文件到github
6:再githu表中查看action执行情况，执行成功后，就可以直接通过github的域名访问博客了

第四步 小试牛刀，测试自动部署网页的情况
1.在本地电脑使用命令创建一个文档，并添加自己的博客内容
2.使用git将刚刚新建的文档推送至github.等几分钟后就可以在网页中看到新建的页面了
3.修改刚刚的文档，然后再次推送至github.查看页面效果