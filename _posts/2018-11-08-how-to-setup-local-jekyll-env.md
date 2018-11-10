---
layout: post
title:  本地搭建Jekyll环境(win7)
date:   2018-11-08 01:08:00 +0800
categories: document
tag: 教程
---


* content
{:toc}

  一直想做一个自己的博客，后来几多对比之下选用了jekll。暂时使用Github Page把网页跑起来。但是本地环境易于调试，所以就尝试着搭建了jekyll本地环境。
	
  

搭建Jekyll本地环境步骤：

1.搭建ruby环境
------------------------------------


Ruby官网下在地址：[https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/ "Ruby Downloads for Windows")（建议浏览器开始下载后复制下载链接，使用讯雷等下载工具。　并且尽量下载稳定版本.作者下载了 Ruby+Devkit 2.4.5-1 (x64) ）
![](https://i.imgur.com/X1chF3P.png)


本地安装好以后会提示更新MSYS2镜像，一般国内都比较慢，可添加成中科大镜像，后面安装jekyll也比较方便。

目录　＼Ruby24-x64\msys64\etc\pacman.d　下

	mirrorlist.msys文件中将下面镜像地址添加至首行
	Server = http://mirrors.ustc.edu.cn/msys2/msys/$arch/ 

	mirrorlist.mingw64文件中将下面镜像地址添加至首行
	Server = http://mirrors.ustc.edu.cn/msys2/mingw/x86_64/

	mirrorlist.mingw32文件中将下面镜像地址添加至首行
	Server = http://mirrors.ustc.edu.cn/msys2/mingw/i686/
	
Ruby环境搭建好以后cmd窗口输入 ruby -v 检测是否安装成功

![](https://i.imgur.com/viur8Lq.png)



2.安装Jekyll 
------------------------------------


cdm窗口运行 gem install jekyll，
![](https://i.imgur.com/Jpuot7O.png)
    
    
	D:\>gem install jekyll
	Fetching: jekyll-3.8.5.gem (100%)
	Successfully installed jekyll-3.8.5
	Parsing documentation for jekyll-3.8.5
	Installing ri documentation for jekyll-3.8.5
	Done installing documentation for jekyll after 3 seconds
	1 gem installed
	D:\>

由于之前安装过，所以依赖的一些软件基本没有下载，10秒就完成。

安装完成后本地测试 jekyll -v

![](https://i.imgur.com/guvOIvk.png)

	D:\>jekyll -v
	jekyll 3.8.5

	D:\>

3.运行Jekyll 即可启动本地服务
------------------------------------


到jekyll space目录下运行jekyll server
![](https://i.imgur.com/MQ4AU3o.png)

	E:\>cd E:\jekyllWorkspace\LessWords.github.io

	E:\jekyllWorkspace\LessWords.github.io>jekyll server
	Configuration file: E:/jekyllWorkspace/LessWords.github.io/_config.yml
       Deprecation: You appear to have pagination turned on, but you haven't included the `jekyll-paginate` gem. Ensure you have `plugins: [jekyll-pagina
            Source: E:/jekyllWorkspace/LessWords.github.io
       Destination: E:/jekyllWorkspace/LessWords.github.io/_site
 	Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 1.905 seconds.
  	Please add the following to your Gemfile to avoid polling for changes:
    	gem 'wdm', '>= 0.1.0' if Gem.win_platform?
 	Auto-regeneration: enabled for 'E:/jekyllWorkspace/LessWords.github.io'
    Server address: http://127.0.0.1:4000/LessWords.github.io/
  	Server running... press ctrl-c to stop.

 浏览器输入 http://127.0.0.1:4000/LessWords.github.io/ 即可访问本地服务