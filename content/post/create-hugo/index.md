---
title: "【Hugo】Stack主题的使用记录"
date: 2024-10-02 00:00:00+0000
weight: 1
image: https://hugo.opendocs.io/images/hugo-logo-wide.svg
---
Hugo官网

运行环境
hugo版本：v0.117.0（扩展版）

go：1.21.0

PowerShell 7（x64）

Windows10

Hugo是一个使用Go编写的静态站点生成器，即网站构建工具。

静态的意思是指在内容在网站上呈现之前需要全部编译成HTML文件。而动态的站点生成器是请求哪个页面就编译生成哪个HTML页面。

在Windows上可以选用包管理器Chocolatey、Scoop、Winget来安装Hugo。

这里我选择使用winget来安装。

安装winget：从 Microsoft Store 获取应用程序安装程序。再安装Hugo扩展版。

winget install Hugo.Hugo.Extended
1
测试安装成功与否：hugo version。



使用 Hugo 时通常会使用Git、Go和Dart Sass 。Go环境则是主要用于Hugo的模块功能。Dart Sass 将 Sass 转译为 CSS。

Windows 10 默认是 Windows PowerShell 是 5.X 版本，在 Win10 V1903 以上版本后，打开 PowerShell 时，会提示 “尝试新的跨平台 PowerShell aka.ms/pscore6 ” 。安装新版PowerShell：

$ winget search Microsoft.PowerShell
Name               Id                           Version Source
--------------------------------------------------------------
PowerShell         Microsoft.PowerShell         7.3.6.0 winget
PowerShell Preview Microsoft.PowerShell.Preview 7.4.0.3 winget
$ winget install --id Microsoft.Powershell --source winget
初始化
我们在文档下面创建一个名为MyHugoSite的目录结构：

```bash
cd Documents
hugo new site MyHugoSite
cd MyHugoSite
```

提示告诉我们有关主题的获取方式、文件的添加和站点的构建。

将MyHugoSite目录初始化为Git存储库：

```bash
git init

添加主题
git submodule add https://github.com/CaiJimmy/hugo-theme-stack/ themes/hugo-theme-stack
```


使用git submodule命令添加一个子模块到themes文件夹下，这个主题子模块可以用作参考。当我们需要对其样式或功能做出修改时，可以将其内容部分或文件拷贝到根目录下（MyHugoSite）对应位置。

启用主题：在hugo.toml中添加一句theme='hugo-theme-stack'：



启动Hugo的开发服务器查看站点：

```bash
hugo server
```
按ctrl+C停止。

默认不包括草稿内容。

添加新页面：

```bash
hugo new content posts/the-first-post.md
```

启动服务器，且包含草稿内容：
```bash
hugo server --buildDrafts
或
hugo server -D
```

```bash
修改配置文件
mv hugo.toml hugo.toml.bak
cp themes/hugo-theme-stack/exampleSite/config.yaml .
```

