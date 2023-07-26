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



 // 微信小程序 [学习视频](https://www.bilibili.com/video/BV1834y1676P/?p=62&spm_id_from=pageDriver&vd_source=59bd26938eebdd53594d9fc21b805bd3) =====================================================================
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
	  - scaleToFill(默认值):缩放模式,不保持纵横比缩放图片，使图片宽高完全拉伸至填满image元素
	  - aspectFit:缩放模式，保持纵横缩放图片，也就是可以完整把图片显出来
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
    1) 特点:以on开头，用来监听某些事件的触发
	2) 举例:wx.onWindowResize(function callback)监听窗口尺寸变化
   - 同步api
    1) 特点1: 以Sync结尾的api都是同步api
	2）特点2: 同步api的执行结果，可以通过函数返回值直接获取，如果执行出错会报错
	3) 举例: wx.setStorageSync('key', 'value')向本地存储导入内容
   - 异步api
    1) 特点: 类似于jq的$.ajax()函数，需要通过success,fail,complete接收调用的结果
	2) 举例: wx.request发起网络请求，通过sucecss回调函数接收数据。 
	
- 协同工作和发布-协同工作
 - 了解权限管理需求
  - 在中大型公司里，人员分工非常仔细:同一个小程序项目，一般有不同岗位、角色的员工同时参与设计和开发
 - 了解项目成员的组织结构
  - 产品组、设计组、开发组、测试组
 - 小程序开发流程
  - 产品组提出需求=>设计组设计=>开发组开发=>体验(产品组、设计组)=>测试组=>发布
 - 小程序成员管理
  - 管理员 项目成员 体验成员
  - 开发者权限说明
   - 开发设置:设置小程序服务器域名、消息推送和扫描普通链接二维码打开小程序
   - 腾讯云管理:云开发相关设置
  - 添加项目成员和体验成员
   - 后台管理=>成员管理(项目成员、体验成员)
 - 小程序的版本
  - 开发中的不同版本
   1) 开发版本
   2) 体验版本
   3）审核中的版本
   4) 线上版本
 - 发布上线的流程: 上传代码=>提交审核=>发布
  - 上传代码
   1) 点击开发者工具的"上传"按钮，后台查看上传之后的版本\
    后台管理=>版本管理=>开发版本
   2) 填写版本号和项目备注
 - 基于小程序码进行推广
  - 获取的5个步骤: 登录管理后台=>设置=>基本设置=>基本信息=>小程序码和线下物料下载
 - 运营数据
  - 在小程序后台查看：后台=>统计
  - 使用"小程序数据助手"查看：打开微信，搜索"小程序数据助手"


- WXML模版语法-数据绑定
 - 数据绑定基本原则
  - 在data中定义数据
  - 在WXML中使用数据
- WXML模版语法-事件绑定
 - 事件是渲染层到逻辑层的通讯方式
 - 常用事件
  1) tap类型:bindtap或bind:tap; 手触摸后马上离开，类似于html中的click事件
  2) input类型:bindinput或bind:input; 文本框的输入事件
  3) change类型:bindchange或bind:change;状态改变时触发
 - 事件对象的属性列表
  1) type属性:string类型;事件类型
  2) timeStamp:Integet类型;页面打开到触发事件所经过的毫秒数
  3)【target】:Object类型;触发事件的源头组件的一些属性值集合
  4)【currentTarget】:Object类型;当前事件所绑定的组件的一些属性值集合
  5) detail
  6) touches: Array;触摸事件，当前停留在屏幕中的触摸点信息的数组
  7) changedTouches: Array;触摸事件，当前变化的触摸点信息的数组
 - target和currentTarget的区别
  - 比如<view class="outer" bindtag="outerBind"><button>按钮</button></view>,点击button以冒泡方式触发外部outer标签的处理事件.\
  此时e.target指的是触发事件的源头组件button,而e.currentTarget指的是正在触发事件的那个组件outer
 - bindtag的语法格式
 - 在事件处理中为data中的数据赋值;this.setData()\
  data: {count:0}  changeCount() { this.setData({count: this.data.count + 1}) }
 - 事件传参
  - 为组件提供data-*自定义属性传参，其中*是参数名字:<button bindtap="btnHandler" data-info="{{2}}"></button>;data-info="2"的写法传的是字符串的2; \
    在btnHandler中，通过event.target.dataset.参数名 即可获取到具体参数的值。
 - bindinput:
  - <input bindinput="inputHandler"></input>
  - inputHandler(e) {// e.detail.value是变化后，文本框最新的值}
 - 实现文本框和data之间的数据同步
  - 实现步骤
   1) 定义数据
   2) 渲染结构 <input value="{{msg}}" bindinput="iptHandler"></input>
   3) 美化样式
   4) 绑定input事件处理函数\
	iptHandler(e) {// e.detail.value是变化后，文本框最新的值 \
		this.setData({msg: e.detail.value})}
