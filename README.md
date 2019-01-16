# 小程序笔记
### JSON配置
- app.json      
`app.json` 指小程序的全局配置。  
例：
        {
        "pages": ["pages/index/index", "pages/logs/logs"],
        "window": {
        "backgroundTextStyle": "light",
        "navigationBarBackgroundColor": "#fff",
        "navigationBarTitleText": "WeChat",
        "navigationBarTextStyle": "black"
        }
        }  
1.`pages`：页面路径列表。
2.`window`:定义小程序所有页面的顶部背景颜色，文字颜色定义等。    
>>>>>>> app.json
