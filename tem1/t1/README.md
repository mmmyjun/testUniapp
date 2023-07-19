# uniapp默认模板

## [学习视频](https://ke.qq.com/course/3169971/10920598598344371#term_id=103296764) \
uniapp使用upx作为默认尺寸单位，upx是相对于基准宽度的单位，可根据屏幕宽度进行自适应。\
uniapp规定屏幕基准宽度750upx; \
设计稿1px/设计稿基准宽度=框架样式1upx/750upx，等价于页面元素宽度=750*元素在设计稿中的宽度/设计稿基准宽度 \
Tips:设计稿可以用iphone6(375px)作为视觉稿的标准 \
举例: 如果设计稿宽度640px,元素A在设计稿上的宽度为100px,那么A在uniapp宽度应该为750*100/640=117upx;

网络请求、模版语法、打开页面、页面传参

## 列表到详情接口
### 列表
https://unidemo.dcloud.net.cn/api/news
- 返回数据格式
- id 新闻id 如:7432
- title 标题
- created_at 创建时间
- author_avatar 图标
### 详情
地址:https://unidemo.dcloud.net.cn/api/news/36kr/+id(新闻id,上个页面传过来的)；
使用rich-text【富文本组件】来展示新闻内容；
<rich-text class="richText" :nodes="strings"></rich-text>

"condition" : { //模式配置，仅开发期间生效
	"current": 0, //当前激活的模式(list 的索引项)
	"list": [
		{
			"name": "test", //模式名称
			"path": "pages/info/info", //启动页面，必选
			"query": "newsid=43242" //启动参数，在页面的onLoad函数里面得到
		}
	]
}