# JSON配置
- app.json  
- project.config.json  
- logs.json  

## app.json
配置例子：
```
{
  "pages": ["pages/index/index", "pages/logs/index"],
  "window": {
    "navigationBarTitleText": "Demo"
  },
  "tabBar": {
    "list": [
      {
        "pagePath": "pages/index/index",
        "text": "首页"
      },
      {
        "pagePath": "pages/logs/logs",
        "text": "日志"
      }
    ]
  },
  "networkTimeout": {
    "request": 10000,
    "downloadFile": 10000
  },
  "debug": true,
  "navigateToMiniProgramAppIdList": ["wxe5f52902cf4de896"]
}
```
| 属性                           | 必填 | 描述                                 |
| ------------------------------ | ---- | ------------------------------------ |
| pages                          | 是   | 页面路径列表                         |
| window                         | 否   | 全局的默认窗口表现                   |
| tabBar                         | 否   | 底部`tab`栏的表现                    |
| networkTimeout                 | 否   | 网络超时时间                         |
| debug                          | 否   | 是否开启`debug`模式，默认为关闭      |
| functionalPages                | 否   | 是否启用插件功能页，默认关闭         |
| subpackages                    | 否   | 分包结构配置                         |
| workers                        | 否   | `Worker`代码放置的目录               |
| requiredBackgroundModes        | 否   | 需要在后台使用的能力，如音乐播放     |
| plugins                        | 否   | 使用到的插件                         |
| preloadRule                    | 否   | 分包预下载规则                       |
| resizable                      | 否   | iPad小程序是否支持屏幕旋转，默认关闭 |
| navigateToMiniProgramAppIdList | 否   | 需要跳转的小程序列表                 |
| usingComponents                | 否   | 全局自定义组件配置                   |
| permission                     | 否   | 小程序接口权限相关设置               |

#### pages
用于指定小程序由哪些页面组成，每一项都对应一个页面的路径+文件名 信息。  
**e.g:**  
目录为：
```
├── app.js
├── app.json
├── app.wxss
├── pages
│   │── index
│   │   ├── index.wxml
│   │   ├── index.js
│   │   ├── index.json
│   │   └── index.wxss
│   └── logs
│       ├── logs.wxml
│       └── logs.js
└── utils
```
app.json中：
```
{
  "pages":["pages/index/index","pages/logs/logs"]
}
```

#### window
用于设置小程序的状态栏、导航条、标题、窗口背景色。  
- navigationBarBackgroundColor:导航栏背景色(十六进制颜色值)
- navigationBarTextStyle:导航栏标题颜色(`black`/`white`)
- navigationBarTitleText:导航栏标题文字内容(`string`)
- backgroundColor:窗口的背景色
- backgroundTxtStyle:下拉loading的样式(`dark`/`light`)
- enablePullDownRefresh:是否开启当前页面的下拉刷新
- onReachBottomDistance:页面上拉触底事件触发时距页面底部距离(单位px)

#### tabBar
若小程序是一个多tab应用（客户端窗口的底部或顶部有tab栏可以切换页面），可以通过tabBar配置项指定tab栏的表现，以及tab切换时显示的对应页面。  
- color:tab上的文字默认颜色(十六进制颜色)
- selectedColor:文字选中时的颜色
- backgroundColor:tab的背景色
- borderStyle
- list
- position
- custom

其中list接受一个数组，只能配置最少2个、最多5个tab。tab按数组的顺序排序，每个项都是一个对象，其属性值：  

| 属性             | 必填 | 说明                          |
| ---------------- | ---- | ----------------------------- |
| pagePath         | 是   | 页面路径，必须在pages中先定义 |
| text             | 是   | tab上按钮文字                 |
| iconPath         | 否   | 图片路径                      |
| selectedIconPath | 否   | 选中时的图片路径              |

#### networkTimeout  
各类网络请求的超时时间，单位为毫秒。


#### debug
可以在开发者工具中开启`debug`模式，在开发者工具的控制台面板，调试信息以`info`的形式给出，其信息有Page的注册，页面路由，数据更新，事件触发等。可以帮助开发者快速定位一些常见的问题。


#### functionalPages
启用插件功能页时，插件所有者小程序需设置为`true`


#### requiredBackgroundModes
申明需要后台运行能力，类型为数组。  
- audio:后台音乐播放


#### permission
小程序接口权限相关设置。

| 属性               | 类型             | 必填 | 描述             |
| ------------------ | ---------------- | ---- | ---------------- |
| scope.userLocation | PermissionObject | 否   | 位置相关权限声明 |

###### PermissionObject结构  
| 属性 | 必填 | 说明                                             |
| ---- | ---- | ------------------------------------------------ |
| desc | 是   | 小程序获取权限时展示的接口用途说明。(最长30字符) |

