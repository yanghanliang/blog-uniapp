### 新建项目

> 选择app模板，使用手机调试时需要打开手机usb调试


### pages.json

```md

{
	"pages": [ //pages数组中第一项表示应用启动页，参考：https://uniapp.dcloud.io/collocation/pages
		{
			"path": "pages/index/index",
			"style": {
				"navigationBarTitleText": "uni-app"
			}
		}
	],
	"globalStyle": {
		"navigationBarTextStyle": "black",
		"navigationBarTitleText": "uni-app",
		"navigationBarBackgroundColor": "#F8F8F8",
		"backgroundColor": "#F8F8F8"
	},
	"condition" : { //模式配置，仅开发期间生效
		"current": 0, //当前激活的模式(list 的索引项)
		"list": [
			{
				"name": "", //模式名称
				"path": "", //启动页面，必选
				"query": "" //启动参数，在页面的onLoad函数里面得到
			}
		]
	}
}

```