- 条件渲染
 - wx:if wx:elif wx:else
 - 结合<block>使用wx:if
  - 如果想要一次性控制多个组件的显示与隐藏，可以使用一个<block></block>把多个组件包装起来，并在<block>标签上使用wx:if控制属性
 - 直接使用hidden="{{condition}}"也能控制元素的显示与隐藏，频繁切换建议用这个
- 列表渲染 wx:for
 - <view wx:for="{{array}}">索引:{{index}}.item是:{{item}}</view> 
 - 手动指定索引和当前项的变量名*  wx:for-index指定当前循环项的索引的变量名  wx:for-item可以指定当前项的变量名
 - wx:key的使用

- WXSS和CSS
 - rpx:微信小程序独有。实现原理：鉴于不同设备屏幕大小不同，为了实现屏幕的自动适配，rpx把所有设备的屏幕，在宽度上等分为750份(当前屏幕的总宽度为750rpx)
  - 在较小的设备上。1rpx代表的宽度较小.
  - 在较大的设备上。1rpx代表的宽度较大\
  小程序在不同设备上运行的时候，会自动把rpx的样式单位换算成对应的像素单位来渲染，从而实现屏幕适配。
  - rpx与px之间的单位换算
  - 在iphone6,屏幕宽度为375px,共有750个物理像素，等分为750rpx.\
    750rpx=375px=750物理像素\
	1rpx=0.5rpx=1物理像素\
	官方建议：开发微信小程序时，设计师用iphone6为视觉稿的标准\
	开发举例:在iphone6上如果要绘制宽100px,高200px的盒子，换算成rpx单位，宽高分别为200px,400px	
 - @import
 - 全局样式(app.wxss)和局部样式 (页面.wxss)
  - 当局部样式和全局样式冲突，根据就近原则，局部样式会覆盖全局样式
  - 当局部样式的权重>=全局样式的权重时，才会覆盖全局样式

- 全局配置(app.json是小程序的全局配置文件)
 - pages:记录当前小程序所有页面的存放路径
 - window:全局设置小程序窗口的外观：navigationBar导航栏区域、background背景区域（默认不可见，下拉才显示）
 - tabBar:设置小程序底部的tabBar效果
 - style:是否启用新版的组件样式
- window节点常用的配置项
 	"navigationBarTitleText": "Weixin",导航栏标题文字内容 \
	"navigationBarBackgroundColor": "#fff",导航栏背景颜色 \
	"navigationBarTextStyle":"black",导航栏标题颜色，仅支持black/white \
	"backgroundColor": "#fff", 下拉刷新窗口的背景色 \
	"backgroundTextStyle":"light",下拉刷新时loading样式，仅支持dark/light \
	"enablePullDownRefresh": "false",全局开启下拉刷新功能 \
	"onReachBottomDistance": 50，页面上拉触底事件触发时距页面底部举例，单位为px，默认50px