**e.g:**
```
{
  "pages":["pages/index/index"],
  "permission":{
    "scope.userLocation":{
      "desc":"你的位置信息将用于小程序位置接口的效果展示"
    }
  }
}
```

---
## project.config.json  
###### 使用一个工具时会有一些个性化配置，如界面颜色、编译配置...防止环境变化而重新配置，小程序开发者工具会在每个项目的根目录生成一个`project.config.json`,在工具上做的任何配置都会写入此文件，当环境变化时，只需载入同一项目的代码包即可恢复个性化配置。  
[开发者工具的配置](https://developers.weixin.qq.com/miniprogram/dev/devtools/projectconfig.html)  
**e.g:**
```
{
  "miniprogramRoot": "./src",
  "qcloudRoot": "./svr",
  "setting": {
    "postcss": true,
    "es6": true,
    "minified": true,
    "urlCheck": false
  },
  "packOptions": {
    "ignore": []
  },
  "debugOptions": {}
}
```
---
## page.json
`page.json`用来表示pages/logs目录下的`logs.json`这类和小程序页面相关的配置。  
可以让开发者独立定义每个页面的一些属性。  
#### 页面配置
每个小程序页面都可以使用`.json`文件来对本页面的窗口表现进行配置。  
页面的配置只能设置`app.json`中部分`window`配置项的内容。  
页面中配置项会覆盖`app.json`的`window`中相同的配置项。  
细节：[页面配置](https://developers.weixin.qq.com/miniprogram/dev/framework/config.html)  
**e.g:**
```
{
  "navigationBarBackgroundColor":"#ffffff",
  "navigationBarTextStyle":"black",
  "navigationBarTitleText":"微信接口功能演示",
  "backgroundColor":"#eeeeee",
  "backgroundTxtStyle":"light"
}
```
> `.json`只能设置`window`相关的配置项，以决定本页面的窗口表现，所以无需写`window`属性
---
# WXML模板
`HTML`与`WXML`的不同
- 标签名有些不一样  
将某些组件包装起来，大大提高开发效率。  
小程序`WXML`用的标签是`view`,`button`,`text`等等，这些标签是小程序包装好的基本能力，还提供了地图、视频、音频等组件能力。  
**详细组件参考**[小程序的组件](https://developers.weixin.qq.com/miniprogram/dev/component/)  
- 多了些`wx:if`这样的属性以及`{{}}`这样的表达式  
详细参考[WXML](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxml/index.html)
---
# 页面Page
### Page(Object)构造器
`Page(Object)`函数用来注册一个页面。接受一个`Object`类型参数，其指定页面的初始数据、生命周期回调、时间处理函数等。  
**Object参数说明：**  

| 属性              | 描述                                                                   |
| ----------------- | ---------------------------------------------------------------------- |
| data              | 页面初始数据                                                           |
| onLoad            | 生命周期回调——监听页面加载                                             |
| onShow            | 监听页面显示                                                           |
| onReady           | 监听页面初次渲染完成                                                   |
| onHide            | 监听页面隐藏                                                           |
| onUnload          | 监听页面卸载                                                           |
| onPullDownRefresh | 监听用户下拉动作                                                       |
| onReachBottom     | 页面上拉触底事件的处理函数                                             |
| onShareAppMessage | 用户点击右上角转发                                                     |
| onPageScroll      | 页面滚动触发事件的处理函数                                             |
| onResize          | 页面尺寸改变时触发                                                     |
| onTabItemTap      | 当前是tab页时，点击tab时触发                                           |
| 其他              | 可以添加任意函数或数据到`Object`参数中，在页面的函数中用`this`可以访问 |

**e.g.:**
```
// index.js
Page({
  data: {
    text: 'This is page data.'
  },
  onLoad(options) {
    // Do some initialize when page load.
  },
  onReady() {
    // Do something when page ready.
  },
  onShow() {
    // Do something when page show.
  },
  onHide() {
    // Do something when page hide.
  },
  onUnload() {
    // Do something when page close.
  },
  onPullDownRefresh() {
    // Do something when pull down.
  },
  onReachBottom() {
    // Do something when page reach bottom.
  },
  onShareAppMessage() {
    // return custom share data when user share.
  },
  onPageScroll() {
    // Do something when page scroll
  },
  onResize() {
    // Do something when page resize
  },
  onTabItemTap(item) {
    console.log(item.index)
    console.log(item.pagePath)
    console.log(item.text)
  },
  // Event handler.
  viewTap() {
    this.setData({
      text: 'Set some data for updating view.'
    }, function () {
      // this is setData callback
    })
  },
  customData: {
    hi: 'MINA'
  }
})
```

### data
`data`是页面第一次渲染使用的初始数据。   
**e.g.:**
```
<view>{{text}}</view>
<view>{{array[0].msg}}</view>
```
```
Page({
  data: {
    text: 'init data',
    array: [{msg: '1'}, {msg: '2'}]
  }
})
```
1/21
