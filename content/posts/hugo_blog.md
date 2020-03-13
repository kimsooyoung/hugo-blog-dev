---
weight: 1
title: "How to make Hugo Blog like this?? (Hugo + GitHub pages)"
date: 2020-03-12T18:18:59+09:00
lastmod: 2020-03-13T21:29:01+08:00
draft: true
author: "Swimming Kim"
license: "MIT"
description: "Let's make a FULL-FREE blog like this"

tags: ["Hugo", "Blog"]
categories: ["Web"]
hiddenFromHomePage: false

toc: true
autoCollapseToc: false
math: false
lightgallery: true
linkToMarkdown: true
share:
enable: true
comment: true
---

## Hugo 블로그 구축기

> Hugo 설치, Open-Source theme를 사용해서 블로그 구축, GitHub Page로 배포하는 과정을 다룹니다.

<!--more-->

---

<img width="1500" alt="스크린샷 2020-03-12 오후 8 16 46" src="https://user-images.githubusercontent.com/12381733/76516288-7b08b500-649e-11ea-8760-8fdc95ca5ea1.png">
>

---

### 이 블로그를 구축하는 과정을 기록합니다.

1. Hugo의 소개와 설치 및 기본 사용법
2. Hugo의 다양한 open-source theme들 소개
3. 블로그 포스트를 작성하고 로컬 환경에서 실행
4. GitHub Page를 사용해서 무료로 배포!!
5. 배포 이후 유지보수 (새 포스트 추가)

{{< admonition >}}
최대한 많은 분들이 읽으실 수 있도록 단어 선택 및 자세한 설명을 하려 노력하였습니다.
전문 개발자 분들께서 보시기에 너무 쉬울 수도 있어요 :smile::smile:
{{< /admonition >}}

## 1. Hugo의 소개와 설치 및 기본 사용법

> Hugo is a fast and modern static site generator written in Go, and designed to make website creation fun again.

