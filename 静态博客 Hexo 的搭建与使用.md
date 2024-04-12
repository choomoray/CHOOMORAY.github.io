---
title: 静态博客 Hexo 的搭建与使用
date: 2024-4-4
updated: 
tags: 
  - 安装配置
  - 使用教程
  - Blog
  - Hexo
  - NodeJS
  - Git
categories: 
  - 其它
cover: https://github.com/choomoray/choomoray.github.io/blob/image_backup/2023/静态博客Hexo安装使用教程/封面.png?raw=true
---



{% note warning no-icon %}

**使用`Hexo`+`Github` 搭建静态博客**，不需要购买域名、服务器资源，也不需要繁琐的备案，从难易程度上静态博客的搭建是比动态的要简单些的，唯一不便之处可能就是操作文章很繁琐。

{% endnote %}

----



# 写博客

主要使用`Markdown`格式写博客，出于美化缘故，一些语法会有一丝丝不同。



## 文章页面配置

在文章最上方使用`---`可填写文章页面配置信息Front-matter

```yaml
---
title: 		# 文章标题
date: 		# 创建时间
updated: 	# 修改时间
tags: 		# 标签 # 多个标签使用 - 隔开
  - tag1
  - tag2
  - ...
categories:	# 类别 # 同标签，但有上下级关系
  - categories1
  - categories2
  - ...
cover: https://xxx.png # 封面图片
---

# 写法				# 解释
title				【必需】文章标题
date				【必需】文章创建日期
updated				【可选】文章更新日期
tags				【可选】文章标签
categories			【可选】文章分类
keywords			【可选】文章关键字
description			【可选】文章描述
top_img				【可选】文章顶部图片
cover				【可选】文章缩略图(如果没有设置top_img,文章页顶部将显示缩略图，可设为false/图片地址/留空)
comments			【可选】显示文章评论模块(默认 true)
toc				【可选】显示文章TOC(默认为设置中toc的enable配置)
toc_number			【可选】显示toc_number(默认为设置中toc的number配置)
toc_style_simple		【可选】显示 toc 简洁模式
copyright			【可选】显示文章版权模块(默认为设置中post_copyright的enable配置)
copyright_author		【可选】文章版权模块的文章作者
copyright_author_href		【可选】文章版权模块的文章作者链接
copyright_url			【可选】文章版权模块的文章连结链接
copyright_info			【可选】文章版权模块的版权声明文字
mathjax				【可选】显示mathjax(当设置 mathjax 的 per_page: false 时，才需要配置，默认 false )
katex				【可选】显示 katex (当设置 katex 的 per_page: false 时，才需要配置，默认 false )
aplayer				【可选】在需要的页面加载 aplayer 的 js 和 css,请参考文章下面的音乐 配置
highlight_shrink		【可选】配置代码框是否展开(true/false)(默认为设置中 highlight_shrink 的配置)
aside				【可选】显示侧边栏 (默认 true)
abcjs				【可选】加载 abcjs (当设置 abcjs 的 per_page: false 时，才需要配置，默认 false )
password			【可选】文章密码

```





## 博客美化



### 提示标签







{% tabs 提示标签 %}

<!-- tab  标签样式 -->

{% note simple %}

