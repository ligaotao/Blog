---
title: web打印
date: 2016-10-27 13:48:51
tags: 'js'
---
## web打印

最近由于公司需要打印web页面，需要实现自定义logo 及页头页脚，能够控制打印页面中选中的元素，经过搜索资料现在有三种方案：

1. ie的`ActiveX`的插件
2. 第三方公司的插件，商用是收费且需要安装插件
3. 现代浏览器下的打印pdf

第一第二的方案不能有很好的体验。这里先尝试使用pdf打印的方案，首先需要通过`jsPDF`这个插件将页面元素生成PDF，然后打印pdf

这里需要解决几个问题
- [ ] 自定义logo转base64
- [ ] jsPDF不支持中文问题
- [ ] 位置问题
- [ ] 分页问题


1. logo转base64，可以通过canvas的toDataUrl()接口拿到base64码
2. jsPDF不支持中文，可以看一下原因或者将文字用canvas绘制出来
3. 位置问题需要查看文档，看一下单位换算的问题
4. 分页，需要将最终的图片进行分割，来决定pdf的页数

将以上问题解决后需要完善排版问题

[jsPDF文档](http://rawgit.com/MrRio/jsPDF/master/docs/global.html)
