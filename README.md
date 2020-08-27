# Tojxml

基于 [towxml](https://github.com/sbfkcel/towxml.git) 项目修改为京东小程序版本。

**Tojxml** 是一个可将`HTML`、`Markdown`转为京东小程序`JXML`(JingDong Markup Language)的渲染库。用于解决在微信小程序中`Markdown`、`HTML`不能直接渲染的问题。

[**官方交流群：182874473（点击加入）**](https://jq.qq.com/?_wv=1027&k=54KTcZi)，进群答案：wiki和issues

## 特色

Tojxml 3.0 完整支持以下功能。当然在构建时可仅保留需要功能以减少体积大小和代码依赖。

- 支持echarts图表（3.0+）✨
- 支持LaTex数学公式（3.0+）✨
- 支持yuml流程图（3.0+）✨
- 支持按需构建（3.0+）✨
- 支持代码语法高亮、代码块行号显示
- 支持emoji表情:wink:
- 支持上标、下标、下划线、删除线、表格、视频、图片（几乎所有html元素）……
- 支持typographer字符替换
- 支持多主题切换
- 支持Markdown TodoList
- 支持事件绑定（这样允许自行扩展功能哟，例如：点击页面中的某个元素，更新当前页面内容等...）
- 极致的中文排版优化
- 支持前后解析数据

## 截图

以下截图即`demo`项目编译的效果

![Tojxml](https://raw.githack.com/sbfkcel/blog/gh-pages/wxml_demo/demo3.x.png)

## 使用说明

### 安装

下载组件代码：

将 `tojxml` 文件夹放到小程序项目根目录中。

### 调用

```html
<tojxml nodes="{{article}}"/>
```

```javascript
import tojxml from '/tojxml/index'

Page({
  data: {
    article: ''
  },
  onLoad () {
    const htmlStr = '<p style="text-align: left;"><span style="font-size:18px;">tojxml是将html、markdown转换为jxml标签</span></p>↵<p style="text-align: left;"><br /></p>↵<p style="text-align: left;"><span style="font-size:18px;color:#ff0000;">使用说明：</span></p><img src="http://img30.360buyimg.com/fwmarket/jfs/t1/114849/26/15546/122752/5f3f38b0E320e107e/249aa63177118eb8.jpg" alt="" width="850">'

    const result = tojxml(htmlStr, 'html')

    this.setData({
      article: result
    })
  }
})
```

### Tojxml Attributes

| 参数      | 说明                                 | 类型      | 可选值       | 默认值   |
|---------- |------------------------------------ |---------- |------------- |-------- |
| nodes | 通过调用 /tojxml/index 的 tojxml 方法生成的标签节点数组 | array | - | - |

### tojxml(str: string, type: string[, options])

- str 必选，html或markdown字符串
- type 必选，需要解析的内容类型html或markdown
- options [object] 可选，可以该选项设置主题、绑定事件、设置base等
  - base [string] 可选，用于指定静态相对资源的base路径。例如：https://xx.com/static/
  - theme [string] 可选，默认:light，用于指定主题'light'或'dark'，或其它自定义
  - events [object] 可选，用于为元素绑定事件。key为事件名称，value则必须为一个函数。例如:{tap:e=>{console.log(e)}}

## License

MIT
