本项目是一个基于 Hugo 静态网站生成器和 Stack 主题构建的个人博客/文档网站。

## 技术栈

### 核心组件

- **Hugo**：一个用 Go 语言编写的静态网站生成器，速度快、易用性强
- **Stack 主题**：一个响应式、功能丰富的 Hugo 主题，适合博客和个人网站

### 主要技术

- **Markdown**：用于编写内容的主要标记语言
- **YAML/TOML**：用于配置文件
- **SCSS**：用于样式定制
- **JavaScript/TypeScript**：用于交互功能

## 项目结构

```
E:.
│  .gitmodules                # 记录Git子模块信息
│  .hugo_build.lock           # Hugo构建锁文件，防止并发构建冲突
│  hugo.exe                   # Hugo可执行文件
│  hugo.yaml                  # 主配置文件，包含全站配置参数
│
├─archetypes                  # 内容模板目录
│      default.md             # 默认的文章模板
│
├─assets                      # 静态资源目录（会被Hugo处理）
│  │  jsconfig.json           # JavaScript配置文件
│  │
│  ├─icons                    # SVG图标目录
│  │      bilibili.svg        # B站图标
│  │      GitHub.svg          # GitHub图标
│  │
│  └─img                      # 图片资源目录
│          avatar.png         # 头像文件
│
├─content                     # 网站内容目录
│  │  _index.md               # 首页内容（多语言）
│  │  _index.zh-cn.md         # 中文首页内容
│  │
│  ├─archives                 # 归档页面目录
│  │      _index.md           # 归档页主文件
│  │
│  ├─categories               # 分类目录
│  │  └─Test                  # 测试分类
│  │          _index.md       # 分类描述文件
│  │
│  ├─page                     # 独立页面目录
│  │  ├─about                 # 关于页面
│  │  │      index.md         # 关于页内容
│  │  │      index.zh-cn.md   # 中文关于页
│  │  │
│  │  ├─archives              # 归档页
│  │  │      index.md  
│  │  │
│  │  ├─links                 # 友情链接页
│  │  │      index.md  
│  │  │
│  │  └─search                # 搜索页
│  │          index.md
│  │
│  └─post                     # 博客文章目录
│      ├─class_vue_01         # Vue教程第一章
│      │      index.md        # 文章内容
│      │
│      ├─markdown-syntax      # Markdown语法示例
│      │      index.md
│      │
│      └─math-typesetting     # 数学公式示例
│              index.md
│
├─data                        # 数据文件目录（可用于存储全局数据）
├─i18n                        # 国际化翻译文件目录
├─layouts                     # 布局模板目录（覆盖主题默认布局）
│  │  404.html                # 404页面模板
│  │  index.html              # 首页模板
│  │
│  ├─page                     # 页面级模板
│  │      search.html         # 搜索页模板
│  │      search.json         # 搜索数据模板
│  │
│  ├─partials                 # 局部模板目录
│  │  ├─article               # 文章相关组件
│  │  │  └─components         # 文章子组件
│  │  │          content.html # 文章内容模板
│  │  │          tags.html    # 标签显示模板
│  │  │
│  │  ├─comments              # 评论系统模板
│  │  │  └─provider           # 各评论提供商模板
│  │  │          disqus.html  # Disqus评论模板
│  │  │          waline.html  # Waline评论模板
│  │  │
│  │  ├─widget                # 小工具模板
│  │  │      toc.html         # 目录组件模板
│  │
│  ├─shortcodes               # 短代码目录
│  │      bilibili.html       # B站视频嵌入短代码
│  │      video.html          # 通用视频短代码
│  │
│  └─_default                 # 默认模板目录
│      │  baseof.html         # 基础模板框架
│      │  list.html           # 列表页模板
│      │  single.html         # 单页模板
│
├─public                      # 构建输出目录（自动生成）
│  ├─about                    # 关于页输出
│  ├─archives                 # 归档页输出
│  ├─categories               # 分类页输出
│  ├─post                     # 文章页输出
│  └─tags                     # 标签页输出
│
├─resources                   # 资源缓存目录（Hugo生成）
├─static                      # 静态文件目录（直接复制到public）
│      favicon.ico            # 网站图标
│
└─themes                      # 主题目录
    └─hugo-theme-stack        # Stack主题
        ├─archetypes          # 主题提供的模板
        ├─assets              # 主题静态资源
        ├─i18n                # 主题翻译文件
        └─layouts             # 主题模板文件
```