**[butterfly](https://butterfly.js.org/posts/2df239ce/#Note-Bootstrap-Callout) 提供了非常多的提示标签样式[参考](https://zhu-dongya.gitee.io/posts/hexo-butterfly-04/)：**

**图标样式：none、<font color=gray>default</font>、<font color=6F42C1>primary</font>、<font color=5CB85C>success</font>、<font color=31708F>info</font>、<font color=8A6D3B>warning</font>、<font color=A94442>danger</font>**

**标签样式：simple、modern、flat、disabled、no-icon**

```yaml
{% note 图标样式 标签样式 %}

{% endnote %}
```



{% endnote %}



{% tabs 标签样式, 3 %}

<!-- tab simple -->

{% note simple%}

none

{% endnote %}

{% note default simple%}

default

{% endnote %}

{% note primary simple%}

primary

{% endnote %}

{% note success simple%}

success

{% endnote %}

{% note info simple%}

info

{% endnote %}

{% note warning simple%}

warning

{% endnote %}

{% note danger simple%}

danger

{% endnote %}

<!-- endtab -->



<!-- tab modern -->

{% note modern%}

none

{% endnote %}

{% note default modern%}

default

{% endnote %}

{% note primary modern%}

primary

{% endnote %}

{% note success modern%}

success

{% endnote %}

{% note info modern%}

info

{% endnote %}

{% note warning modern%}

warning

{% endnote %}

{% note danger modern%}

danger

{% endnote %}

<!-- endtab -->



<!-- tab flat -->

{% note flat%}

none

{% endnote %}

{% note default flat%}

default

{% endnote %}

{% note primary flat%}

primary

{% endnote %}

{% note success flat%}

success

{% endnote %}

{% note info flat%}

info

{% endnote %}

{% note warning flat%}

warning

{% endnote %}

{% note danger flat%}

danger

{% endnote %}

<!-- endtab -->



<!-- tab disabled -->

{% note disabled%}

none

{% endnote %}

{% note default disabled%}

default

{% endnote %}

{% note primary disabled%}

primary

{% endnote %}

{% note success disabled%}

success

{% endnote %}

{% note info disabled%}

info

{% endnote %}

{% note warning disabled%}

warning

{% endnote %}

{% note danger disabled%}

danger

{% endnote %}

<!-- endtab -->



<!-- tab no-icon -->

{% note no-icon%}

none

{% endnote %}

{% note default no-icon%}

default

{% endnote %}

{% note primary no-icon%}

primary

{% endnote %}

{% note success no-icon%}

success

{% endnote %}

{% note info no-icon%}

info

{% endnote %}

{% note warning no-icon%}

warning

{% endnote %}

{% note danger no-icon%}

danger

{% endnote %}

<!-- endtab -->



<!-- tab 自定义 -->

当然，还有自定义icon样式

{% note 'fab fa-apple' simple %}

在 [矢量图库](https://fontawesome.com.cn/v4/icons)中选择喜欢的矢量图

```yaml
{% note 'fab xxx' simple %}

{% endnote %}
```



{% endnote %}



<!-- endtab -->

{% endtabs %}

<!-- endtab -->



<!-- tab 分栏 -->

{% tabs 分栏名字 %}

<!-- tab 预览 -->

{% tabs 分栏预览, 2 %}

<!-- tab -->

空

<!-- endtab -->



<!-- tab -->

设置默认预览分栏

<!-- endtab -->



<!-- tab 自定义名字 @fab fa-apple -->

自定义名字  + 矢量图片

<!-- endtab -->

{% endtabs %}

<!-- endtab -->



<!-- tab 实现 -->

```yaml
{% tabs %}	

<!-- tab -->

<!-- endtab -->

<!-- tab -->

<!-- endtab -->

{% endtabs %}
```



```yaml
# 默认分栏名字，默认显示某个分栏
{% tabs 分栏预览, 2 %}	

# 第一个分栏
<!-- tab -->

空

<!-- endtab -->


# 第二个分栏

<!-- tab -->

设置默认预览分栏

<!-- endtab -->


# 第三个分栏
<!-- tab 自定义名字 @fab fa-apple -->

自定义名字  + 矢量图片

<!-- endtab -->


{% endtabs %}
```



<!-- endtab -->

{% endtabs %}

<!-- endtab -->

<!-- tab 折叠框 -->

{% tabs 折叠框 %}

<!-- tab 预览 -->

{% folding name open,默认打开的折叠框 %}

这是一个默认打开的折叠框

{% endfolding %}



{% folding name, 内嵌代码块%}

```yaml
hello world
```

{% endfolding %}



{% folding red, 嵌套测试 %}
{% folding blue, 嵌套 %}
没了
{% endfolding %}
{% endfolding %}

<!-- endtab -->

<!-- tab 实现 -->

````yaml
{% folding ID open,默认打开的折叠框 %}
这是一个默认打开的折叠框
{% endfolding %}

{% folding name, 内嵌代码块%}
```yaml
hello world
```
{% endfolding %}

{% folding red, 嵌套测试 %}
{% folding blue, 嵌套 %}
没了
{% endfolding %}
{% endfolding %}
````



<!-- endtab -->

{% endtabs %}

<!-- endtab -->

{% endtabs %}





----



# 环境搭建

{% tabs 环境搭建 %}

<!-- tab NodeJs -->

{% note no-icon %}

**NodeJS** 的安装说实在搞得头大，总是莫名其妙的出现各种问题，像 cnpm 系统不识别之类的，总之就是非常头大，不过还好，总算是找到了一个没有任何报错的安装方法→ [BV19F411t7zX](https://www.bilibili.com/video/BV19F411t7zX/?vd_source=b4e7a930b6168115887cecaf26f330e6)。

{% endnote %}



1. **下载 NodeJS**

   [NodeJS 官网](https://nodejs.cn/download/) 下载对应版本，这里使用的是 Windows-64 安装包

   ![NodeJS版本选择](https://github.com/choomoray/choomoray.github.io/blob/image_backup/2023/静态博客Hexo安装使用教程/NodeJS版本选择.png?raw=true)

   解压后新建两个文件夹：用来放缓存文件的 `node_cache` 和用来放系统全局文件的 `node_global`

2. **配置环境变量**

   在**系统变量**中新建一个  `NODE_HOME`

   ![配置环境变量](https://github.com/choomoray/choomoray.github.io/blob/image_backup/2023/静态博客Hexo安装使用教程/配置环境变量.png?raw=true)

   然后再从**系统变量**的 `PATH` 中添加下面三段

   ```
   %NODE_HOME%
   %NODE_HOME%\node_cache
   %NODE_HOME%\node_global
   ```

   以上工作完成后，再终端中输入 `node -v`、`npm -v` 测试环境变量是否配置成功

3. **配置 npm & cnpm**

   ```
   // 配置 npm 全局
   npm config set prefix "node_global 的路径"
   // 配置 npm 缓存
   npm config set cache "node_cache 的路径"
   // 国内下载慢所以用阿里的镜像下载
   npm config set registry https://registry.npm.taobao.org
   ```

   没有报错就说明已经成功配置了，然后就可以下载镜像文件了

   ```
   npm install -g cnpm
   ```

   安装成功后输入 `cnpm -v` 测试是否成功，在 node_global 文件夹下也可以看到 cnpm 文件，NodeJS 的安装配置到此完成！

<!-- endtab -->



<!-- tab Git -->

{% note no-icon %}

[Git](https://git-scm.com/downloads) 直接下载对应版本安装即可，一直下一步傻瓜式安装

{% endnote %}



{% note no-icon %}

Git的使用在以后用到的时候再进行更新，目前仅为上传不同名文件夹内容到远程仓库的不同分支中，方法也非常简单，使用Github桌面端就可以进行操作，把仓库克隆到要上传的文件夹父目录，克隆完成后把名字一改再重新寻址就可以了

{% endnote %}

<!-- endtab -->



<!-- tab Hexo -->

1. **Hexo 安装**

   {% note no-icon %}

   Hexo 官网有提供的详尽的 [安装使用文档](https://hexo.io/zh-cn/docs/)，需要注意的是，Hexo 需要搭配 Git 和 NodeJS 使用，在安装之前需要把前面两个提前安装！也可以参考→[BV1Yb411a7ty](https://www.bilibili.com/video/BV1Yb411a7ty/?vd_source=b4e7a930b6168115887cecaf26f330e6)

   {% endnote %}

   Hexo 使用的是命令行进行操作，首先**安装 Hexo**，hexo -v 测试安装

   ```yaml
   cnpm install -g hexo-cli
   ```

   在博客文件夹根目录下**初始化 Hexo**

   ```yaml
   hexo init
   npm install	// 初始化成功了就不需要再执行这步了
   ```

2. **Hexo 基本操作**

   |     功能     |    代码    |   代码全称    |
   | :----------: | :--------: | :-----------: |
   | 启动本地预览 |   hexo s   |  hexo server  |
   | 清理本地缓存 | hexo clean |  hexo clean   |
   | 生成HTML文件 |   hexo g   | hexo generate |
   |  推送到云端  |   hexo d   |  hexo deploy  |
   | 创建新的文章 |   hexo n   |   hexo new    |

3. **Blog 部署到 Github**

   首先再本目录下安装部署插件

   ```
   cnpm install --save hexo-deployer-git
   ```

   插件装完后去 `_config.yml` 里进行必要配置！在文件最下面修改 `# Deployment` 里面的信息

   ```
   type: git
   repo: https://github.com/choomoray/choomoray.github.io.git
   branch: blog	// 可以不写，默认保存到 Github 仓库的 master 分支中
   ```

   







<!-- endtab -->

{% endtabs %}











# 主题 & 美化（待完成......）

在 [Butterfly](https://github.com/jerryc127/hexo-theme-butterfly) 下载好压缩包，解压到 Theme 文件夹，然后在 `_config.yml` 里把默认的 Theme 替换成需要修改的主题文件夹名就大功告成了！



{% note no-icon %}

主题美化可以参考作者写的[详细文档](https://butterfly.js.org/)

{% endnote %}



## 网站美化

{%tabs 网站基本信息,2%}

<!-- tab 主配置文件 -->

{%folding 1, 网站基本信息 %}

```yaml
# Site
title: CHOOMORAY	# 网站标题
subtitle: ''		# 网站副标题
description: ''
keywords:
author: choomoray 	# 作者名
language: zh-CN
timezone: ''

# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
url: https://choomoray.github.io/	# 网站链接
```

{%endfolding%}{%folding 2, 设置默认主题 %}

```yaml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: hexo-theme-butterfly-dev
```

{%endfolding%}{%folding 3, Git推送%}

```yaml
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git	# 推送类型
  repo: https://github.com/choomoray/choomoray.github.io.git	# 推送目标
  branch: blog	# 推送分支
```

{%endfolding%}

<!-- endtab --> <!-- tab 主题配置文件 -->

{%folding 1, 导航栏%}

```yaml
nav: # 折叠导航栏
  logo: 		# image
  display_title: true	# 左上角 HOME
  fixed: false 		# 折叠导航栏
  
menu: # 导航栏内容
  首页: / || fas fa-home
  时间轴: /archives/ || fas fa-archive
  标签: /tags/ || fas fa-tags
  分类: /categories/ || fas fa-folder-open
  收藏: /link/ || fas fa-link
  ME: /diary/ || fas fa-video
  # List||fas fa-list:
  #   Music: /music/ || fas fa-music
  #   Movie: /movies/ || fas fa-video
  # Link: /link/ || fas fa-link
  # About: /about/ || fas fa-heart
```

{%endfolding%} {%folding 4, 侧边栏%}

```yaml
aside:
  enable: true
  hide: false
  button: true
  mobile: true # display on mobile
  position: left # left or right
  display:
    archive: true
    tag: true
    category: true
  card_author:
    enable: true
    description:
    button:
      enable: true
      icon: fab fa-github
      text: Follow Me
      link: https://github.com/choomoray
```



  {%endfolding%}{%folding 6, 目录%}

```yaml
toc:
  post: true	# 文章页
  page: true
  number: true	# 章节显示
  expand: true	# 折叠目录
  style_simple: true # for post
  scroll_percent: true
```

  {%endfolding%}{%folding 9, 底栏%}

```yaml
footer:
  owner:
    enable: true
    since: 2024
  custom_text: 
  copyright: false # Copyright of theme and framework
```

 {%endfolding%} {%folding 2, 代码块样式 & 显示行数限制%}

```yaml
highlight_theme: light 	# 代码块样式
highlight_copy: true 	# 右上角 复制按钮
highlight_lang: true 	# 显示代码语言
highlight_shrink: false # 折叠代码块
highlight_height_limit: 120 # unit: px # 代码块显示行数限制
code_word_wrap: false	
```

{%endfolding%}  {%folding 7, 文章修改%}

```yaml
post_edit:
  enable: false
  # url: https://github.com/user-name/repo-name/edit/branch-name/subdirectory-name/
  # For example: https://github.com/jerryc127/butterfly.js.org/edit/main/source/
  url:
```

{%endfolding%} {%folding 8, 过期提醒%}

```yaml
noticeOutdate:
  enable: true
  style: flat # style: simple/flat
  limit_day: 500 # When will it be shown
  position: top # position: top/bottom
  message_prev: 文章过期提示：本文最近更新于
  message_next: 天前，部分信息可能已经过时，请谨慎参考本文内容。
```

{%endfolding%}   {%folding 3, 允许复制%}

```yaml
# copy settings
# copyright: 复制的内容后面加上版权信息
copy:
  enable: true	# 允许复制
  copyright:
    enable: false
    limit_count: 50
```

{%endfolding%}   {%folding 5, 打赏%}

```yaml
# Sponsor/reward
reward:
  enable: true
  text: 
  QR_code:
    - img: https://github.com/choomoray/choomoray.github.io/blob/image_backup/%E8%83%8C%E6%99%AF%E5%9B%BE/%E5%BE%AE%E4%BF%A1%E8%B5%9E%E8%B5%8F%E7%A0%81.png?raw=true
      link: https://choomoray.github.io/
      text: 微信
```

 {%endfolding%}  {%folding 10, 访问人数 & 运行时长%}

```yaml
busuanzi: # 访问人数
  site_uv: false
  site_pv: false
  page_pv: false

# Time difference between publish date and now
# Formal: Month/Day/Year Time or Year/Month/Day Time
runtimeshow:	# 运行时长
  enable: false
  publish_date: 1/1/2024

# Aside widget - Newest Comments
newest_comments:	# 评论
  enable: false
  sort_order: # Don't modify the setting unless you know how it works
  limit: 6
  storage: 10 # unit: mins, save data to localStorage
  avatar: true
```

 {%endfolding%}   {%folding 11, 右下按钮（翻译 & 阅读模式 & 深色模式）%}

```yaml
translate:	# 翻译
  enable: false
  # The text of a button
  default: 繁
  # the language of website (1 - Traditional Chinese/ 2 - Simplified Chinese）
  defaultEncoding: 2
  # Time delay
  translateDelay: 0
  # The text of the button when the language is Simplified Chinese
  msgToTraditionalChinese: '繁'
  # The text of the button when the language is Traditional Chinese
  msgToSimplifiedChinese: '簡'

# Read Mode 阅读模式
readmode: true

# dark mode 深色模式
darkmode:	
  enable: true
  # Toggle Button to switch dark/light mode
  button: true
  # Switch dark/light mode automatically (自動切換 dark mode和 light mode)
  # autoChangeMode: 1  Following System Settings, if the system doesn't support dark mode, it will switch dark mode between 6 pm to 6 am
  # autoChangeMode: 2  Switch dark mode between 6 pm to 6 am
  # autoChangeMode: false
  autoChangeMode: true
  # Set the light mode time. The value is between 0 and 24. If not set, the default value is 6 and 18
  start: # 8
  end: # 22
```

 {%endfolding%}  {% folding 主页仿键盘敲入文字效果%}

```yaml
subtitle:
  enable: true
  # Typewriter Effect (打字效果)
  effect: true
  # Customize typed.js (配置typed.js)
  # https://github.com/mattboldt/typed.js/#customization
  # startDelay: 300 # time before typing starts in milliseconds
  # typeSpeed: 150 # type speed in milliseconds
  # backSpeed: 50 # backspacing speed in milliseconds

  typed_option:
  # source 调用第三方服务
  # source: false 关闭调用
  # source: 1  调用一言网 https://hitokoto.cn/
  # source: 2  调用一句网 https://yijuzhan.com/
  # source: 3  调用今日诗词 https://www.jinrishici.com/
  # subtitle 会先显示 source , 再显示 sub 的內容
  source: false
  # 如果关闭打字效果，subtitle 只会显示 sub 的第一行文字
  sub:  
    - 今日事，今日毕！
    - 书不记，熟读可记；义不精，细思可精；惟有志不立，直是无着力处。
    - 有志者，事竟成，破釜沉舟，百二秦关终属楚；苦心人，天不负，卧薪尝胆，三千越甲可吞吴。
    - 静以修身，俭以养德，非淡泊无以明志，非宁静无以致远。
    - 尺有所短；寸有所长。物有所不足；智有所不明。
```

{%endfolding%}{%folding 网页进入效果%}

```yaml
# Enter transitions
enter_transitions: true
```

{%endfolding%}{%folding 打字效果%}

```yaml
# Typewriter Effect (打字效果)
# https://github.com/disjukr/activate-power-mode
activate_power_mode:
  enable: false
  colorful: true # open particle animation (冒光特效)
  shake: true #  open shake (抖动特效)
  mobile: false
```

{%endfolding%}{%folding 背景样式%}

```yaml
# Background effects (背景特效)
# --------------------------------------

# canvas_ribbon (静止彩带背景)
# See: https://github.com/hustcc/ribbon.js
canvas_ribbon:
  enable: false
  size: 150
  alpha: 0.6
  zIndex: -1
  click_to_change: true
  mobile: false

# Fluttering Ribbon (动态彩带背景)
canvas_fluttering_ribbon:
  enable: true
  mobile: false
  	
# canvas_nest	# 纯色背景
# https://github.com/hustcc/canvas-nest.js
canvas_nest:
  enable: false
  color: '0,0,255' #color of lines, default: '0,0,0'; RGB values: (R,G,B).(note: use ',' to separate.)
  opacity: 0.7 # the opacity of line (0~1), default: 0.5.
  zIndex: -1 # z-index property of the background, default: -1.
  count: 99 # the number of lines, default: 99.
  mobile: false
```

{%endfolding%}{%folding 鼠标点击效果%}

```yaml
# Mouse click effects: fireworks (鼠标点击效果: 烟花特效)
fireworks:
  enable: false
  zIndex: 9999 # -1 or 9999
  mobile: false

# Mouse click effects: Heart symbol (鼠标点击效果：爱心)
click_heart:
  enable: false
  mobile: false

# Mouse click effects: words (鼠标点击效果：文字)
clickShowText:
  enable: true
  text:
    - 富强
    - 民主
    - 文明
    - 和谐
    - 自由
    - 平等
    - 公正
    - 法治
    - 爱国
    - 敬业
    - 诚信  
    - 友善
  fontSize: 15px
  random: true
  mobile: true
```

{%endfolding%}

<!-- endtab -->

{% endtabs %}



## 文章美化



### 顶栏图片

| 配置             | 解释                                                         |
| :--------------- | :----------------------------------------------------------- |
| index_img        | 主页的 top_img                                               |
| default_top_img  | 默认的 top_img，当页面的 top_img 没有配置时，会显示 default_top_img |
| archive_img      | 归档页面的 top_img                                           |
| tag_img          | tag 子页面 的 默认 top_img                                   |
| tag_per_img      | tag 子页面的 top_img，可配置每个 tag 的 top_img              |
| category_img     | category 子页面 的 默认 top_img                              |
| category_per_img | category 子页面的 top_img，可配置每个 category 的 top_img    |







## 功能补充

### <span id="jump_功能补充页">标签页 & 分类页</span>

模板默认是没有标签页和分类页的，需要我们自己添加，非常简单，在命令行中分别敲入下面两行代码，`source` 目录下就会自动生成对应文件夹，里面的 index.md 就是对应文件

```yaml
hexo new page tags
hexo new page categories
```



### 搜索功能

非常实用的搜索功能，但是 Hexo 原生并不支持，需要安装依赖：

```yaml
npm install hexo-generator-search --save
```

修改`主配置文件`，添加如下内容：

```yaml
search:	# 搜索
  path: search.xml
  field: post
  content: true
  template: ./search.xml
```

在主题中开启搜索，在`主题配置文件`添加以下内容：

```yaml
local_search:
-  enable: false
+  enable: true
```



### <span id='jump_文章加密'>文章加密</span>

> 静态博客文章加密典型的防君子不防小人，程序只是卡在了调用那里，后台该能看到的还是可以看到的！

文章加密同样需要依赖支持：

```yaml
npm install --save hexo-blog-encrypt
```

在`主配置文件`中添加下面代码：

```yaml
# 安全
encrypt: # hexo-blog-encrypt
  abstract: 这里有东西被加密了，需要输入密码查看哦。
  message: 您好, 这里需要密码.
  tags:
  - {name: tagName, password: 密码A}
  - {name: tagName, password: 密码B}
  template: <div id="hexo-blog-encrypt" data-wpm="{{hbeWrongPassMessage}}" data-whm="{{hbeWrongHashMessage}}"><div class="hbe-input-container"><input type="password" id="hbePass" placeholder="{{hbeMessage}}" /><label>{{hbeMessage}}</label><div class="bottom-line"></div></div><script id="hbeData" type="hbeData" data-hmacdigest="{{hbeHmacDigest}}">{{hbeEncryptedData}}</script></div>
  wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
  wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
```

在文章中使用加密，在「头文件」中添加 `password` 关键词即可：

```yaml
password: 123456
```

![访问内容需要密码](https://github.com/choomoray/choomoray.github.io/blob/image_backup/2023/静态博客Hexo安装使用教程/访问内容需要密码.png?raw=true)



### 插入本地图片

> [官方文档](https://hexo.io/zh-cn/docs/asset-folders)简单易懂，要比网上一个答案到处抄来的靠谱（花了好几个小时也没成功）。总结一下：

首先要打开`主配置文档`中的`允许使用本地静态资源`：

```yaml
post_asset_folder: true
```

然后在`source`文件夹下创建`images`文件，把图片放入images文件夹就可以了，引用格式如下：

```yaml
![图片描述](../images/....../1.png)
```

需要注意的是：图片路径必须使用`/`



### 页面锚点

开启页面锚点后，当你在进行滚动时，页面链接会根据标题ID进行替换
(注意: 每替换一次，会留下一个历史记录。所以如果一篇文章有很多锚点的话，网页的历史记录会很多。)

修改 `主题配置文件`

```yaml
# anchor
anchor:
  # when you scroll, the URL will update according to header id.
  auto_update: false
  # Click the headline to scroll and update the anchor
  click_to_scroll: false
```

