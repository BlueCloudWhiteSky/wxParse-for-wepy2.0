# 这是一个wxParse组件，用于wepy2.0
1、下载wxParse的代码[wxParse](https://github.com/icindy/wxParse "wxParse")<br>
2、拷贝本项目 **src/components/** 目录下的 **html2wxml.wpy** 文件<br>
3、在wepy.config.js中加入以下代码<br>
   
    module.exports = {
	  ...
      static: ['src/wxParse/wxParse.wxml']
	  ...
    }
4、引用
```javascript

<template>
  <view class="html-content">
    <html2wxml :content="htmlContent"></html2wxml>
  </view>
</template>

<script>
  import wepy from '@wepy/core'
  wepy.page({
    data: {
      htmlContent: 'html内容'
    }
  })
</script>

<config>
  {
    usingComponents: {
      html2wxml: '~@/components/html2wxml'
    }
  }
</config>

```
组件核心代码：
```javascript
...
<import src="../wxParse/wxParse.wxml" />
<wx-template is="wxParse" data="{{wxParseData: htmlParserTpl.nodes}}"></wx-template>
...
```
因为template标签会被编译成view标签，所以这里需要使用wx-template
这里感谢[#2223](https://github.com/Tencent/wepy/issues/2223 "#2223")给出的解答
至于组件用法也非常简单，接收一个content参数就ok了，若是项目有更丰富的需求，可自行开发。
做这块功能踩了不少坑，今天总结一下发出来希望后面开发这个功能的兄嘚们可以少走点弯路。
### 第三选择：
除了使用wxParse这个组件转html之外，微信也提供了[rich-text](https://developers.weixin.qq.com/miniprogram/dev/component/rich-text.html "rich-text")
但是rich-text目前不支持video标签，具体差异可以看文档，可根据项目需求灵活选择。<br>
相比之下wxParse组件拓展性就强一些，可以支持图片、视频、自定义样式等等<br>
最后如果连组件也懒得写的同学还有一个更简单的路子，就是有个wxParser的第三方插件，直接在公众号上面添加插件引用后就可使用了<br>
戳这里[wxParser](https://mp.weixin.qq.com/wxopen/pluginbasicprofile?action=intro&appid=wx9d4d4ffa781ff3ac&token=1906820051&lang=zh_CN "wxParser")<br>
如果这篇文章帮到了你，可以给个star激励作者分享更多文章

### End