2023/8/26的config.yaml
```yaml
baseurl: https://example.com
# languageCode: en-us
languageCode: zh-cn
theme: hugo-theme-stack
paginate: 5
title: 影麟
copyright: 影麟

languages:
    zh-cn:
        languageName: 中文
        # 博客名
        title: 影麟
        weight: 1
        params:
            description: 影麟的个人博客

    # en:
    #     languageName: English
    #     title: Example Site
    #     weight: 2
    #     params:
    #         description: Example description
    
    # ar:
    #     languageName: عربي
    #     languagedirection: rtl
    #     title: موقع تجريبي
    #     weight: 3
    #     params:
    #         description: وصف تجريبي

# Change it to your Disqus shortname before using
disqusShortname: hugo-theme-stack

# GA Tracking ID
googleAnalytics:

# Theme i18n support
# Available values: ar, bn, ca, de, el, en, es, fr, hu, id, it, ja, ko, nl, pt-br, th, uk, zh-cn, zh-hk, zh-tw
DefaultContentLanguage: zh-cn

# Set hasCJKLanguage to true if DefaultContentLanguage is in [zh-cn ja ko]
# This will make .Summary and .WordCount behave correctly for CJK languages.
hasCJKLanguage: true

permalinks:
    post: /p/:slug/
    page: /:slug/

params:
    mainSections:
        - post
    featuredImageField: image
    rssFullContent: true
    favicon:  # e.g.: favicon placed in `static/favicon.ico` of your site folder, then set this field to `/favicon.ico` (`/` is necessary)

    footer:
        since: 2020
        customText:

    # 日期格式
    dateFormat:
        published: Jan 02, 2006
        lastUpdated: Jan 02, 2006 15:04 MST

    sidebar:
        # 头像处的表情
        emoji: 🍥
        # 简介
        subtitle: 学无止境，勇攀高峰！
        avatar:
            enabled: true
            local: true
            # 位于assets/img/下的图片，头像
            src: img/avatar.png

    article:
        math: false
        toc: true
        readingTime: true
        license:
            enabled: true
            default: Licensed under CC BY-NC-SA 4.0

    comments:
        enabled: true
        provider: disqus

        disqusjs:
            shortname:
            apiUrl:
            apiKey:
            admin:
            adminLabel:

        utterances:
            repo:
            issueTerm: pathname
            label:

        remark42:
            host:
            site:
            locale:

        vssue:
            platform:
            owner:
            repo:
            clientId:
            clientSecret:
            autoCreateIssue: false

        # Waline client configuration see: https://waline.js.org/en/reference/component.html
        waline:
            serverURL:
            lang:
            pageview:
            emoji:
                - https://unpkg.com/@waline/emojis@1.0.1/weibo
            requiredMeta:
                - name
                - email
                - url
            locale:
                admin: Admin
                placeholder:

        twikoo:
            envId:
            region:
            path:
            lang:

        # See https://cactus.chat/docs/reference/web-client/#configuration for description of the various options
        cactus:
            defaultHomeserverUrl: "https://matrix.cactus.chat:8448"
            serverName: "cactus.chat"
            siteName: "" # You must insert a unique identifier here matching the one you registered (See https://cactus.chat/docs/getting-started/quick-start/#register-your-site)

        giscus:
            repo:
            repoID:
            category:
            categoryID:
            mapping:
            lightTheme:
            darkTheme:
            reactionsEnabled: 1
            emitMetadata: 0

        gitalk:
            owner:
            admin:
            repo:
            clientID:
            clientSecret:

        cusdis:
            host:
            id:
    widgets:
        homepage:
            - type: search
            - type: archives
              params:
                  limit: 5
            - type: categories
              params:
                  limit: 10
            - type: tag-cloud
              params:
                  limit: 10
        page:
            - type: toc

    opengraph:
        twitter:
            # Your Twitter username
            site:

            # Available values: summary, summary_large_image
            card: summary_large_image

    defaultImage:
        opengraph:
            enabled: false
            local: false
            src:

    colorScheme:
        # Display toggle
        toggle: true

        # Available values: auto, light, dark
        default: auto

    imageProcessing:
        cover:
            enabled: true
        content:
            enabled: true

### Custom menu
### See https://docs.stack.jimmycai.com/configuration/custom-menu.html
### To remove about, archive and search page menu item, remove `menu` field from their FrontMatter
menu:
    main: []

    social:
        - identifier: github
          name: GitHub
          url: https://github.com/Shadow-Kylin/Shadow-Kylin.github.io
          params:
              icon: brand-github

        # - identifier: twitter
        #   name: Twitter
        #   url: https://twitter.com
        #   params:
        #       icon: brand-twitter

related:
    includeNewer: true
    threshold: 60
    toLower: false
    indices:
        - name: tags
          weight: 100

        - name: categories
          weight: 200

markup:
    goldmark:
        renderer:
            ## Set to true if you have HTML content inside Markdown
            unsafe: true
    tableOfContents:
        endLevel: 6
        ordered: true
        startLevel: 1
    highlight:
        noClasses: false
        codeFences: true
        guessSyntax: true
        lineNoStart: 1
        lineNos: true
        lineNumbersInTable: true
        tabWidth: 4
```


修改内容区
```bash
cp -r ./themes/hugo-theme-stack/exampleSite/content/categories ./content
cp -r ./themes/hugo-theme-stack/exampleSite/content/page ./content
cp -r ./themes/hugo-theme-stack/exampleSite/content/_index.zh-cn.md ./content
```

运行
运行 hugo server。

初始样子



修改配置和添加文章后的样子



文章位置
主题默认在主页输出 content/post 目录下的内容，应该在那个目录新建文章。



左侧菜单项目
主页，关于，归档，搜索，链接等页面在 content/page/ 目录中有对应的目录。



把对应目录中的 index.md 复制为 index.zh-cn.md, 然后将 index.zh-cn.md 的 front matter 中的 title 修改成对应的中文标题就让侧边栏显示成中文。



主题中的图标
主题自带一些来自 Tabler Icons的图标，它们放在 themes/hugo-theme-stack/assets/icons/ 目录中。