## 配置文件详解

### 基础配置

```yaml
baseurl: https://YeYingQingYu.github.io  # 网站部署后的根URL
languageCode: en-us                      # 默认语言代码（影响日期格式等）
theme: hugo-theme-stack                  # 使用的主题名称
title: Sandy Memories 丨 沙系             # 网站标题
copyright: Raining Leaves                # 页脚版权信息
```

### 多语言配置

```yaml
DefaultContentLanguage: zh-cn  # 默认内容语言
hasCJKLanguage: true          # 启用中日韩语言支持（优化分词和摘要）

languages:
  zh-hk:                       # 繁体中文配置
    languageName: 繁體中文
    title: Raining Leaves丨葉櫻清雨
    weight: 1                  # 语言菜单排序权重
    params:
      sidebar:
        subtitle: Fall in the dark  # 侧边栏副标题

  zh-cn:                       # 简体中文配置
    languageName: 简体中文
    title: Sandy Memories丨沙系
    weight: 2
    params:
      sidebar:
        subtitle: Fall in the dark
```

### 服务集成

```yaml
services:
  disqus:
    shortname: "hugo-theme-stack"  # Disqus评论系统ID（需替换为你的）
  googleAnalytics:
    id:                           # GA跟踪ID（示例：UA-XXXXX-X）
```

### 内容设置

```yaml
pagination:
  pagerSize: 5  # 分页每页显示文章数

permalinks:
  post: /p/:slug/  # 文章URL格式
  page: /:slug/    # 页面URL格式
```

### 核心配置

#### 主要内容设置

```yaml
params:
  mainSections: ["post"]  # 主内容区显示的分区
  featuredImageField: image  # 文章特色图片的Front Matter字段名
  rssFullContent: true      # RSS输出全文
  favicon: /favicon.ico     # 网站图标路径
```

#### 侧边栏配置

```yaml
sidebar:
  emoji: 🍥                # 侧边栏图标
  subtitle: 欢迎来到我的文档。  # 副标题（支持Markdown）
  avatar:
    enabled: true          # 启用头像
    local: true            # 使用本地图片
    src: img/avatar.png    # 头像路径（相对于static/）
```

#### 文章显示设置

```yaml
article:
  math: false        # 是否启用数学公式
  toc: true          # 显示目录
  readingTime: false # 显示阅读时间
  license:           # 文章许可协议
    enabled: false
    default: CC BY-NC-SA 4.0
```

#### 评论系统

```yaml
comments:
  enabled: false
  provider: disqus  # 可选：disqus/giscus/waline等
  # 各平台详细配置示例：
  waline:
    serverURL: ""   # Waline服务端URL
    emoji: ["https://unpkg.com/@waline/emojis/weibo"]
```

#### 小工具配置

```yaml
widgets:
  homepage:          # 首页小工具
    - type: search   # 搜索框
    - type: archives # 归档列表
      params:
        limit: 5     # 显示5个月
    - type: categories # 分类云
      params:
        limit: 10    # 显示10个分类
```

#### SEO优化

```
opengraph:
  twitter:
    card: summary_large_image  # Twitter卡片样式
defaultImage:                 # 默认分享图片
  opengraph:
    enabled: false
```

#### 外观设置

```yaml
colorScheme:
  toggle: true     # 显示亮/暗模式切换按钮
  default: auto    # 默认模式（auto/light/dark）

imageProcessing:   # 图片处理配置
  cover: true      # 启用封面图处理
  content: true    # 启用内容图片处理
```

### 菜单配置

```yaml
menu:
  main: []  # 主菜单（空数组表示使用自动生成）

  social:    # 社交链接
    - identifier: github
      name: GitHub
      url: https://github.com/YeYingQingYu
      params:
        icon: GitHub  # 使用主题内置图标

    - identifier: bilibili
      name: bilibili
      url: https://space.bilibili.com/1865091
      params:
        icon: bilibili
```

### 高级内容处理

