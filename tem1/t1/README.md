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


onLoad 在页面加载时调用，仅一次；
onShow页面显示/切入前台时触发，两个生命周期非阻塞式调用。
onReady 是页面初始化数据已经完成后调用的，并不意味着onLoad和onShow执行完毕。
调用顺序是onLoad > onShow > onReady



- uni-app参考小程序规范，提供了一批内置组件。\
下为html标签和uni-app内置组件的映射表：\
div 改成 view \
span、font 改成 text \
a 改成 navigator \
img 改成 image \
input 仅仅是输入框。 原html规范中input不仅是输入框，还有radio、checkbox、时间、日期、文件选择功能。在uni-app和小程序规范中，input仅仅是输入框。
其他功能uni-app有单独的组件或API：radio组件、checkbox组件、时间选择、日期选择、图片选择、视频选择、多媒体文件选择(含图片视频)、通用文件选择。 \
form、button、label、textarea、canvas、video 这些还在。 \
select 改成 picker \
iframe 改成 web-view \
ul、li没有了，都用view替代。做列表一般使用uList组件 \
audio 不再推荐使用，改成api方式，背景音频api文档 其实老的HTML标签也可以在uni-app里使用，uni-app编译器会在编译时把老标签转为新标签，比如把div编译成view。但不推荐这种用法，调试H5端时容易混乱。\
- 除了改动外，新增了一批手机端常用的新组件
scroll-view 可区域滚动视图容器 \
swiper 可滑动区域视图容器 \
icon 图标 \
rich-text 富文本（不可执行js，但可渲染各种文字格式和图片） \
progress 进度条 \
slider 滑块指示器 \
switch 开关选择器 \
camera 相机 \
live-player 直播 \
map 地图 \
cover-view 可覆盖原生组件的视图容器 \
cover-view需要多强调几句，uni-app的非h5端的video、map、canvas、textarea是原生组件，层级高于其他组件。如需覆盖原生组件，则需要使用cover-view组件。详见层级介绍


- js api的变化
因为uni-app的api是参考小程序的，所以和浏览器的js api有很多不同，如 \
alert,confirm 改成 uni.showmodel \
ajax 改成 uni.request \
cookie、session 没有了，local.storage 改成 uni.storage \
uni-app的js api还有很多，但基本就是小程序的api，把wx.xxx改为uni.xxx即可
uni-app在不同的端，支持条件编译，无限制的使用各端独有的api，详见条件编译


微信小程序与普通网页区别\
1.运行环境:网页运行在浏览器环境中,小程序运行在微信环境中
2.api:小程序无法调用dombom api。但是她可调用微信环境提供的api:地理定位、扫码、支付
3.开发模式不同
https://mp.weixin.qq.com 立即注册。获取appid:登录后找后台菜单“开发”，点开后就有了。

js
json:app.json project.config.json sitemap.json 每个页面文件夹中的*.json
wxml
wxss


WXML和HTML区别
- 标签名称
 - HTML(div,span,img,a) 
 - WXML(view,text,image,navigator)
- 属性节点
 - <a href="#"></a>
 - <navigator url="/pages/home/home"></navigator>
- 提供了类似于vue中的模版语法
 - 数据绑定
 - 列表渲染
 - 条件渲染

WXSS和CSS区别
- 新增了rpx尺寸单位
 - css需要手动进行像素单位换算，例如rem 
 - WXSS在底层支持新的尺寸单位rpx,在不同大小的屏幕上小程序会自动换算
- 提供了全局样式(app.wxss)和局部样式(xxPage.wxss)
- WXSS仅支持部分css选择器
 - .class #
 - element
 - 并集选择器，后代选择器
 - ::after和::before等伪类选择器

js逻辑交互
- 小程序的js文件分类 
 - app.js
  - 是小程序的入口文件，通过调用App()函数来启动整个小程序 
 - 页面.js
  - 是页面的入口文件，通过调用Page()函数来启动整个小程序
 - 普通的.js
  - 是普通的功能模块文件，封装公共的函数或属性供页面使用,比如utils文件夹里untils.js

宿主环境(host environment):android是安卓软件的宿主环境。它不能再ios环境下运行\
小程序的宿主环境
- 手机微信是小程序的宿主环境
 - 小程序借助宿主环境提供的能力，可以万策划给你普通网页没法完成的功能。比如微信扫码、支付、登录、地理定位等
- 小程序宿主环境包含的内容
 - 通信模型
  - 通信的主体.小程序中的主体是渲染层（WXML、WXSS）和逻辑层(js)
  - 通信模块分2部分
   1) 渲染层和逻辑层的通信:由微信客户端进行转发
   2) 逻辑层和第三方服务器之间的通信:由微信客户端进行转发
 - 运行机制
  - 启动的过程
   1) 把小程序代码包下载到本地
   2) 解析app.json全局配置文件
   3) 执行app.js小程序入口文件，调用App()创建小程序实例
   4) 渲染小程序首页
   5) 小程序启动完成
  - 页面渲染的过程
   1) 加载解析页面.json配置文件
   2）加载页面的.wxml模版和.wxss样式
   3) 执行页面的.js文件，调用Page()创建页面实例
   4) 小程序渲染完成
 - 组件
  - 小程序中的组件也是由宿主环境提供的，官方把小程序组件分为9大类。分别是
   - 视图容器!!:
    1) view: 类似div,块级元素
	2) scroll-view:属性scroll-y允许纵向滚动(此时必须给scroll-view一个固定高度);scroll-x允许横向滚动
	3) swiper和swiper-item
   - 基础内容!!:
    1) text:属性selectable，实现长按选中文本内容。
	2) rich-text：它的nodes属性节点，把html字符串渲染为对应的ui结构。\
	<rich-text nodes="<h1 style='color:red'>标题</h1>"></rich-text>
   - 表单组件!!:
   - 导航组件!!:
   - 媒体组件
   - map地图组件
   - canvas画布组件
   - 开放能力
   - 无障碍访问
   其他常用组件
   - button
    - 功能比html的button按钮丰富
	- 通过open-type属性可以调用微信提供的各种功能（客服、转发、获取用户授权、获取用户信息等）
   - image
    - image组件默认宽度约300px、高度为240px 
	- mode属性用来指定图片的裁剪和缩放模式，常用的mode属性如下
	  - scaleToFill:默认值默认缩放模式
	  - aspectFit:缩放模式，保持纵横缩放图片，也就是可以完成把图片显出来
	  - aspectFill:缩放模式，保持纵横缩放图片只保证图片短边能完全显示出来。也就是只在水平或者垂直方向是完整的，另一个方向会发发生截取
	  - widthFit:缩放模式，宽度不变，高度自动变化，保持原图宽高比不变
	  - heightFit
   - navigator
    - 页面导航组件
	- 类似于html的a链接
 - api
  - 小程序api是宿主环境提供的，通过这些api，可以开发:获取用户信息、本地存储、支付功能等
  - api分三类
   - 事件监听
    1) 特点:以on开头，用来监听某些事件的出发
	2) 举例:wx.onWindowResize(function callback)监听窗口尺寸变化
   - 同步api
    1) 特点1: 以sync结尾的api都是
	2）特点2: 同步api的执行结果，可以通过函数返回值直接获取，如果执行出错会报错
	3) 举例: wx.setStorage('key', 'value')向本地存储导入内容
   - 异步api
    - 特点: 类似于jq的$.ajax()函数，需要通过success,fail,complete接收调用的结果
	- 举例: wx.request发起网络请求，通过sucecss回调函数接收数据。 