[Hugo](https://gohugo.io/)는 Go언어 기반의 Static Site Generator입니다.

워드프레스, Wix등의 다양한 홈페이지 제작 플랫폼들이 있고, 직접 원하는 기능들을 구현해서 사용하는 개발자분들도 계십니다.

웹 개발의 경험이 많지 않아 이들의 구체적인 차이점은 모르지만, 우선 제가 원했던 홈페이지의 스펙과 기능을 설명드리려 합니다.

---

- 블로그 글쓰기가 손쉽게 가능!
- 최대한 빠르게
- 최대한 예쁘게
- 무료로!!

---

저에게 있어 위 모든 조건을 만족하는 형태가 Hugo + GitHub Page 였습니다.

{{< admonition >}}
단, _블로그 글쓰기가 손쉽게 가능_ 에서 Hugo는 [markdown](https://ko.wikipedia.org/wiki/%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4)문법을 사용하기에, 이에 익숙치 않으신 분은 다소 어려움이 있을 수 있습니다.
{{< /admonition >}}

그럼 지금부터 차근차근 시작해 보겠습니다! :seedling::seedling:

## 1 Requirements

저의 개발 환경은 다음과 같습니다.

- Mac OS Catalina
- Hugo v0.67.0
- [Git 2.21.1](https://git-scm.com/)
- [homebrew](https://brew.sh/index_ko)
- [LoveIt Theme](https://github.com/dillonzq/LoveIt)

{{< admonition note "만약 저와 같은 LoveIt theme을 쓰신다면" >}}
가장 최신 버전의 hugo를 사용하시기 바랍니다. (적어도 v0.62.0이상)
다음은 제가 사용했던 theme의 주의사항입니다.

_Since [Markdown Render Hooks](https://gohugo.io/getting-started/configuration-markup/#markdown-render-hooks) was introduced in the [Hugo Christmas Edition](https://gohugo.io/news/0.62.0-relnotes/), this theme only supports Hugo versions above **v0.62.0**._
{{< /admonition >}}

## 2 Installation

mac OS를 사용하신다면 terminal을 통해 다음과 같이 손쉽게 설치가 가능합니다.

```bash
brew install hugo
```

### 2.1 Create New Hugo Site

첫번째 hugo site를 만들어 봅니다.

원하는 작업 폴더로 이동하신 후 terminal에서 다음의 과정을 따라하시면 됩니다.

```bash
cd <your-working-space-folder>
hugo new site <your-site-name>
cd <your-site-name>
```

위 과정을 거치면 다음과 같은 폴더 구조가 구축됩니다.

```
<your-site-name>
│    config.toml
│
└─── archetypes
│    └─── default.md
│
└─── content
│
└─── data
│
└─── layouts
│
└─── static
│
└─── themes
```

이 중에서 우리가 자주 사용할 부분은 다음과 같습니다.

- config.toml : 홈페이지의 주된 속성들에 대한 configuration이 담기게 됩니다.
- content : 새로운 블로그 글을 쓰게 되면, 해당 포스트가 이곳에 담기게 됩니다.
- themes : 선택한 디자인 theme가 담기게 됩니다.

### 2.2 Clone the Theme

[Hugo Themes](https://themes.gohugo.io/)에는 수많은 다양한 theme들이 있습니다.

무려 오픈소스이기 때문에 copyright만 잘 명시한다면 개인 용도로 얼마든지 사용할 수 있습니다.

저는 [**LoveIt**](https://github.com/dillonzq/LoveIt) 라는 theme을 선택하였습니다.

theme을 사용하기 위해서는

1. 해당 theme의 [최신 배포 버전을 다운 :(far fa-file-archive): .zip file](https://github.com/dillonzq/LoveIt/releases) 받아 프로젝트의 `themes` 폴더에 넣기

2) git을 사용하여 `themes` 폴더 안에 clone하기

```bash
cd themes
git clone -b master https://github.com/dillonzq/LoveIt.git themes/LoveIt
```

3. theme repository를 `<your-site-name>`의 submodule로 두기

```bash
git init
git submodule -b master add https://github.com/dillonzq/LoveIt.git themes/LoveIt
```

### 2.3 Basic Configuration {#basic-configuration}

The following is a basic configuration for the LoveIt theme:

```toml
baseURL = "http://example.org/"
# [en, zh-cn, fr, ...] determines default content language
defaultContentLanguage = "en"
# language code
languageCode = "en"
title = "My New Hugo Site"

# Change the default theme to be use when building the site with Hugo
theme = "LoveIt"

[params]
  # LoveIt theme version
  version = "0.1.X"

[menu]
  [[menu.main]]
    identifier = "posts"
    # you can add extra information before the name (HTML format is allowed), such as icons
    pre = ""
    name = "Posts"
    url = "/posts/"
    # title will be shown when you hover on this menu link
    title = ""
    weight = 1
  [[menu.main]]
    identifier = "tags"
    pre = ""
    name = "Tags"
    url = "/tags/"
    title = ""
    weight = 2
  [[menu.main]]
    identifier = "categories"
    pre = ""
    name = "Categories"
    url = "/categories/"
    title = ""
    weight = 3
```

{{< admonition >}}
When building the website, you can set a theme by using `--theme` option. However, we suggest you modify the configuration file (**config.toml**) and set the theme as the default.
{{< /admonition >}}

### 2.4 Create Your First Post

Here is the way to create your first post:

```bash
hugo new posts/first_post.md
```

Feel free to edit the post file by adding some sample content and replacing the title value in the beginning of the file.

{{< admonition >}}
By default all posts and pages are created as a draft. If you want to render these pages, remove the property `draft: true` from the metadata or set the property `draft: false`.
{{< /admonition >}}

### 2.5 Launching the Website Locally

Launch by using the following command:

```bash
hugo serve
```

Go to `http://localhost:1313`.

![Basic configuration preview](/images/theme-documentation-basics/basic-configuration-preview.png "Basic configuration preview")

{{< admonition tip >}}
When you run `hugo serve`, when the contents of the files change, the page automatically refreshes with the changes.
{{< /admonition >}}

### 2.6 Build the Website

When your site is ready to deploy, run the following command:

```bash
hugo
```

A `public` folder will be generated, containing all static content and assets for your website. It can now be deployed on any web server.

{{< admonition tip >}}
The website can be automatically published and hosted with [Netlify](https://www.netlify.com/) (Read more about [Automated HUGO deployments with Netlify](https://www.netlify.com/blog/2015/07/30/hosting-hugo-on-netlifyinsanely-fast-deploys/)).
Alternatively, you can use [AWS Amplify](https://gohugo.io/hosting-and-deployment/hosting-on-aws-amplify/), [Github pages](https://gohugo.io/hosting-and-deployment/hosting-on-github/), [Render](https://gohugo.io/hosting-and-deployment/hosting-on-render/) and more...
{{< /admonition >}}

## 3 Configuration

### 3.1 Site Configuration {#site-configuration}

In addition to [Hugo global configuration](https://gohugo.io/overview/configuration/) and [menu configuration](#basic-configuration), **LoveIt** lets you define the following parameters in your site configuration (here is a `config.toml`, whose values are default).

{{< admonition >}}
Note that some of these parameters are explained in details in other sections of this documentation.
{{< /admonition >}}

```toml
[params]
  # LoveIt theme version
  version = "0.1.X"
  # site description
  description = "This is My New Hugo Site"
  # site keywords
  keywords = ["Theme", "Hugo"]
  # site default theme ("light", "dark", "auto")
  defaultTheme = "auto"
  # public git repo url only then enableGitInfo is true
  gitRepo = ""
  # LoveIt :(fas fa-greater-than-equal): :(far fa-file-archive): v0.1.1
  # which hash function used for SRI, when empty, no SRI is used ("sha256", "sha384", "sha512", "md5")
  fingerprint = ""
  # Header info
  [params.header]
    # desktop header mode ("fixed", "normal", "auto")
    desktopMode = "fixed"
    # mobile header mode ("fixed", "normal", "auto")
    mobileMode = "auto"
  # Footer Copyright Info
  [params.footer]
    # Site creation time
    since = 2019
    # ICP info only in China (HTML format is allowed)
    icp = ""
    # license info (HTML format is allowed)
    license= '<a rel="license external nofollow noopener noreffer" href="https://creativecommons.org/licenses/by-nc/4.0/" target="_blank">CC BY-NC 4.0</a>'
  # Home Page Info
  [params.home]
    # Home Page Profile
    [params.home.profile]
      enable = true
      # Gravatar Email for preferred avatar in home page
      gravatarEmail = ""
      # URL of avatar shown in home page
      avatarURL = "/images/avatar.png"
      # subtitle shown in home page
      subtitle = "This is My New Hugo Site"
      # whether to use typeit animation for subtitle
      typeit = true
      # whether to show social links
      social = true
    # Home Page Posts
    [params.home.posts]
      enable = true
      # special amount of posts in each home posts page
      paginate = 6
      # default behavior when you don't set "hiddenFromHomePage" in front matter
      defaultHiddenFromHomePage = false
  # Social Info in home page
  [params.social]
    GitHub = "xxxx"
    Linkedin = "xxxx"
    Twitter = "xxxx"
    Instagram = "xxxx"
    Email = "xxxx@xxxx.com"
    Facebook = "xxxx"
    Telegram = "xxxx"
    # Medium = "xxxx"
    # Gitlab = "xxxx"
    Youtubelegacy = "xxxx"
    # Youtubecustom = "xxxx"
    # Youtubechannel = "xxxx"
    # Tumblr ="xxxx"
    # Quora = "xxxx"
    # Keybase = "xxxx"
    # Pinterest = "xxxx"
    # Reddit = "xxxx"
    # Codepen = "xxxx"
    # FreeCodeCamp = "xxxx"
    # Bitbucket = "xxxx"
    # Stackoverflow = "xxxx"
    # Weibo = "xxxx"
    # Odnoklassniki = "xxxx"
    # VK = "xxxx"
    # Flickr = "xxxx"
    # Xing = "xxxx"
    # Snapchat = "xxxx"
    # Soundcloud = "xxxx"
    # Spotify = "xxxx"
    # Bandcamp = "xxxx"
    # Paypal = "xxxx"
    # Fivehundredpx = "xxxx"
    # Mix = "xxxx"
    # Goodreads = "xxxx"
    # Lastfm = "xxxx"
    # Foursquare = "xxxx"
    # Hackernews = "xxxx"
    # Kickstarter = "xxxx"
    # Patreon = "xxxx"
    # Steam = "xxxx"
    # Twitch = "xxxx"
    # Strava = "xxxx"
    # Skype = "xxxx"
    # Whatsapp = "xxxx"
    # Zhihu = "xxxx"
    # Douban = "xxxx"
    # Angellist = "xxxx"
    # Slidershare = "xxxx"
    # Jsfiddle = "xxxx"
    # Deviantart = "xxxx"
    # Behance = "xxxx"
    # Dribble = "xxxx"
    # Wordpress = "xxxx"
    # Vine = "xxxx"
    # Googlescholar = "xxxx"
    # Researchgate = "xxxx"
    # Mastodon = "xxxx"
    # MastodonPrefix = "https://mastodon.technology/"
    # Thingiverse = "xxxx"
    # Devto = "xxxx"
    # Gitea = "xxxx"
    # XMPP = "xxxx"
    # Matrix = "xxxx"
    # Bilibili = "xxxx"

  # Page config
  [params.page]
    # whether to use lightgallery in the page
    lightgallery = true
    # whether to show link to Raw Markdown content of the post
    linkToMarkdown = true
  # mathematical formulas (KaTeX https://katex.org/)
  [params.math]
    enable = true
    # default block delimiter is $$ ... $$ and \\[ ... \\]
    blockLeftDelimiter = ""
    blockRightDelimiter = ""
    # default inline delimiter is $ ... $ and \\( ... \\)
    inlineLeftDelimiter = ""
    inlineRightDelimiter = ""
    # KaTeX extension copy_tex
    copyTex = true
    # KaTeX extension mhchem
    mhchem = true
  # Social Share Links in post page
  [params.share]
    enable = true
    Twitter = true
    Facebook = true
    Linkedin = true
    Whatsapp = true
    Pinterest = true
    # Tumblr = true
    HackerNews = true
    # Reddit = true
    # VK = true
    # Buffer = true
    # Xing = true
    # Line = true
    # Instapaper = true
    # Pocket = true
    # Digg = true
    # Stumbleupon = true
    # Flipboard = true
    # Weibo = true
    # Renren = true
    # Myspace = true
    # Blogger = true
    # Baidu = true
    # Odnoklassniki = true
    # Evernote = true
    # Skype = true
    # Trello = true
    # Mix = true
  # Comment Config
  [params.comment]
    enable = true
    # Disqus Comment Config (https://disqus.com/)
    [params.comment.disqus]
      # LoveIt :(fas fa-greater-than-equal): :(far fa-file-archive): v0.1.1
      enable = false
      # Disqus shortname to use Disqus in posts
      shortname = ""
    # Gitalk Comment Config (https://github.com/gitalk/gitalk)
    [params.comment.gitalk]
      # LoveIt :(fas fa-greater-than-equal): :(far fa-file-archive): v0.1.1
      enable = false
      owner = ""
      repo = ""
      clientId = ""
      clientSecret = ""
    # Valine Comment Config (https://github.com/xCss/Valine)
    [params.comment.valine]
      enable = false
      appId = ""
      appKey = ""
      placeholder = "Your comment ..."
      notify = false
      verify = true
      avatar = "mp"
      meta= ""
      pageSize = 10
      lang = "en"
      visitor = true
      recordIP = true
    # Facebook Comment Config (https://developers.facebook.com/docs/plugins/comments)
    [params.comment.facebook]
      enable = false
      width = "100%"
      numPosts = 10
      appId = ""
      languageCode = "en_US"

  # site verification code for Google/Bing/Yandex/Pinterest/Baidu
  [params.verification]
    google = ""
    bing = ""
    yandex = ""
    pinterest = ""
    baidu = ""
  # Publisher Info just for SEO
  [params.publisher]
    name = "xxxx"
    [params.publisher.logo]
      url = "logo.png"
      width = 127
      height = 40
  # Website Log Info just for SEO
  [params.logo]
    url = "logo.png"
    width = 127
    height = 40
  # Website Image Info just for SEO
  [params.image]
    url = "cover.png"
    width = 800
    height = 600
  # CSS and JS Files CDN
  [params.cdn]
    # fontawesome-free@5.12.1 https://fontawesome.com/
    fontawesomeFreeCSS = ''
    # animate.css@3.7.2 https://github.com/daneden/animate.css
    animateCSS = ''
    # smooth-scroll@16.1.2 https://github.com/cferdinandi/smooth-scroll
    smoothScrollJS = ''
    # sharer@0.4.0 https://github.com/ellisonleao/sharer.js
    sharerJS = ''
    # lazysizes@5.2.0 https://github.com/aFarkas/lazysizes
    lazysizesJS = ''
    # lightgallery@1.1.3 lg-thumbnail@1.1.0 lg-zoom@1.1.0 https://github.com/sachinchoolur/lightgallery.js
    lightgalleryCSS = ''
    lightgalleryJS = ''
    lightgalleryThumbnailJS = ''
    lightgalleryZoomJS = ''
    # typeit@6.5.1 https://github.com/alexmacarthur/typeit
    typeitJS = ''
    # katex@0.11.1 https://github.com/KaTeX/KaTeX
    katexCSS = ''
    katexJS = ''
    katexAutoRenderJS = ''
    katexCopyTexCSS = ''
    katexCopyTexJS = ''
    katexMhchemJS = ''
    # mermaid@8.4.8 https://github.com/knsv/mermaid
    mermaidJS = ''
    # aplayer@1.10.1 https://github.com/MoePlayer/APlayer
    aplayerCSS = ''
    aplayerJS = ''
    # meting@2.0.1 https://github.com/metowolf/MetingJS
    metingJS = ''
    # echarts@4.6.0 https://echarts.apache.org/
    echartsJS = ''
    echartsMacaronsJS = ''
    # gitalk@1.6.2 https://github.com/gitalk/gitalk
    gitalkCSS = ''
    gitalkJS = ''
    # valine@1.3.10 https://valine.js.org/
    valineJS = ''

# Markup related configuration in Hugo
[markup]
  # Syntax Highlighting (https://gohugo.io/content-management/syntax-highlighting)
  [markup.highlight]
    codeFences = true
    guessSyntax = true
    lineNoStart = 1
    lineNos = true
    lineNumbersInTable = true
    noClasses = false
    style = "monokai"
    tabWidth = 4
  # Goldmark is from Hugo 0.60 the default library used for Markdown
  [markup.goldmark]
    [markup.goldmark.extensions]
      definitionList = true
      footnote = true
      linkify = true
      strikethrough = true
      table = true
      taskList = true
      typographer = true
    [markup.goldmark.renderer]
      # whether to use HTML tags directly in the document
      unsafe = true
  # Table Of Contents settings
  [markup.tableOfContents]
    startLevel = 2
    endLevel = 6

# Author Info
[author]
  name = "xxxx"
  link = ""

# Sitemap Info
[sitemap]
  changefreq = "weekly"
  filename = "sitemap.xml"
  priority = 0.5

# Permalinks Info (https://gohugo.io/content-management/urls/#permalinks)
[Permalinks]
  # posts = ":year/:month/:filename"
  posts = ":filename"

# Privacy Info (https://gohugo.io/about/hugo-and-gdpr/)
[privacy]
  [privacy.googleAnalytics]
    anonymizeIP = true

  [privacy.youtube]
    privacyEnhanced = true

# Options to make output .md files
[mediaTypes]
  [mediaTypes."text/plain"]
    suffixes = ["md"]

# Options to make output .md files
[outputFormats.MarkDown]
  mediaType = "text/plain"
  isPlainText = true
  isHTML = false

# Options to make hugo output files
[outputs]
  home = ["HTML", "RSS"]
  page = ["HTML", "MarkDown"]
  section = ["HTML", "RSS"]
  taxonomy = ["HTML", "RSS"]
  taxonomyTerm = ["HTML"]
```

![Complete configuration preview](/images/theme-documentation-basics/complete-configuration-preview.png "Complete configuration preview")

### 3.2 Favicons, Browserconfig, Manifest

It is recommended to put your own favicons:

- apple-touch-icon.png (180x180)
- favicon-32x32.png (32x32)
- favicon-16x16.png (16x16)
- mstile-150x150.png (150x150)
- android-chrome-192x192.png (192x192)
- android-chrome-512x512.png (512x512)

into `/static`. They’re easily created via [https://realfavicongenerator.net/](https://realfavicongenerator.net/).

Customize `browserconfig.xml` and `site.webmanifest` to set theme-color and background-color.

### 3.3 Add Logo and Cover for SEO

Add a logo image (127x40) and a cover image (800x600) in the `static` directory.

### 3.4 Style Customization

**LoveIt** theme has been built to be as configurable as possible by defining custom `.scss` style files.

The directory including the custom `.scss` style files is `config/css` relative to **your project path**.

In `_override.scss`, you can override the variables in `themes/LoveIt/assets/css/_variables.scss` to customize the style.

Here is a example:

```scss
@import url("https://fonts.googleapis.com/css?family=Fira+Mono:400,700&display=swap&subset=latin-ext");
$code-font-family: Fira Mono, Source Code Pro, Menlo, Consolas, Monaco,
  monospace;
```

In `_custom.scss`, you can add some css style code to customize the style.

## 4 Multilingual and i18n

**LoveIt** theme is fully compatible with Hugo multilingual mode.

It provides:

- Translation strings for default values (**English**, **Chinese** and **French**). **Feel free to contribute!**
- In-browser language switching

![Language Switch](/images/theme-documentation-basics/language-switch.gif "Language Switch")

### 4.1 Basic Configuration

After learning [how Hugo handle multilingual websites](https://gohugo.io/content-management/multilingual), define your languages in your [site configuration](#site-configuration).

For example with English, Chinese and French website:

```toml
# [en, zh-cn, fr, ...] determines default content language
defaultContentLanguage = "en"

[languages]
  [languages.en]
    weight = 1
    title = "My New Hugo Site"
    languageCode = "en"
    languageName = "English"
    [[languages.en.menu.main]]
      identifier = "posts"
      pre = ""
      name = "Posts"
      url = "/posts/"
      title = ""
      weight = 1
    [[languages.en.menu.main]]
      identifier = "tags"
      pre = ""
      name = "Tags"
      url = "/tags/"
      title = ""
      weight = 2
    [[languages.en.menu.main]]
      identifier = "categories"
      pre = ""
      name = "Categories"
      url = "/categories/"
      title = ""
      weight = 3

  [languages.zh-cn]
    weight = 2
    title = "我的全新 Hugo 网站"
    # language code, CN only here
    languageCode = "zh-CN"
    languageName = "简体中文"
    # whether to include Chinese/Japanese/Korean
    hasCJKLanguage = true
    [[languages.zh-cn.menu.main]]
      identifier = "posts"
      pre = ""
      name = "文章"
      url = "/posts/"
      title = ""
      weight = 1
    [[languages.zh-cn.menu.main]]
      identifier = "tags"
      pre = ""
      name = "标签"
      url = "/tags/"
      title = ""
      weight = 2
    [[languages.zh-cn.menu.main]]
      identifier = "categories"
      pre = ""
      name = "分类"
      url = "/categories/"
      title = ""
      weight = 3

  [languages.fr]
    weight = 3
    title = "Mon nouveau site Hugo"
    languageCode = "fr"
    languageName = "Français"
    [[languages.fr.menu.main]]
      identifier = "posts"
      pre = ""
      name = "Postes"
      url = "/posts/"
      title = ""
      weight = 1
    [[languages.fr.menu.main]]
      identifier = "tags"
      pre = ""
      name = "Balises"
      url = "/tags/"
      title = ""
      weight = 2
    [[languages.fr.menu.main]]
      identifier = "categories"
      name = "Catégories"
      pre = ""
      url = "/categories/"
      title = ""
      weight = 3
```

Then, for each new page, append the language code to the file name.

Single file `my-page.md` is split in three files:

- in English: `my-page.en.md`
- in Chinese: `my-page.zh-cn.md`
- in French: `my-page.fr.md`

{{< admonition >}}
Be aware that only translated pages are displayed in menu. It’s not replaced with default language content.
{{< /admonition >}}

{{< admonition tip >}}
Use [Front Matter parameter](https://gohugo.io/content-management/multilingual/#translate-your-content) to translate urls too.
{{< /admonition >}}

### 4.2 Overwrite Translation Strings

Translations strings are used for common default values used in the theme. Translations are available in **English**, **Chinese** and **French**, but you may use another language or want to override default values.

To override these values, create a new file in your local i18n folder `i18n/<languageCode>.toml` and inspire yourself from `themes/LoveIt/i18n/en.toml`.

By the way, as these translations could be used by other people, please take the time to propose a translation by [making a PR](https://github.com/dillonzq/LoveIt/pulls) to the theme!