```yaml
markup:
  goldmark:
    extensions:
      passthrough:  # 允许原始HTML和LaTeX
        enable: true
        delimiters:
          block: [ ["\\[", "\\]"], ["$$", "$$"] ]  # 数学公式块
          inline: [ ["\\(", "\\)"] ]               # 行内公式
    renderer:
      unsafe: true  # 允许HTML标签

  tableOfContents:  # 目录设置
    startLevel: 2   # 从h2开始
    endLevel: 4     # 到h4结束

  highlight:        # 代码高亮
    lineNos: true   # 显示行号
    tabWidth: 4     # 缩进空格数
```

### 配置建议与注意事项

**Disqus评论**

   - 将 `disqus.shortname` 替换为你自己的Disqus站点ID。

**多语言优化**

   - 在 `i18n/zh-cn.yaml` 中添加中文翻译
   - 确保内容文件有对应语言后缀（如 `index.zh-cn.md`）

**社交图标**

   - Stack主题内置图标包括：GitHub、Twitter、Instagram等，完整列表参考主题文档。

**启用数学公式**

   ```yaml
params:
  article:
    math: true
   ```

**自定义样式**

   - 在 `assets/scss/custom.scss` 中添加CSS覆盖主题默认样式。

**部署注意事项**

   - 确保 `baseurl` 与GitHub Pages仓库名匹配
   - 构建前执行 `hugo --minify` 优化输出

## 内容编写指南

### 创建新文章

在 `content/post` 目录下新建文件夹和 `index.md` 文件：

```bash
hugo new post/新文章/index.md
```

文章 Front Matter 示例：

```markdown
---
title: "文章标题"
date: 2023-06-15
draft: false
tags: ["标签1", "标签2"]
categories: ["分类"]
image: "图片路径"
---

这里是文章内容...
```

### Markdown 语法示例

#### 基础格式

```markdown
# 一级标题
 二级标题

**粗体** *斜体* ~~删除线~~

[链接文字](https://example.com)

![图片描述](图片路径)
```

#### 代码块

~~~markdown
```javascript
function hello() {
  console.log("Hello World!");
}
```
~~~

#### 表格

```markdown
| 标题1 | 标题2 |
|-------|-------|
| 内容1 | 内容2 |
```

#### 数学公式

```markdown
行内公式: $E=mc^2$

块级公式:
$$
\sum_{i=1}^n i = \frac{n(n+1)}{2}
$$
```



## 自定义修改指南

### 修改主题样式

1. 创建 `assets/scss/custom.scss` 文件
2. 添加自定义样式：

```scss
// 修改主题颜色
:root {
    --primary-color: #3a86ff;
}

// 调整文章样式
.article-content {
    font-size: 1.1rem;
    line-height: 1.8;
}
```

### 添加自定义页面

1. 在 `content/page` 下创建新文件夹，如 `projects`
2. 添加 `index.md`：

```markdown
---
title: "我的项目"
layout: "custom"  # 使用自定义布局
---

 项目列表

- 项目1
- 项目2
```

3. 在 `layouts/page/custom.html` 创建自定义布局

### 多语言支持

1. 在 `i18n` 目录下添加语言文件，如 `zh-cn.yaml`
2. 内容示例：

```yaml
- id: read_more
  translation: "阅读更多"
- id: published
  translation: "发布于"
```

## 项目部署

### 本地预览

```bash
hugo server -D
```

### 构建静态文件

```bash
hugo
```

### 部署到 GitHub Pages

1. 构建静态文件
2. 将 `public` 目录内容推送到 `gh-pages` 分支

## 常见问题解决

### 图片无法显示

- 确保图片路径正确
- 图片放在 `static` 或 `assets/img` 目录下
- 使用相对路径，如 `![描述](/img/avatar.png)`

### 样式不生效

- 检查 SCSS 文件语法
- 确保 Hugo 版本支持 SCSS
- 运行 `hugo server --disableFastRender` 强制刷新

### 多语言切换无效

- 检查 `languages` 配置
- 确保有对应的语言内容文件
- 检查 `i18n` 目录下的翻译文件

## 进阶功能

### 添加评论系统

在 `config.yaml` 中配置：

```yaml
params:
    comments:
        enabled: true
        provider: disqus  # 或 giscus, waline 等
        disqus:
            shortname: "your-disqus-shortname"
```

### 添加分析工具

```yaml
services:
    googleAnalytics:
        id: "UA-XXXXX-X"
```

### 自定义短代码

在 `layouts/shortcodes` 下创建自定义短代码，如 `notice.html`：

```html
<div class="notice {{ .Get 0 }}">
    {{ .Inner }}
</div>
```
