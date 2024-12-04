---
title: 静态博客 Hexo 的搭建与使用
date: 2024-11-26
updated: 2024-11-26
tags: 
  - 环境搭建
  - 手册
  - Hexo
  - Blog
  - NodeJS
cover: https://github.com/choomoray/choomoray.github.io/blob/article/2024/2024-11-26%20%E9%9D%99%E6%80%81%E5%8D%9A%E5%AE%A2Hexo%E7%9A%84%E6%90%AD%E5%BB%BA%E4%B8%8E%E4%BD%BF%E7%94%A8/%E5%B0%81%E9%9D%A2.jpg?raw=true

---



{% note warning no-icon %}

**使用`Hexo`+`Github` 搭建静态博客**，不需要购买域名、服务器资源，也不需要繁琐的备案，从难易程度上静态博客的搭建是比动态的要困难些的，还有不能像动态博客一样实时在后台进行修改。考虑到写博客的数量很少，再加上昂贵的服务器费用，这点困难好像也显得微不足道。

{% endnote %}



----



# 环境搭建

{% tabs 环境搭建, 2 %}

<!-- tab NodeJs -->

{% note no-icon %}

**NodeJS** 的安装说实在搞得头大，总是莫名其妙的出现各种问题，像 cnpm 系统不识别之类的，总之就是非常头大，不过还好，总算是找到了一个没有任何报错的安装方法→ [BV19F411t7zX](https://www.bilibili.com/video/BV19F411t7zX/?vd_source=b4e7a930b6168115887cecaf26f330e6)。

{% endnote %}

1. **下载 NodeJS**

   [NodeJS 官网](https://nodejs.cn/download/) 下载对应版本，这里使用的是 Windows-64 安装包

   解压后新建两个文件夹：用来放缓存文件的 `node_cache` 和用来放系统全局文件的 `node_global`

2. **配置环境变量**

   在**系统变量**中新建一个  `NODE_HOME`

   ![配置环境变量](https://img2.imgtp.com/2024/05/27/E312n3KL.png)

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

* **Hexo 安装**

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

* **Hexo 基本操作**

<table>
    <tr>
        <td>功能</td>
        <td>代码</td>
        <td>代码全称</td>
    </tr>
    <tr>
        <td>启动本地预览</td>
        <td>hexo s</td>
        <td>hexo server</td>
    </tr>
    <tr>
        <td>清理本地缓存</td>
        <td>hexo clean</td>
        <td>hexo clean</td>
    </tr>
    <tr>
        <td>生成 HTML 文件</td>
        <td>hexo g</td>
        <td>hexo generate</td>
    </tr>
    <tr>
        <td>推送到云端</td>
        <td>hexo d</td>
        <td>hexo deploy</td>
    </tr>
    <tr>
        <td>创建新的文章</td>
        <td>hexo n</td>
        <td>hexo new</td>
    </tr>
</table>

* **Blog 部署到 Github**

1. 首先再本目录下安装部署插件

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



# 主题 & 美化（缝缝补补中......）



{% note no-icon %}

主题美化包下载：[【Butterfly】](https://github.com/jerryc127/hexo-theme-butterfly)

主题美化可以参考作者写的[【详细文档】](https://butterfly.js.org/)

{% endnote %}

## 基础功能设置

在进行美化前，先将网站的基础设置配置一下：

将主题文件夹里的`_config.yml`复制一份到根目录下，改名为`_config.(your theme name).yml`，Hexo会先根据这里的配置文件配置主题。之后修改主题配置直接在这里修改就可以了，升级主题也可以直接覆盖原主题。

设置Github推送：在`_config.yml`文件夹内代修改：

<details> <summary>Github推送</summary><pre><code> 
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git	# 推送类型
  repo: https://github.com/choomoray/choomoray.github.io.git	# 推送目标
  branch: blog	# 推送分支
</code></pre> </details>



<details> <summary>名字</summary><pre><code>
```
内容
```
</code></pre> </details>

````
<details> <summary>名字</summary><pre><code>
```
内容
```
</code></pre> </details>
````



## 网站美化

{%tabs 网站基本信息,2%}

<!-- tab 主配置文件 -->

<details> <summary>添加.yml文件</summary><pre><code>
```
将主题文件夹里的_config.yml复制一份到根目录下
改名为_config.(your theme name).yml
Hexo会先根据这里的配置文件配置主题
之后修改主题配置直接在这里修改就可以了，升级主题也可以直接覆盖原主题。_config.hexo-theme-butterfly-dev.yml
```
</code></pre> </details>

<details> <summary>网站基本信息</summary><pre><code>
```
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
</code></pre> </details>

<details> <summary>设置默认主题</summary><pre><code>
```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: hexo-theme-butterfly-dev
```
</code></pre> </details>

<details> <summary>Git推送</summary><pre><code>
```
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git	# 推送类型
  repo: https://github.com/choomoray/choomoray.github.io.git	# 推送目标
  branch: blog	# 推送分支
```
</code></pre> </details>

<!-- endtab --> <!-- tab 主题配置文件 -->

<details> <summary>颜色</summary><pre><code>
```
# Beautify/Effect (美化/效果)
# --------------------------------------
# Theme color for customize
# Notice: color value must in double quotes like "#000" or may cause error!
theme_color:
  enable: true
  main: gray
#   paginator: "#00c4b6"
#   button_hover: "#FF7242"
#   text_selection: "#00c4b6"
#   link_color: "#99a9bf"
#   meta_color: "#858585"
#   hr_color: "#A4D8FA"
#   code_foreground: "#F47466"
#   code_background: "rgba(27, 31, 35, .05)"
#   toc_color: "#00c4b6"
#   blockquote_padding_color: "#49b1f5"
#   blockquote_background_color: "#49b1f5"
#   scrollbar_color: "#49b1f5"
#   meta_theme_color_light: "ffffff"
#   meta_theme_color_dark: "#0d0d0d"
# Website Background (设置网站背景颜色)
# can set it to color or image (可以设置图片 和 颜色)
# The formal of image: url(http://xxxxxx.com/xxx.jpg)
background:
# Footer Background
footer_bg: "#C9C9C9"	# 设置网站底部颜色
```
</code></pre> </details>

<details> <summary>导航栏</summary><pre><code>
```
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
</code></pre> </details>

<details> <summary>侧边栏</summary><pre><code>
```
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
</code></pre> </details>

<details> <summary>目录</summary><pre><code>
```
toc:
  post: true	# 文章页
  page: true
  number: true	# 章节显示
  expand: true	# 折叠目录
  style_simple: true # for post
  scroll_percent: true
```
</code></pre> </details>

<details> <summary>底栏</summary><pre><code>
```
footer:
  owner:
    enable: true
    since: 2024
  custom_text: 
  copyright: false # Copyright of theme and framework
```
</code></pre> </details>

<details> <summary>主页显示文章封面</summary><pre><code>
```
cover:
  # display the cover or not (是否显示文章封面)
  index_enable: true
  aside_enable: true
  archives_enable: true
  # the position of cover in home page (封面显示的位置)
  # left/right/both
  position: both
  # When cover is not set, the default cover is displayed (没有设置封面cover时，显示默认的封面)
  default_cover:
    # - https://i.loli.net/2020/05/01/gkihqEjXxJ5UZ1C.jpg
```
</code></pre> </details>

<details> <summary>允许复制</summary><pre><code>
```
# copy settings
# copyright: 复制的内容后面加上版权信息
copy:
  enable: true	# 允许复制
  copyright:
    enable: false
    limit_count: 50
```
</code></pre> </details>

<details> <summary>访问人数 & 运行时长</summary><pre><code>
```
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
</code></pre> </details>

<details> <summary>右下按钮（翻译 & 阅读模式 & 深色模式）</summary><pre><code>
```
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
</code></pre> </details>

<details> <summary>主页仿键盘敲入文字效果</summary><pre><code>
```
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
    - 静以修身，俭以养德，非淡泊无以明志，非宁静无以致远。
    - 尺有所短；寸有所长。物有所不足；智有所不明。
```
</code></pre> </details>

<details> <summary>网页进入效果</summary><pre><code>
```
# Enter transitions
enter_transitions: true
```
</code></pre> </details>

<details> <summary>打字效果</summary><pre><code>
```
# Typewriter Effect (打字效果)
# https://github.com/disjukr/activate-power-mode
activate_power_mode:
  enable: false
  colorful: true # open particle animation (冒光特效)
  shake: true #  open shake (抖动特效)
  mobile: false
```
</code></pre> </details>

<details> <summary>背景样式</summary><pre><code>
```
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
</code></pre> </details>

<details> <summary>鼠标点击效果</summary><pre><code>
```
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
</code></pre> </details>

<details> <summary>图片大图查看模式</summary><pre><code>
```
# Lightbox (图片大图查看模式)
# --------------------------------------
# You can only choose one, or neither (只能选择一个，或者两个都不选)
# medium-zoom
# https://github.com/francoischalifour/medium-zoom
medium_zoom: false
# fancybox
# https://fancyapps.com/fancybox/
fancybox: false
```
</code></pre> </details>

<details> <summary>网页预加载</summary><pre><code>
```
# https://instant.page/
# prefetch 预加载
instantpage: true
```
</code></pre> </details>

<details> <summary>图片懒加载</summary><pre><code>
```
# Lazyload (图片懒加载)
# https://github.com/verlok/vanilla-lazyload
lazyload:
  enable: true
  field: site # site/post
  placeholder: /img/加载图片.gif # 加载出图片前的占位符
  blur: true	# 模糊加载效果
```
</code></pre> </details>

<!-- endtab -->

{%endtabs%}

## 文章美化

{%tabs 文章美化%}

<!--tab 功能添加-->

<details> <summary>搜索功能</summary><pre><code>
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
</code></pre> </details>

<details> <summary>文章加密</summary><pre><code>
{%note no-icon%}静态博客文章加密典型的防君子不防小人，程序只是卡在了调用那里，后台该能看到的还是可以看到的！{%endnote%}
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
![访问内容需要密码](https://github.com/choomoray/choomoray.github.io/blob/image/2023/静态博客Hexo安装使用教程/访问内容需要密码.png?raw=true)
</code></pre> </details>

<details> <summary>页面锚点</summary><pre><code>
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
</code></pre> </details>

<details> <summary>插入本地图片</summary><pre><code>
{%note no-icon%}[官方文档](https://hexo.io/zh-cn/docs/asset-folders)简单易懂，要比网上一个答案到处抄来的靠谱（花了好几个小时也没成功）。总结一下：{%endnote%}
首先要打开`主配置文档`中的`允许使用本地静态资源`：
```yaml
post_asset_folder: true
```
然后在`source`文件夹下创建`images`文件，把图片放入images文件夹就可以了，引用格式如下：
```yaml
![图片描述](../images/....../1.png)
```
{%note info disabled%}需要注意的是：图片路径必须使用`/`{%endnote%}
</code></pre> </details>

<details> <summary>标签页 & 分类页</summary><pre><code>
{%note no-icon%}模板默认是没有标签页和分类页的，需要我们自己添加，非常简单，在命令行中分别敲入下面两行代码，`source` 目录下就会自动生成对应文件夹，里面的 index.md 就是对应文件{%endnote%}
```yaml
hexo new page tags
hexo new page categories
```
{%note no-icon%}分类页和主页的背景图片{%endnote%}
<table>
    <tr>
        <td>配置</td>
        <td>解释</td>
    </tr>
    <tr>
        <td>index_img</td>
        <td>主页的 top_img</td>
    </tr>
    <tr>
        <td>default_top_img</td>
        <td>默认的 top_img，当页面的 top_img 没有配置时，会显示 default_top_img</td>
    </tr>
    <tr>
        <td>archive_img</td>
        <td>归档页面的 top_img</td>
    </tr>
    <tr>
        <td>tag_img</td>
        <td>tag 子页面 的 默认 top_img</td>
    </tr>
    <tr>
        <td>tag_per_img</td>
        <td>tag 子页面的 top_img，可配置每个 tag 的 top_img</td>
    </tr>
    <tr>
        <td>category_img</td>
        <td>category 子页面 的 默认 top_img</td>
    </tr>
    <tr>
        <td>category_per_img</td>
        <td>category 子页面的 top_img，可配置每个 category 的 top_img</td>
    </tr>
</table>
</code></pre> </details>

<details> <summary>字数统计</summary><pre><code>
要实现字数统计功能，需要安装依赖后重新编译：
```yaml
npm install hexo-wordcount --save
或 yarn add hexo-wordcount
```
```yaml
# wordcount (字数统计)
# see https://butterfly.js.org/posts/ceeb73f/
wordcount:
  enable: true
  post_wordcount: true
  min2read: true
  total_wordcount: true
```
</code></pre> </details>

<!--endtab--> <!--tab 内容美化-->

<details> <summary>美化页面显示</summary><pre><code>
{%note info disabled%}文章中的标题H1H2...和分隔线等美化{%endnote%}
```yaml
beautify:
  enable: true
  field: site # site/post
  title-prefix-icon: # '\f0c1'
  title-prefix-icon-color: # '#F47466'
```
</code></pre> </details>

<details> <summary>代码块样式 & 显示行数限制</summary><pre><code>
```
highlight_theme: light  # 代码块样式
highlight_copy: true    # 右上角 复制按钮
highlight_lang: true    # 显示代码语言
highlight_shrink: false # 折叠代码块
highlight_height_limit: 120 # unit: px # 代码块显示行数限制
code_word_wrap: false 
```
</code></pre> </details>

<details> <summary>文章修改</summary><pre><code>
```
post_edit:
  enable: false
  # url: https://github.com/user-name/repo-name/edit/branch-name/subdirectory-name/
  # For example: https://github.com/jerryc127/butterfly.js.org/edit/main/source/
  url:
```
</code></pre> </details>

<details> <summary>过期提醒</summary><pre><code>
```
noticeOutdate:
  enable: true
  style: flat # style: simple/flat
  limit_day: 500 # When will it be shown
  position: top # position: top/bottom
  message_prev: 文章过期提示：本文最近更新于
  message_next: 天前，部分信息可能已经过时，请谨慎参考本文内容。
```
</code></pre> </details>

<details> <summary>版权声明</summary><pre><code>
```
post_copyright:
  enable: true
  decode: true	# 显示文字（默认全字母）
  author_href:
  license: KFC-VME-50
  license_url: https://choomoray.github.io/
```
</code></pre> </details>

<details> <summary>分享</summary><pre><code>
```
# Share System (分享)
# --------------------------------------
# Share.js
# https://github.com/overtrue/share.js
sharejs:
  enable: false
  sites: facebook,twitter,wechat,weibo,qq
# AddToAny
# https://www.addtoany.com/
addtoany:
  enable: false
  item: facebook,twitter,wechat,sina_weibo,facebook_messenger,email,copy_link
```
</code></pre> </details>

<details> <summary>打赏</summary><pre><code>
```
# Sponsor/reward
reward:
  enable: true
  text: 
  QR_code:
    - img: https://github.com/choomoray/choomoray.github.io/blob/image/Hexo/%E5%BE%AE%E4%BF%A1%20%E8%B5%9E%E8%B5%8F%E7%A0%81.png?raw=true
      link: https://choomoray.github.io/
      text: 微信
```
</code></pre> </details>

<!--endtab-->

{%endtabs%}





