如果要使用自定义图标，把它们放在 assets/icons/ 目录。

front matter是什么：



文章封面
在 front matter 中通过 image 属性定义要使用的封面图片。

image: hugo-logo-wide.svg

这个封面图片放在哪儿？



或者我们封面使用外链也可以。

导入字体
```scss
themes/hugo-theme-stack/assets/scss/style.scss

@import url('https://cdn.jsdelivr.net/npm/lxgw-wenkai-lite-webfont@1.1.0/style.css');
@import url('https://cdn.jsdelivr.net/npm/@fontsource/cascadia-code@4.2.1/index.min.css');

修改字体

themes/hugo-theme-stack/assets/scss/variables.scss

:root {
    --sys-font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Droid Sans", "Helvetica Neue";
    --zh-font-family: "PingFang SC", "Hiragino Sans GB", "Droid Sans Fallback", "Microsoft YaHei";

    --base-font-family: "Lato", var(--sys-font-family), var(--zh-font-family), sans-serif;
    --code-font-family: Menlo, Monaco, Consolas, "Courier New", monospace;
}
```

代码折叠



```html
<!-- 折叠代码 -->

<details class="codefold">
    <summary class="codefold__title">
        <span class="codefold__title-text">
            " {{ with .Get 0}}{{.}}{{else}}click to expand{{ end }} "
        </span>
    </summary>
    {{ .Inner }}
</details>

<!-- 样式 -->
<style>
    .codefold {
        margin: 1.5em 0;
        border: 1px solid #e9edf3;
        /* overflow: hidden; */
        background-color: #f6f8fa;
    }

    .codefold__title {
        padding: 0.5em 1em;
        cursor: pointer;
        user-select: none;
        background-color: #f6f8fa;
    }

    .codefold__title-text {
        flex: 1;
        font-size: 1.2em;
        font-weight: 600;
        color: rgb(215, 178, 130);
        text-decoration: 2px underline;
    }

    .codefold_tip {
        font-size: 1.2em;
        font-weight: 600;
        color: #6280ad;
    }
</style>

<!-- 
    使用格式
    双括号 百分号 codefold 标题 百分号 双括号
    代码
    双括号 百分号 /codefold 百分号 双括号
 -->
 ```




友链三栏
在下面文件夹中的custom.scss中添加后面代码。


```scss
@media (min-width: 1024px) {
    .article-list--compact.links {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;//三栏
        background: none;
        box-shadow: none;
        
        article {
            background: var(--card-background);
            border: none;
            box-shadow: var(--shadow-l2);
            margin-bottom: 8px;
            border-radius: 10px;
            &:nth-child(odd) {//奇数
                margin-right: 8px;
            }
        }
    }
}
```


音乐播放器
使用APlayer播放器。

在partials文件夹下添加music.html：

```html
<!DOCTYPE html>
<html>

<head>
    <!-- require APlayer -->
    <script src="https://cdn.jsdelivr.net/npm/aplayer@1.10.1/dist/APlayer.min.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer@1.10.1/dist/APlayer.min.css">
    <!-- require MetingJS -->
    <script src="https://cdn.jsdelivr.net/npm/meting@2.0.1/dist/Meting.min.js"></script>
    <style>
        .aplayer-body {
            opacity: 0.8;
            color: #030006;
            font-weight: 600;
            box-shadow: 0 2px 10px #5b57ca;
            border-radius: 20px;
        }
    </style>
</head>

<body>
    <div id="aplayer">
    </div>
    <script>
        const ap = new APlayer({
            container: document.getElementById('aplayer'),
            fixed: true,//固定到底部
            theme: '#e9e9e9',
            audio: [
                {
                    name: '歌名',
                    url: '链接',
                    artist: '歌手名',
                    cover: "封面地址"
                },
            ]
        });
    </script>
</body>
```



之后，在footer/custom.html中添加{{partial "music" .}}。

文章评论
使用Waline，其教程很完整。

根据Waline教程从头完成到使用Vercel部署完成。

最后在config.yaml中的waline的serverURL给上你的Vercel服务器地址。

以及开启评论

comments:
        enabled: true
        provider: waline

快速搭建
上面的操作有些儿繁琐，我们可以使用模板快速搭建：CaiJimmy/hugo-theme-stack-starter。

成果
影麟

上面博客里的大部分图片都存在了Github，所以你们可能会获取失败。

参考文章
墨语-Hugo Stack 主题使用方法
建站技术 | 使用 Hugo+Stack 简单搭建一个博客——失迹の博客
（1）带着Stack主题入坑Hugo