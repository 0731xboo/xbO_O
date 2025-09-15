---
title: 错误修复记录
description: 日常所碰到的问题修复记录
sticky: 4 #用于设置在首页展示的 精选文章，值越大展示越靠前
top: 4 #用于设置在首页置顶展示的文章，从 1 开始，值越小越靠前
recommend: 4 #可用于配置左侧推荐列表数据表现，默认只展示同级目录下的文章
---

# 日常错误修复记录

## Navigator.clipboard 属性 writeText 方法无法正常调用

### 错误描述
- **错误信息**: `TypeError: Cannot read properties of undefined (reading 'writeText')`
- **场景**: 该错误出现在公司的易读书后台管理系统中，具体网址为 `http://www.readse.com/readse/#/login`

### 问题分析
- **原因**: `Navigator.clipboard.writeText()` 方法只能在安全上下文中使用，即在 HTTPS 协议的网站中。由于当前网站使用的是 HTTP 协议，因此无法调用该方法。

### 解决方案
1. **升级到 HTTPS**: 
   - 将网站从 HTTP 升级到 HTTPS，以确保所有通信都是安全的，并支持使用 `Navigator.clipboard` 方法。

2. **临时解决方案**:
   - 如果暂时无法升级到 HTTPS，可以考虑使用 `document.execCommand('copy')` 作为替代方法。不过需要注意，该方法在现代浏览器中可能会逐步被淘汰。

### 相关资源
- [MDN Web Docs - Clipboard API](https://developer.mozilla.org/en-US/docs/Web/API/Clipboard_API)
- [MDN Web Docs - Using the Clipboard](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Interact_with_the_clipboard)