- tabBar:多页面快速切换。顶部 底部
  - 只能配置最少2个，最多5个tab页签
  - 当渲染顶部tabBar时，不显示icon只显示文本
  - 在app.json里tabbar的路径要写最前面
   ```js
    "tabBar": {
		"list": {
			"pagePath": "pages/home/home",
			"text": "首页",
			"iconPath": "/images/tabs/home.png",
			"selectedIconPath": "/images/tabs/home-active.png"
		}
	}
	```
- 小程序的页面配置
 - 页面配置

- 网络数据请求
 - 整你请求https类型的接口
 - 必须将接口的域名添加到信任列表里（合法域名：不能使用ip地址或lcoalhost,域名必须经过ICP备案）
  - 配置request合法域名，后台=>开发=>开发设置=>服务器域名
 - 发起请求
  - wx.request 发起get请求 发起post请求
  - 在页面刚加载时请求数据，此时需要在页面的onLoad事件,this.getData()
  - 跳过request合法域名校验。如果目前只有http协议接口，为了不耽误开发调试，可以先在 微信小程序的详情=>本地设置=>勾选“不校验合法域名...”
  - 跨域和ajax,跨域只存在浏览器中，ajax技术的核心是依赖于浏览器中的xmlhttprequest这个对象，
  - 由于小程序的宿主环境是微信客户端，所以小程序中不能叫做“发起ajax请求”，而是“发起网络数据请求”
	

- 视图与逻辑 页面导航:页面之间相互跳转,浏览器中实现的两种方式:<a>、location.href
 - 小程序两种方式
  - 声明式导航
   - 在页面中声明一个<navigator>导航组件
   - 通过点击<navigator>组件
   - tabBar页面指的是被配置为tabBar的页面 \
    1) 在使用<navigator>组件跳转到指定的tabBar页面时，需要指定url属性和open-type属性，其中:、
	 *url表示要跳转的页面的地址，必须以/开头; \
	 *open-type表示跳转的方式，必须为switchTab\
	 示例代码: <navigator url="/pages/msg/msg" open-type="switchTab">导航到消息页面</navigator>
	2) 导航到非tabBar页面.其中：
	 *url表示要跳转的页面的地址，必须以/开头; \
	 *open-type表示跳转的方式，必须为navigate(默认值!!!，可不写) 
	3) 后退导航
	 - 如果要后退到上一级页面，
	 * <navigator delta="1" open-type="navigateBack"> 其中delta="1"默认是数字1,可省略
  - 编程式导航。调用小程序的导航api，实现页面的跳转
    1) 导航到tabBar页面\
     调用wx.switchTab(object)方法，可以跳转到tabBar页面。其中object参数对象的属性列表如下:\
	 url(需要跳转的tabBar页面路径，路径后不能带参数)、success、fail、complete
	2) 导航到非tabBar页面\
	 调用wx.navigateTo({})
	3) 后退导航\
	 wx.navigateBack(Object)，其中参数对象属性列表如下:\
	 delta(number,默认值1)、success、fail、complete
- 导航传参
 - 声明式导航传参
  1) 参数与路径之间使用?分隔
  2）参数键与参数值用=相连
  3) 不同参数用&分隔
  - <navigator url="/pages/msg/msg?name=zs&age=20" >导航到消息页面</navigator>
 - 编程式导航传参
  wx.navigateTo({url: '/pages/info/info?name=zs&age=20"'})
 - 在onLoad中接收参数:onLoad: function(options)

- 下拉刷新（手指在屏幕上的下拉滑动操作，从而重新加载页面数据的行为），加载更多
 - 全局开启下拉刷新
  - 在app.json window.enablePullDownRefresh:true
 - 局部开启下拉刷新
  - 在页面.json window.enablePullDownRefresh:true =>推荐
 - 监听面的下拉刷新事件
  - 在页面的.js文件中，通过onPullDownRefresh()函数即可监听页面的下拉刷新事件
 - 停止页面的下拉刷新效果
  - onPullDownRefresh(){this.setData({count:0}); wx.stopPullDownRefresh()}

