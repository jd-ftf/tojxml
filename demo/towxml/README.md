<div align="center"><img width="240" src="https://cdn.rawgit.com/sbfkcel/towxml/78b0886d/logo.svg"/></div>


# TOWXML

**towxml** 是一个可将`HTML`、`markdown`转换为`WXML`(WeiXin Markup Language)的渲染库。

由于微信小程序不能直接渲染`HTML`，因此富文本编辑器生成的`HTML`内容无法直接在小程序中展示。

可能是出于安全因素（XSS），即使`WXML`文本在小程序中也是以字符串方式进行渲染。当然，还是期望之后能开放这样的接口。


## 效果预览


## 特色

- 支持代码语法高亮
- 使用简单
- 多主题动态支持
- 极致的中文排版优化

## 快速上手

**1. 克隆TOWXML到小程序根目录**
```
    git clone https://github.com/sbfkcel/towxml.git
```

**2. 在小程序`app.js`中引入库**
```javascript
    //app.js
    const Towxml = require('/towxml/main');     //引入towxml库
    App({
        onLaunch: function () {
        },
        towxml:new Towxml()                     //创建towxml对象，供小程序页面使用
    })
```

**3. 在小程序页面文件中引入模版**
```html
    <!--pages/index.wxml-->

    <!--引入towxml模版入口文件，并使用模版-->
    <import src="/towxml/entry.wxml"/>
    <template is="entry" data="{{...article}}"/>
```

**4. 在小程序对应的js中请求数据**
```javascript
    //pages/index.js

    const app = getApp();
    Page({
        data: {
            //article将用来存储towxml数据
            article:{}
        },
        onLoad: function () {
            const _ts = this;

            //请求markdown文件，并转换为内容
            wx.request({
                url: 'http://xxx/doc.md',
                header: {
                    'content-type': 'application/x-www-form-urlencoded'
                },
                success: (res) => {
                    //将markdown内容转换为towxml数据
                    let data = app.towxml.toJson(res.data,'markdown');

                    //设置文档显示主题，默认'default'
                    data.theme = 'black';

                    //设置数据
                    _ts.setData({
                        article: data
                    });
                }
            });
        }
    })
```

**5. 引入对应的WXSS**
```css
    /**pages/index.wxss**/

    /**基础风格样式**/
    @import '/towxml/style/main.wxss';


    /**如果页面有动态主题切换，则需要将使用到的样式全部引入**/

    /**主题配色（浅色样式）**/
    @import '/towxml/style/theme/default.wxss';

    /**主题配色（深色样式）**/
    @import '/towxml/style/theme/black.wxss';
```

OK，大功告成~~


## API
如果为了追求极致的体验，建议将`markdown`、`html`转换为**towxml**数据的过程放在服务器上，在小程序中直接请求数据即可。

**1. 依赖环境**

需要 [Node.js](https://www.nodejs.org/) 环境。（已经安装请忽略）


**2. 安装`towxml`**
```
    npm install towxml
```

**3. 接口使用**
```javascript
    const Towxml = require('towxml');
    const towxml = new Towxml();

    //Markdown转WXML
    let wxml = towxml.md2wxml('# Article title');

    //html转WXML
    let wxml = towxml.html2wxml('<h1>Article title</h1>');

    //Markdown转towxml数据
    let data = towxml.toJson('# Article title','markdown');

    //htm转towxml数据
    let data = towxml.toJson('# Article title');
```

## Demo示例
1. 将`towxml/demo`添加为小程序工程
2. 再克隆`towxml`到`demo`目录
3. 使用小程序开发工具编译即可

## License
MIT