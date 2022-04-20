---
title: "使用jekyll依托github page搭建自己的博客"
categories: 
    - 博客搭建
tags:
    - jekyll
    - github page
author_profile: true
---

现在你正在看的这个博客就是使用jekyll搭建在github page上的，并且使用了mmistake主题。下面我将以下几个方面进行简单的介绍。

- 这个无序列表会被替换成目录
{:toc}

## 前置知识

本博客默认您了解以下内容

- HTML（知道是什么就行）
- MarkDown（至少能熟练编写）
- Git（会add,commit,clone,pull,push就可以）
- Github（有一个Github账户，并有能稳定访问Github的网络环境）

## 为什么使用jekyll加github page

首先，网页分为静态网页和动态网页，因为博主不是计算机/软件专业的，所以具体的区别就不详细叙述，大家网上随便一搜就能找到[^1]，不需要我班门弄斧了。对应的，搭建自己的博客也就分为了动态博客与静态博客，也对应了不同的搭建工具，它们都能大幅的简化我们简历博客的流程，让小白也能建立自己的博客。

静态博客常用的主要有[jekyll](http://jekyllcn.com/)，[hexo](https://hexo.io/zh-cn/index.html)，[hugo](https://www.gohugo.org/)等，网上也能找到对应的优缺点对比，就不再赘述。

动态博客用的比较多的应该是WordPress，但是需要注意的是，使用动态博客必须有一个自己的服务器，并且最好有一个域名，所以成本自然就上去了。

经过多方比较和综合考虑，我先是决定了使用静态博客搭配Github Page（因为我的云服务器和域名还有几个月就过期了），又因为jekyll与Github Page的搭配是最好的（Github Page好像就是基于jekyll的），所以我最终选择了使用jekyll。

~~需要注意的一点是jekyll是基于ruby的，但是据说ruby对于windows的支持并不十分良好，但是没有linux经验的同学也不要担心，如果你只是想搭建一个在线博客，并不需要在本地搭建环境，所以完全不会linux也是没有问题。~~
经过亲自测试，现在在window下安装ruby进对于使用jekyll来说，已经非常简单（甚至比linux还简单），根据官方文档[^2]进行安装即可，注意要有比较好的网络环境（你懂的）

## Github Page 的相关设置

我对这一部分也不是特别的熟悉，只能简单的说一下对应的过程，其背后的原理就不清楚了。

1. 在自己Github账号中新建一个名为username.github.io的空仓库。
2. 在仓库的sitting中选择github page。![图片具体]({{ site.url }}{{ site.baseurl }}/assets/images/posts/2022-04-19/Snipaste_2022-04-20_00-41-46.png)
3. 将这个仓库克隆下来，备用。
4. 【*可选* 】 写一个index.html，push上去，访问 `https://username.github.io` （username是你的GitHub用户名），看看是不是对应的index.html的内容。

## jekyll的相关知识

本质上jekyll就是一个转换器，将你写的markdown文件转化成HTML，并加上对应的主题等等，实现一个静态的博客，同时你也可以添加一些插件来实现各种功能。

jekyll的相关知识通过其官方文档[^2]就可以完全掌握，如果在我学习过程中没有遇到问题则不会对其进行过多的讲解，官方的中文文档已经足够清晰。

> **如果只想写博客，并不想了解更多，或者相应的专业知识比较少，文档的内容可以只看[欢迎](http://jekyllcn.com/docs/home/)和[目录结果](http://jekyllcn.com/docs/structure/)部分。**

### 开始
{:.no_toc}

#### 快速指南
{:.no_toc}

***建议不要跟着这个部分走，可以直接略过***

#### 安装
{:.no_toc}

安装部分中的“事前要求”部分可能是整个流程中最困难的，中间遇到了一些问题，记录如下。

1. ruby的安装（使用linux系统，虚拟机或者双系统都无所谓）
   - 如果使用的是Ubuntu系统，那么系统是自带ruby的，不知道为啥在接下来的步骤中会有问题，在[这里](https://stackoverflow.com/questions/37720892/you-dont-have-write-permissions-for-the-var-lib-gems-2-3-0-directory)找到了解决方案。
   - 但是需要注意的是，这个答案已经比较老了，不要直接运行 ` rbenv install 2.3.1 ` ，版本太老。当前对应最新的ruby版本可以通过运行 `rbenv install -l` 查看。
2. 在现在的版本中，RubyGems已经自带在Ruby中了，不需要独立安装
3. Nodejs在Ubuntu中可以直接使用 ` apt install nodejs ` 进行安装
4. Python直接ubuntu自带
5. 最后直接 `gem install jekyll` 就行

#### 基本用法
{:.no_toc}

这个时候你其实已经可以把自己的仓库初始化成一个博客，push上去看一下有没有效果，github会自动的进行build（所以你其实完全可以不在本地配置jekyll）。注意可以在仓库的Actions中看到对应的构建过程，如果出错，可以根据出错信息进行排查。

> 如果你看了其他的一些教程，你会发现他们可能使用的指令是 `bundle exec jekyll serve`，与官网的有些不同。这是使用了bundle，可能是用来保证gem包的版本不出问题（博主没有接触过ruby，不是十分理解），总之用 `bundle exec jekyll serve` 应该是更好的，不过要配合gemfile使用。

#### 目录结构
{:.no_toc}

重点如下

- _config.yml：是你配置这个博客的一些基本信息的地方
- _post文件夹：是放你的博文的地方

其他的地方暂时不理解没关系，看到后面会更加理解；如果到后面还不理解，也没关系，照样可以写博客。

#### 配置
{:.no_toc}

这里完全看不懂也没关系，不影响使用。

### 博客内容
{:.no_toc}

> 建议先阅读，“撰写博客”，“使用草稿”，“创建页面”这三个部分，其他的部分可以选读，不看也问题不大，遇到问题在来看也可以。

***之后的部分如果不想深入了解jekyll，其实没太大必要继续读，但是读了也许可以帮助你解决很多问题。***

## 找到一个喜欢的主题

现在你已经可以使用默认的模板写一些博文了，但是我们自建博客，肯定是希望能够漂漂亮亮，与众不同的博客，所以我们需要寻找一个好看的主题。

可以通过 [http://jekyllthemes.org/](http://jekyllthemes.org/) 查看自己喜欢的主题，也可以直接在GitHub或者其他地方自己寻找。

## 使用jekyll搭配Github Page最简单的方法

1. 直接下载对应主题的zip包，或者下载他的Github Page的对应仓库sername/username.github.io，解压到自己的对应位置。
2. 将_config.yml中的信息内容全部改成自己的对应信息
3. 将_post文件夹中的其他人的博客全部删掉
4. 【可选】删掉/修改不需要的README.md，doc文件夹，test文件夹等
5. 在_post文件夹中写博客就行了，具体方法参考[jekyll文档的撰写博客](http://jekyllcn.com/docs/posts/)部分。
6. 写完push到自己的GithubPage对应仓库。

## 总结

到此，我们已经基本了解了jekyll和对应的GithubPage配置方法，可以开始愉快的写博文了，但是我们还是只能使用他人的主题模板，并且对jekyll只有一个浅层的理解。如果想要对主题进行定制或者魔改，则需要对jekyll有更深入的了解。

下一篇博文我将会以[minimal-mistakes](https://mmistakes.github.io/minimal-mistakes/)这个主题为例，介绍一下如何对主题进行定制，同时更加深入的了解jekyll的一些配置和机制。（挖坑。。。。）

[^1]:[C语言教学网](http://c.biancheng.net/view/7186.html)
[^2]:[jekell官方文档](http://jekyllcn.com/docs/home)