- 上拉触底。手指上拉滑动操作，从而加载更多数据
 - 监听页面的上拉触底事件 onReachBottom()
 - 配置上拉触底距离onReachBottomDistance
- 案例效果
- 添加loading wx.showLoading wx.hideLoading

- 自定义编译模式，每次修改代码都定位到第一个。把普通编译改成"+添加编译模式" \
  模式名称（如pages/msg/msg）、启动页面（如pages/msg/msg）、启动参数
  
  
- 生命周期
 - 应用生命周期：小程序启动=>运行=>销毁
 - 页面生命周期：页面加载=>渲染=>销毁
- 生命周期函数
 - 应用生命周期：小程序启动=>运行=>销毁 调用的函数 ,app.js
 ```js
   App({
	// 小程序初始化完成，执行此函数，全局只触发一次，可以做一些初始化的工作
	 onLaunch: function(options) {},
	 onShow: function(options) {},
	 onHide: function() {},
   })
 ```
 - 页面生命周期：页面加载=>渲染=>销毁 调用的函数。页面.js: onLoad onShow onReady onHide onUnload
 ```js
   Page({
     onLoad: function(options) {// 监听页面加载，每个页面只调用1次
       // Do some initialize when page load.
     },
     onShow: function() {
       // Do something when page show.
     },
     onReady: function() { // 监听页面初次渲染完成，每个页面只调用1次.注意：对界面内容进行设置的 API 如wx.setNavigationBarTitle
       // Do something when page ready.
     },
     onHide: function() {
       // Do something when page hide.
     },
     onUnload: function() {
       // Do something when page close.
     },
     onPullDownRefresh: function() {
       // Do something when pull down.
     },
     onReachBottom: function() {
       // Do something when page reach bottom.
     },
     onShareAppMessage: function () {
       // return custom share data when user share.
     },
     onPageScroll: function() {
       // Do something when page scroll
     },
     onResize: function() {
       // Do something when page resize
     },
     onTabItemTap(item) {
       console.log(item.index)
       console.log(item.pagePath)
       console.log(item.text)
     },
     // Event handler.
     viewTap: function() {
       this.setData({
         text: 'Set some data for updating view.'
       }, function() {
         // this is setData callback
       })
     },
     customData: {
       hi: 'MINA'
     }
   })
 ```
 
- WXS:
 - wxml中无法调用页面.js中定义的函数，但是，wxml可以调用wxs中定义的函数。因此小程序中wxs的典型应用场景就是“过滤器”，配合{{}}使用
 - wxs和js的关系
  - wxs有自己的数据类型
   - number、string、boolean、object、function、array、date、regexp
   - wxs不支持类似于es6及以上的语法
    - 不支持let const、解构赋值、...、箭头函数等等
	- 支持var、function 
   - wxs遵循commonjs规范
    - module对象
	- require()函数
	- module.exports对象
- wxs基础语法
 - 内嵌wsx脚本
```js
<view>{{m1.toUpper(username)}}</view>

<wxs module="m1">
module.exports.toUpper = function(str){
	return str.toUpperCase()
}
</wxs>
```
- 定义外联的wxs脚本. wxs代码还可以编写在以.wxs为后缀名的文件内。\
  // utils/tools.wxs文件
  ```js
  function toLower(str) {
	  return str.toLowerCase()
  }
  module.exports = {
	  toLower: toLower // !!!!!!不可以简写
  }
  ```
- 使用外联wxs脚本:<view>{{m2.toLower(country)}}</view> <wxs src="../../utils/tools.wxs" module="m2"></wxs>
- 隔离性
 1) 不能调用js中定义的函数
 2) 不能调用小程序提供的api
- 性能好
 - 在ios设备上，小程序内的wxs会比js快2-20倍
 - 在android设备上，二者运行效率无差异



