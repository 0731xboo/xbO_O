---
#frontmatter属性示例 详见:https://theme.sugarat.top/config/frontmatter.html
title: 文章示例   #标题 ,不指定默认去文章的一级标题
description: 这是文章的描述 #描述 text  不指定默认取文章内容前100字
descriptionHTML: '
<span style="color:var(--description-font-color);">1分钟内完成自己的博客创建</span>
<pre style="background-color: #292b30; padding: 15px; border-radius: 10px;" class="shiki material-theme-palenight"><code>
    <span class="line"><span style="color:#FFCB6B;">npm</span><span style="color:#A6ACCD;"> </span><span style="color:#C3E88D;">create</span><span style="color:#A6ACCD;"> </span><span style="color:#C3E88D;">@sugarat/theme@latest</span></span>
</code>
</pre>' #描述  自定义html

# cover:    #封面信息 ,不指定默认取文章中第一章图片
# hiddenCover: true  #控制是否展示文章封面  可全局配置
# hidden: true #控制文章是否出现在首页列表中
# author: xboo #用于单独设置文章的作者信息
# readingTime: true #用于单独设置是否展示文章的预计阅读时间,可全局配置
# date: 2025-08-19 #单独设置文章的发布时间,不设置默认取git取文件的最后修改时间,格式yyyy-MM-dd
# tag: 示例 #用于按标签给文章分类，同时，在文章页标签可点击跳转
# tags: 示例 文章 #效果同tag 
# categories:分类1 #效果同tag
sticky: 1 #用于设置在首页展示的 精选文章，值越大展示越靠前
top: 1 #用于设置在首页置顶展示的文章，从 1 开始，值越小越靠前
recommend: 1 #可用于配置左侧推荐列表数据表现，默认只展示同级目录下的文章
# publish: false #用于控制文章是否发布  等价于hidden: true recommend: false
# buttonAfterArticle:  #用于单独控制某篇文章底部按钮，点击按钮会在按钮下方渲染一个自定义的html内容，例如可以用来做赞赏按钮，内置了 wechatPay 和 aliPay 两个图标，也可自定义图标(svg)。
  # openTitle: 投币
  # closeTitle: 下次一定
  # content: '<img src="https://img.cdn.sugarat.top/mdImg/MTY0Nzc1NTYyOTE5Mw==647755629193">'
  # icon: aliPay
  # size: small
  # expand: true


---


# @sugarat/theme 文章frontmatter属性
详见:[@sugarat/theme frontmatter属性](https://theme.sugarat.top/config/frontmatter.html)