- 自定义组件
 - 组件的生命周期 lifetimes
  1) created: 还不能调用setData
  2) attached
  3) ready
  4) moved
  5) detached
  6) error
 - 组件所在页面的生命周期 pageLifetimes
  1) show
  2) hide
  3) resize
- 父子组件之间通信的3种方式
 1) 属性绑定
 2) 事件绑定：子组件js中，通过this.triggerEvent('事件名', '参数对象')，父组件通过e.detail获取子传过来的数据\
  <child count="{{count}}" bind:sync="syncCount"></child>  this.triggerEvent('sync',{value})
  ```js
  addCount() {
	  this.setData({
		  count: this.properties.count + 1
	  })
	  this.triggerEvent('sync',{value: this.properties.count})
  }
  ```
 3) 获取组件实例：父组件通过this.selectComponent获取子组件;
 ```js
 getChild() {
	const child = this.selectComponent('.ca')
	// child.setData({
	// 	count: child.properties.count + 1
	// })
	child.addCount()
 }
 ```
 
- behaviors（实现代码共享的一种方式）:类似于vue中的mixin; 包含一组属性、数据、生命周期函数和方法；\
 - 在pages同级创建一个behaviors文件夹里面存放behaviorsxx.js。
 ```js
 
 ```
 - 在某个组件.js中require('../../behaviors/behaviorsxx')
 ```js
 const myBehavior = require('../../behaviors/behaviorsxx')
 Component({
	 behaviors: [myBehavior]
 })
 ```
 - 组件和引用的behavior中可以包含同名的字段
  - 同名data.
  - 同名属性properties或methods
  - 同名的生命周期函数

- 小程序npm包，使用时有3个限制
 - 不支持依赖于node内置库的包，比如(fs,path)
 - 不支持依赖于浏览器内置对象的包:jquery(window)
 - 不支持依赖于c++插件的包
-npm包-[vant weapp](https://youzan.github.io/vant-weapp) 有赞前端团队开源的小程序ui组件库，使用的是mit开源许可协议
 - 安装vant组件库.主要有以下3步:
  1) 通过npm安装(建议指定版本为@1.3.3)
  2) 构建npm包
  3) 修改app.json
- 安装vant
  1) 找到项目根路径，npm init -y，生成package.json
  2) npm i @vant/weapp@1.3.3 -S --production
  3) 微信开发者程序工具=>构建npm,勾选“使用npm模块”，构建完成后pages同级生成miniprogram_npm文件夹，即可引入组件
  4) 点击详情=>本地设置=>使用npm模块
  5) 把app.json的style: 'v2'去除，小程序的新版基础组件强行加上了许多样式，难以去除，不关闭将造成部分组件样式混乱
- 使用
 - app.json里usingCompnents

- css自定义变量主题色
 - 在app.wxss中写入css变量
 ```js
 page {
	 --button-danger-background-color: red;
	 --button-danger-border-color: green;
 }
 ```
- npm包-API Promise(依赖 miniprogram-api-promise)
 - npm install --save miniprogram-api-promise@1.0.4 会装在pages同级为了确保构建不失败先删除miniprogram_npm文件夹(!!!!!!每次安装新的包后)后，点击工具=>构建，\
此时，miniprogram_npm包重新生成在pages同级，此时文件夹下有@vant和miniprogram-api-promise两个包
```js
// 在小程序入口文件中(app.js),只需调用一次promisifyAll()方法，即可实现异步api的Promise化
import { promisifyAll } from 'miniprogram-api-promise'
const wxp = wx.p = {}
// promisify all wx's api
promisifyAll(wx, wxp)
```
记录解决报错：miniprogram_npm/@vant/weapp/calendar/components/month/index.js 已被代码依赖分析忽略，无法被其他模块引用。你可根据控制台中的【代码依赖分析】告警信息修改代码，或关闭【过滤无依赖文件】功能。详情
解决方案: