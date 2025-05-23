# 小程序
##  小程序学习笔记
小程序学习笔记，看黑马视频总结内容+黑马笔记文件内容
多看官方文档：https://developers.weixin.qq.com/miniprogram/dev/framework/
### 字体图标（借助阿里巴巴矢量图库）
1. 首先先找到所需的图标，鼠标放到图标上点击添加入库（三个小按钮上面的小按钮），然后点页面右上角的购物车图标，点击添加至项目。
2. 添加至项目后右上角小购物车图标里就没有图标了，要点击首页导航栏上面的资源管理-我的项目，点击"font-class"，点击查看在线连接，点击"暂无代码，点击生成"，然后会生成一个css链接，点击这个css链接里面的代码就是这些字体图标的代码。
3. 为了防止一个可能影响调试的报错，在生成css代码前，先在"资源管理-我的项目"页面找到"项目设置"，然后把base64勾选上，再生成css代码
4. 在项目根目录下新建文件夹iconfont/iconfont.wxss文件或iconfont.scss文件，把刚才生成的css代码贴进来
5. 在app.scss中导入全局注册iconfont，注意导入后必须要以分号结尾
``` scss
@import"./iconfont/iconfont.scss";
```
6. 在页面中使用这些图标，在想要添加字体图标的text组件文字前再加一个text组件，给它们添加类名class="字体图标类名"然后保存，即可在页面中生效
``` html
<view class="info">
  <text><text class="iconfont icon-shouye"></text> 同城配送</text>
  <text><text class="iconfont icon-on_time"></text> 行业龙头</text>
  <text><text class="iconfont icon-peisong"></text> 半小时送达</text>
  <text><text class="icon-tubiao_dianzan"></text> 100% 好评</text>
</view>
```
**注意text嵌套text必须在一行，否则会出现图标和字不在同一行的情况**
## 文件
### 主体文件和页面文件
一个完整的小程序项目分为两个部分：主体文件和页面文件
1. 主体文件又称小程序全局文件，顾名思义，全局文件能够作用于整个小程序，影响到小程序的每个页面，主体文件必须放到项目的根目录下，主要由三部分组成：

|  文件名  |       作用       | 是否必须 |
| :------: | :--------------: | :------: |
|  app.js  |  小程序入口文件  |   必须   |
| app.json | 小程序的全局配置 |   必须   |
| app.wxss | 小程序的全局样式 |  非必须  |

2. 页面文件是每个页面所需的文件，小程序页面文件都存放在 pages 目录下，一个页面一个文件夹，每个页面通常由四个文件组成，每个文件只对当前页面有效：

| 文件名 |   作用   | 是否必须 |
| :----: | :------: | :------: |
|  .js   | 页面逻辑 |   必须   |
| .wxml  | 页面结构 |   必须   |
| .wxss  | 页面样式 |  非必须  |
| .json  | 页面配置 |  非必须  |

>  注意：
> 1. 页面文件，wxss、json 文件能够覆盖主体文件中的样式和配置
> 2. 强烈建议：页面文件夹名称和页面文件名称要保持一致

### 新建页面方式
1.  在 pages 目录上 点击右键 `新建文件夹`，输入页面目录的名称，在 list  目录上 点击右键 `点击 page`，输入页面文件的名称
> 注意：
>在输入页面文件名称的时候，不要输入后缀名 
> 新建页面成功以后，会在 app.json 的 pages 选项中新增页面路径

2. 在 app.json 的 pages 选项中，新增页面路径
在新增页面目录以后，会自动在 pages 目录下生成页面文件

## 小程序组件（标签）
### 小程序标签和html区别
1. wxml
`WXML` 类似 `HTML` 的角色，在 `WXML` 中需要用小程序提供的 `view`、`text` 、`image`、`navigator` 等标签来构建页面结构
2. wxss
`WXSS` 类似 `CSS` 的角色，`WXSS` 具有 `CSS` 大部分的特性，小程序在 `WXSS` 也做了一些扩充和修改，新增了尺寸单位 `rpx`、提供了全局的样式和局部样式，`WXSS` 仅支持部分 `CSS` 选择器。
3. rpx
`rpx `:  小程序新增的拓展单位，可以根据屏幕宽度进行自适应，小程序规定任何型号手机：屏幕宽都为 750 rpx。
> 建议：
> iPhone6 的设计稿一般是 750px，小程序的宽是 750rpx
> ​	在我们开发小程序页面时，量取多少px，直接写多少rpx，开发方便，也能适配屏幕的适配
> 原因：
> ​	设计稿宽度是 750px，而 iPhone6 的手机设备宽度是 375px， 设计稿想完整展示到手机中，就需要缩小一倍
> ​	在 iPhone6下，px 和 rpx 的换算关系是：1rpx = 0.5px， 750rpx = 375px，刚好能够填充满整个屏幕的宽度
4. 全局样式和局部样式
全局样式：指在 `app.wxss`中定义的样式规则，作用于每一个页面，例如：设置字号、背景色、宽高等全局样式
局部样式：指在`page.wxss`中定义的样式规则，只作用在对应的页面，并会覆盖 app.wxss 中相同的选择器。
### 轮播图组件swiper
1. `swiper`：滑块视图容器，常用来实现轮播图，其中只可放置 [swiper-item](https://developers.weixin.qq.com/miniprogram/dev/component/swiper-item.html) 组件，否则会导致未定义的行为
2. `swiper-item`：仅可放置在[swiper](https://developers.weixin.qq.com/miniprogram/dev/component/swiper.html)组件中，宽高自动设置为100%，代表 `swiper` 中的每一项
3. 使用 `swiper` 组件提供的属性，实现轮播图的订制，常见属性如下：

|                                         属性                                          |         说明         |              类型               |
| :-----------------------------------------------------------------------------------: | :------------------: | :-----------------------------: |
|                                    indicator-dots                                     |  是否显示面板指示点  |      boolean (默认 false)       |
|                                    indicator-color                                    |      指示点颜色      | color (默认：rgba(0, 0, 0, .3)) |
|                                indicator-active-color                                 | 当前选中的指示点颜色 |      color (默认：#000000)      |
|                                       autoplay                                        |     是否自动切换     |      boolean (默认 false)       |
|                                       interval                                        |   自动切换时间间隔   |       number (默认 5000)        |
|                                       circular                                        |   是否采用衔接滑动   |      boolean (默认 false)       |
| [其他属性...](https://developers.weixin.qq.com/miniprogram/dev/component/swiper.html) |

#### 轮播图代码

```html
<!-- 轮播图区域 -->
<view class="swiper">
  <swiper
    circular
    autoplay
    indicator-dots
    interval="2000"
    indicator-color="#efefef"
    indicator-active-color="#ccc"
  >
    <swiper-item>
      <!-- 在小程序中图片不能使用 img 标签，使用后不会生效 -->
      <!-- <img src="../../assets/banner/banner-1.png" alt=""/> -->

      <!-- 需要使用 images 组件 -->
      <!-- image 组件不给 src 属性设置默认值，也占据宽和高 -->
      <!-- image 默认具有宽度，宽是 320px 高度是 240px -->

      <!-- mode 属性：用来设置图片的裁切模式、纵横比例、显示的位置 -->
      <!-- show-menu-by-longpress 属性：长按转发给朋友、收藏、保存图片 -->
      <image src="../../assets/banner/banner-1.png" mode="aspectFill" show-menu-by-longpress />
    </swiper-item>

    <swiper-item>
      <image src="../../assets/banner/banner-2.png" />
    </swiper-item>

    <swiper-item>
      <image src="../../assets/banner/banner-3.png" />
    </swiper-item>
  </swiper>
</view>

```



`➡️ pages/index/index.scss`

```scss

/** index.wxss **/
page {
  height: 100vh;
  background-color: #efefef !important;
}

swiper {
  height: 360rpx;

  swiper-item {
    image {
      width: 100%;
      height: 100%;
    }

    // 在 Sass 拓展语言中，& 符号表示父选择器的引用。它用于在嵌套的选择器中引用父选择器
    // 下面这段代码在编译以后，生成的代码是 swiper-item:first-child
    // &:first-child {
    //   background-color: skyblue;
    // }

    // &:nth-child(2) {
    //   background-color: lightcoral;
    // }

    // &:last-child {
    //   background-color: lightseagreen;
    // }
  }
}
```


### text 组件
text 是文本组件，类似于 span，是行内元素 
### 页面跳转组件navigator

```html
  <navigator url="/pages/list/list">
    <image src="/assets/cate-2.png" alt=""/>
    <text>鲜花玫瑰</text>
  </navigator>
```

常用的属性有 2 个：
1）url ：当前小程序内的跳转链接
   - 在进行 页面跳转时，需要再路径的前面添加 / 斜线，否则跳转不成功
2）open-type ：跳转方式
   - navigate：保留当前页面，跳转到应用内的某个页面。但是不能跳到 tabbar 页面，保留上一级页面
   - redirect： 关闭当前页面，跳转到应用内的某个页面。但不能跳转到 tabbar 页面，关闭上一级页面
   - switchTab：只能跳转到tabBar页面，不能跳转到非v=tabbar页面，并关闭其他所有非 tabBar 页面
   - reLaunch：关闭所有页面，打开到应用内的某个页面
   - navigateBack：关闭当前页面，返回上一页面或多级页面（delta属性表示返回的层级，默认返回上一个页面dekta=1）
   - 
   - 1.要么写navigate要么啥也不写，因为其余的会关闭页面，你navigateBack不回去
   - 2.tabBar页面不能navigateBack上一页，如要返回使用：switchTab

> 注意：
> 1. 路径后可以带参数。参数与路径之间使用 ? 分隔，参数键与参数值用 = 相连，不同参数用 & 分隔
>    例如：`/list?id=10&name=hua`，在 `onLoad(options)` 生命周期函数 中获取传递的参数 
>
> 2. 属性 `open-type="switchTab"` 时不支持传参
### 可滚动视图区域scroll-view
它可以在小程序中实现类似于网页中的滚动条效果，用户可以通过手指滑动或者点击滚动条来滚动内容，scroll-view 组件可以设置滚动方向、滚动条样式、滚动到顶部或底部时的回调函数等属性，可以根据实际需求进行灵活配置。
#### 横向滚动（scroll-x 属性）
使用横向滚动时，需要添加 scroll-x 属性，然后通过 css 进行结构绘制，实现页面横向滚动
```html
<view class="hot">
  <scroll-view class="scroll-x" scroll-x>
    <view>1</view>
    <view>2</view>
    <view>3</view>
  </scroll-view>
</view>
```
```scss
.hot {
  margin-top: 16rpx;

  .scroll-x {
    width: 100%;
    white-space: nowrap;
    background-color: lightblue;

    view{
      display: inline-block;
      width: 50%;
      height: 80rpx;

      &:last-child{
        background-color: lightseagreen;
      }

      &:first-child{
        background-color: lightpink;
      }
    } 
  }
}
```
#### 纵向滚动（scroll-y 属性）
使用竖向滚动时，需要给[scroll-view](https://developers.weixin.qq.com/miniprogram/dev/component/scroll-view.html)一个固定高度，同时添加  scroll-y 属性，实现页面纵向滚动

```html
<view class="hot">
  <scroll-view class="scroll-y" scroll-y>
    <view>1</view>
    <view>2</view>
    <view>3</view>
  </scroll-view>
</view>
```



`➡️ pages/index/index.wxss`： 

```css
.hot {
  margin-top: 16rpx;

  .scroll-y {
    height: 400rpx;
    background-color: lightsalmon;
    margin-top: 60rpx;

    view {
      height: 400rpx;

      &:nth-child(odd) {
        background-color: lightseagreen;
      }

      &:nth-child(even) {
        background-color: lightcoral;
      }
    }  
  }
}
```
### 背景图片
小程序的样式文件中可以使用 `background-image` 属性来设置一个元素的背景图像，但是小程序的 `background-image` 不支持本地路径。
否则会提示：本地资源图片无法通过 WXSS 获取，可以使用网络图片，或者 base64，或者使用<image/>标签


如果用base64，那么在网上找转化base64的网址转化图片，然后把生成的图片地址写进去，但是这样的地址会特别特别长，如果编译器设置了自动换行那么非常占行
```html
<view class="image"></view>
```
```css
.image {
  width: 100%;
  height: 400rpx;
  /* 错误做法：本地资源图片无法通过 WXSS 获取 */
  /* background-image: url('../../static/微信.jpg'); */

  /* 法1：使用网络图片 */
  /* background-image: url('http://8.131.91.46:6677/TomAndJerry.jpg'); */
    
  /* 法2：使用 base64 格式展示图片 */
  /* base64 编码的文件很长，这个地址老师在这边进行了简写，在测试的时候，需要自己将这里转成完成的 64 编码 */
  background-image: url("data:image/jpeg;base64,/9j/4AAQSkZJRgABAQEAeAB4AAD/.....")
  background-position: center;
  background-size: cover;
}
```
### 其他组件
## 小程序事件系统
小程序中和用户做交互需要编写 `JS` 脚本文件，例如：响应用户的点击、获取用户输入的值等等
### 事件绑定和事件对象
1. 事件绑定
小程序中绑定事件使用 `bind` 方法，`click` 事件也需要使用 `tap` 事件来进行代替，绑定事件的方式有两种，bind+(:)+tap="事件名"：

```html
<button bind:tap="handler">按钮</button>
<button bindtap="handler">按钮</button>
```

事件处理函数需要写到 `.js` 文件中，在 `.js` 文件中需要调用小程序提供的 `Page` 方法来注册小程序的页面，直接在 `Page` 方法中创建事件处理函数

```js
// pages/home/home.js
Page({
  // 页面的初始数据
  data: {},

  // 事件处理程序
  handler () {
    console.log('我被执行啦~~~')
  }
  // 其他 coding...
})
```

2. 当组件触发事件时，绑定的事件的处理函数会收到一个事件对象，用来记录事件发生时的相关信息。在触发事件时，事件处理程序会主动的给我们传入一个参数 —— `event`（事件对象）这个对象里面有很多东西，控制台打印看看，需要什么后面加.获取数据

```js
// pages/home/home.js
Page({
  // 页面的初始数据
  data: {},

  // 事件处理程序
  handler (event) {
    // console.log('我被触发了~~~')
    console.log(event)
  }
    
  // 其他 coding...
})
```
### 冒泡和非冒泡事件
1. 事件分为冒泡事件和非冒泡事件：
冒泡事件：当一个组件上的事件被触发后，该事件会向父节点传递。
非冒泡事件：当一个组件上的事件被触发后，该事件不会向父节点传递。
使用 `bind` 绑定的事件，会触发事件冒泡，如果想阻止事件冒泡，用 `catch` 来绑定事件
```html
<view bindtap="parentHandler">
  <!-- 使用 bind 绑定的事件，会产生事件冒泡 -->
  <!-- <button bindtap="handler">按钮</button> -->

  <!-- 使用 catcht 绑定的事件，会阻止事件冒泡 -->
  <button catchtap="handler">按钮</button>
</view>

```

```js
Page({
  data: {},
  handler (event) {
    console.log('我是子绑定的事件 ~~~')
  },
  parentHandler () {
    console.log('我是父绑定的事件 ~~~')
  }
})
```



2. `WXML` 中冒泡事件列表如下表：

| 类型               | 触发条件                                                                               |
| :----------------- | :------------------------------------------------------------------------------------- |
| touchstart         | 手指触摸动作开始                                                                       |
| touchmove          | 手指触摸后移动                                                                         |
| touchcancel        | 手指触摸动作被打断，如来电提醒，弹窗                                                   |
| touchend           | 手指触摸动作结束                                                                       |
| tap                | 手指触摸后马上离开                                                                     |
| longpress          | 手指触摸后，超过350ms再离开，如果指定了事件回调函数并触发了这个事件，tap事件将不被触发 |
| longtap            | 手指触摸后，超过350ms再离开（推荐使用 longpress 事件代替）                             |
| transitionend      | 会在 WXSS transition 或 wx.createAnimation 动画结束后触发                              |
| animationstart     | 会在一个 WXSS animation 动画开始时触发                                                 |
| animationiteration | 会在一个 WXSS animation 一次迭代结束时触发                                             |
| animationend       | 会在一个 WXSS animation 动画完成时触发                                                 |
| touchforcechange   | 在支持 3D Touch 的 iPhone 设备，重按时会触发                                           |
> ​除上表之外的其他组件自定义事件，如无特殊声明都是非冒泡事件
> 例如 [form](https://developers.weixin.qq.com/miniprogram/dev/component/form.html) 的`submit`事件，[input](https://developers.weixin.qq.com/miniprogram/dev/component/input.html) 的`input`事件
### 事件传参-data-自定义数据
在 wxml 文件中，使用 `data-*` 属性将数据传递给事件处理函数。例如：

```html
<view bindtap="parentHandler" data-parent-id="1" data-parentName="tom">
  <!-- 如果需要进行事件传参，需要再组件上通过 data- 的方式传递数据 -->
  <!-- <button bindtap="btnHandler" data-id="1" data-name="tom">按钮</button> -->
  <button data-id="1" data-name="tom">按钮</button>
</view>
```
在 js 文件中，可以通过 event.currentTarget.dataset 获取传递的数据
```js
Page({
  // 按钮触发的事件处理函数
  btnHandler (event) {
    // currentTarget 事件绑定者，也就是指：哪个组件绑定了当前事件处理函数
    // target 事件触发者，也就是指：哪个组件触发了当前事件处理函数
    // currentTarget 和 target 都是指按钮，因为是按钮绑定的事件处理函数，同时点击按钮触发事件处理函数
    // 这时候通过谁来获取数据都可以
    console.log(event.currentTarget.dataset.id)
    console.log(event.target.dataset.name)
  },

  // view 绑定的事件处理函数
  parentHandler (event) {
    // 点击view区域(不点击按钮)
    // currentTarget 事件绑定者：view
    // target 事件触发者：view
    // currentTarget 和 target 都是指 view，如果想获取 view 身上的数据，使用谁都可以

    // 点击按钮(不点击view区域)
    // currentTarget 事件绑定者：view
    // target 事件触发者：按钮
    // 如果想获取 view 身上的数据，就必须使用 currentTarget 才可以
    // 如果想获取的是事件触发者本身的数据，就需要使用 target
    console.log(event)

    // 在传递参数的时候，如果自定义属性是多个单词，单词与单词直接使用中划线 - 进行连接
    // 在事件对象中会被转换为小托峰写法
    console.log(event.currentTarget.dataset.parentId)

    // 在传递参数的时候，如果自定义属性是多个单词，单词如果使用的是小托峰写法
    // 在事件对象中会被转为全部小写的
    console.log(event.currentTarget.dataset.parentname)
  }

})
```

> 注意：
> ​	使用 `data-` 方法传递参数的时候，多个单词由连字符 `-` 连接
> ​	连字符写法会转换成驼峰写法，而大写字符会自动转成小写字符
> ​	例如：
> ​		`data-element-type` ，最终会呈现为 `event.currentTarget.dataset.elementType `
> ​		`data-elementType` ，最终会呈现为 `event.currentTarget.dataset.elementtype`
### 事件传参-mark 自定义数据
1. 小程序进行事件传参的时候，除了使用 `data-*` 属性传递参数外，还可以使用 `mark` 标记传递参数
`mark`是一种自定义属性，可以在组件上添加，用于来识别具体触发事件的 target 节点。同时 `mark` 还可以用于承载一些自定义数据（类似于 `dataset` ）



2. `mark` 和 `dataset` 很相似，主要区别在于：
`mark` 会包含从触发事件的节点到根节点上所有的 `mark:` 属性值 (事件委托的)

`dataset` 仅包含触发事件那一个节点的 `data-` 属性值。


3. 代码说明：
在 wxml 文件中，使用 `mark:自定义属性` 的方式将数据传递给事件处理函数

```html
<view bindtap="parentHandler" mark:parentid="1" mark:parentname="tom">
  <!-- 如果需要使用 mark 进行事件传参，需要使用 mark:自定义属性的方式进行参数传递 -->
  <!-- <button bindtap="btnHandler" mark:id="1" mark:name="tom">按钮</button> -->
  <button mark:id="1" mark:name="tom">按钮</button>
</view>
```
```js
Page({

  // 按钮绑定的事件处理函数
  btnHandler (event) {
    console.log(event.mark.id)
    console.log(event.mark.name)
  },

  // view 绑定的事件处理函数
  parentHandler (event) {
    // 先点击view区域 (不点击按钮)
    // 通过事件对象获取的是 view 身上绑定的数据

    // 先点击按钮 (不点击view区域)
    // 通过事件对象获取到的是 触发事件的节点以及父节点身上所有的 mark 数据
    console.log(event)
  }
})

```
## 模板语法
### 声明和绑定数据
1. 小程序页面中使用的数据均需要在 Page() 方法的 data 对象中进行声明定义
在将数据声明好以后，需要在 WXML 中绑定数据，数据绑定最简单的方式是使用 Mustache 语法``{{双大括号}}``将变量包起来。
>在``{{双大括号}}``内部可以做一些简单的运算，支持如下几种方式：
>算数运算
>三元运算
>逻辑判断
2. 在 ``{{ }} ``语法中，只能写表达式，不能写语句，也不能调用 js 相关的方法
3. 代码讲解
```html
<!-- 如果需要展示数据，在 wxml 中需要使用双大括号写法将变量进行包裹 -->
<!-- 展示内容 -->
<view>{{ school }}</view>
<view>{{ obj.name }}</view>

<!-- 绑定属性值，如果需要动态绑定一个变量，属性值也需要使用双大括号进行包裹 -->
<view id="{{ id }}">绑定属性值</view>

<!-- 如果属性值是布尔值，也需要使用双大括号进行包裹 -->
<checkbox checked="{{ isChecked }}" />

<!-- 算术运算 -->
<view>{{ id + 1 }}</view>
<view>{{ id - 1 }}</view>

<!-- 三元运算 -->
<view>{{ id === 1 ? '等于' : '不等于' }}</view>

<!-- 逻辑判断 -->
<view>{{ id === 1 }}</view>

<!-- 在双大括号写法内部，只能写表达式，不能写语句，也不能调用 js 的方法 -->
<!-- <view>{{ if (id === 1) {} }}</view> -->
<!-- <view>{{ for (const i = 0; i <= 10; i++) {} }}</view> -->
<view>{{ obj.name.toUpperCase() }}</view>
```

```js
// 对应vxml的.js
Page({
  // 在小程序页面中所需要使用的数据均来自于 data 对象
  data: {
    id: 1,
    isChecked: false,
    school: '西华大学',
    obj: {
      name: '西西'
    }
})
```
### 声明和修改数据
1. 小程序中修改数据并不能直接进行赋值（赋值的方法能够修改数据但不能够更新页面数据），而是要通过调用 `this.setData` 方法才能实现
将需要修改的数据以 `key:value` 的形式传给 `this.setData` 方法。
`this.setData` 方法有两个作用：
1）更新数据
2）驱动视图（页面）数据更新
2. 代码举例：
```js
Page({
  // 页面的初始数据
  data: {
    num: 1
  },

  updateNum() {
    this.setData({
      // key (num)是需要修改的数据
      // value (this.data.num + 1)是最新值
      num: this.data.num + 1
    })
  }
}
```
### setData-修改（增删改）对象类型数据
在实际开发中，我们经常会在 `data` 中声明对象类型的数据，小程序中通过调用 setData 方法可以修改页面的数据，包括对象类型的数据。下面是修改对象类型数据的方法：

1. 先定义一个对象
```js
   Page({
     // 定义页面中使用的数据
     data: {
       userInfo: {
         name: '西西',
         age: 22,
         gender: '女'
       }
     }
   }
```

2. 新增或修改对象中的数据：
```js
//把函数绑定在页面的按钮上，点击页面中的按钮触发函数
updateUserInfo(){
   this.setData({
    //新增单个或多个属性：
     'userInfo.color': 'orange',
     //修改属性值：
     'userInfo.name': '琪琪'
   })
}
   ```
3. 新增或修改数据：使用ES6的展开运算符
在修改对象类型的数据时，可以使用 ES6 的展开运算符(...)先复制对象，然后利用新值对旧值覆盖的方式修改

 ```js
   const userInfo = {
    //把userInfo这个对象的数据复制过来
     ...this.data.userInfo,
     //下面的属性值会覆盖userInfo中同名属性值
     name: 'Jerry',
     age: 100
   }
   
   // 修改对象中的多个属性
   this.setData({
     userInfo:userInfo
     //或userInfo
   })
```
4. 使用 Object.assign 方法合并对象
增加或修改对象中的属性
可以用Object.assign()方法将多个对象合并为一个对象，从后往前合并

``` js
const userInfo = Object.assign(this.data.userInfo,{name:'西西',{age:22})

 this.setData({
     userInfo:userInfo
     //或userInfo
   })
```

5. 使用解构赋值修改对象属性
在修改对象类型的数据时，可以使用解构赋值来修改对象属性
```js
   // 将 userInfo 从 data 中进行解构
   const { userInfo } = this.data
   // 产生一份新数据
   const newUserInfo = {
     ...userInfo,
     name: 'Jerry',
     age: 100
   }
   // 修改对象中的多个属性
   this.setData({
     userInfo: newUserInfo
   })
```
6. 删除对象中的属性
在删除对象中的属性时，**不能**使用 `delete` 操作符，因为小程序的数据绑定机制不支持监听 delete 操作
```js
   // 使用展开运算符拷贝一份数据，产生一个新对象
   const newUser = { ...this.data.userInfo }
   // 使用 delete 删除新对象中的属性
   delete newUser.age
   
   this.setData({
     // 将新的对象进行赋值
     userInfo: newUser
   })
```
7. 注意事项：
小程序的数据绑定机制只能监听到 setData 方法中修改的数据，无法监听到直接删除属性的操作，所以在删除对象属性时，需要先将对象复制一份再进行操作，然后再调用setData方法更新数据。
### setData-修改数组类型数据
数组类型数据也是经常会使用的数据格式之一，下面是修改数组类型数据的方法：
1. 定义一个数组
   ```js
   Page({
     // 定义页面中使用的数据
     data: {
       animalList: ['熊猫', '小狗', '小猫']
     }
   }
   ```
2. 使用数组的push方法新增属性
在修改数组类型的数据时，可以使用数组的 push 方法来添加元素
```js
   //使用数组的push方法来添加元素
   this.data.animalList.push('新增了我哦')
   
   // 使用setData进行赋值，更新视图
   this.setData({
     animalList: this.data.animalList
   })
```
3. 使用数组的concat方法合并数组
在修改数组类型的数据时，可以使用数组的 concat 方法来合并数组
```js
   // 使用 concat 方法来合并数组
   const newList = this.data.animalList.concat('新增了我哦')
   
   // 使用 setData 进行赋值
   this.setData({
     animalList: newList
   })
```
4. 使用 ES6 的展开运算符
使用 ES6 的展开运算符先复制数组，然后进行合并
```js
   // 使用 ES6 的展开运算符(...)先复制数组，然后进行合并
   const newList = [...this.data.animalList, '新增了我哦']
   
   // 使用 setData 进行赋值
   this.setData({
     animalList: newList
   })
```

5. 修改数组中某个元素的值：
利用索引的方式进行修改，但必须使用 wx:for 来进行渲染数组，否则会出现错误
```js
   this.setData({
     'animalList[2]': '修改了我哦' 
     //输入对象里面还有东西，可以这样
    //'animalList[2].name': '修改了我哦' 
   })
```
6. 使用数组的 filter 方法删除元素
```js
   // 使用数组的 filter 方法来删除元素
   //把熊猫筛选出来删掉，其他的组成一个新数组
   const newList = this.data.animalList.filter(item => item !== '熊猫')
   
   // 使用 setData 进行赋值
   this.setData({
     animalList: newList
   })
```
### 数据绑定-简易双向绑定
1. 简易双向绑定机制:在对应值之前加入 `model:` 前缀
```html
<input model:value="{{ value }}" />
<checkbox model:checked="{{isChecked}}"/>是否同意该协议
```
如果输入框的值被改变了，`data` 的数据也会随着改变,同时， WXML 中所有绑定了数据的位置也会被一同更新

> 注意：
> 简易双向绑定的属性值如下限制：
> 1. 只能是一个单一字段的绑定，不支持拼接操作，例如：错误用法：
>``<input model:value="值为 {{value}}" />``
> 2. 不能写data路径，也就是不支持数组和对象，例如：**错误用法**：
>``<input model:value="{{ a.b }}" />``
>``<input model:value="{{ obj.value }}" />``
>`` ``
### 列表渲染-基本使用
1. 列表渲染：就是指通过循环遍历一个数组或对象，将其中的每个元素渲染到页面上
1) 只需要在组件上使用 `wx:for` 属性绑定一个数组，即可使用数组中各项的数据重复渲染该组件
默认数组当前项的变量名默认为 `item`
默认数组的当前项的下标变量名默认为 `index`
2) 注意：在使用 `wx:for` 对数组进行遍历的时候，建议加上 `wx:key` 属性，如不提供 `wx:key`，会报一个 `warning`， 如果明确知道该列表是静态，即以后数据不会改变，或者不必关注其顺序，可以选择忽略

2. `wx:key`可以提升性能
`wx:key`值以两种形式提供：
1) 字符串：代表需要遍历的 array 中 item 的某个 property，该 property 的值需要是列表中唯一的字符串或数字，且不能动态改变
2) 保留关键字 `*this` 代表在 for 循环中的 item 本身，当 item 本身是一个唯一的字符串或者数字时可以使用
wx:key 的属性值不需要使用双大括号进行包裹，直接写遍历的数组 中 item 的某个属性，一般是id

3.  当数据改变触发渲染层重新渲染的时候，会校正带有 key 的组件，框架会确保他们被重新排序，而不是重新创建，以确保使组件保持自身的状态，并且 **提高列表渲染时的效率** 

4. 代码示例
``` html
<!--每一项的变量名默认是 item -->
<!--每一项下标(索引)的变量名默认是 index -->
<!--如果渲染的是数组，item:数组的每一项，index:下标-->
<view wx:for="{{ numList }}">{{ item }}-{{ index }}</view>
<!--如果渲染的是对象，item:对象属性的值，index:对象属性-->
<view wx:for="{{ obj }}">{{ item }}-{{ index }}</view>
```
5. 渲染多节点结构块：
如果需要渲染一个包含多节点的结构块，可以使用一个 `<block/>` 标签将多个组件包装起来

```html
<block wx:for="{{ animal }}">
  <view>
    <span>{{ item.name }}</span>
    <span>{{ item.avatar }}</span>
  </view>
</block>
```
>注意：
> `<block/>` 并不是一个组件，它仅仅是一个包装元素，不会在页面中做任何渲染，只接受控制属性。

### 条件渲染
1. 条件渲染主要用来控制页面结构的展示和隐藏，在微信小程序中实现条件渲染有两种方式：
1) 使用 `wx:if`、`wx:elif`、`wx:else` 属性组
2) 使用 `hidden` 属性：hidden 属性属性值如果是true会隐藏结构，如果是 false会展示结构

2. `wx:if` 和 `hidden` 二者的区别：
- `wx:if` ：当条件为 `true` 时将内容渲染出来，否则元素不会进行渲染，通过移除/新增节点的方式来实现
- `hidden` ：当条件为 `true` 时会将内容隐藏，否则元素会显示内容，通过css的 `display` 样式属性来实现的

3. 代码演示
```html
<!-- 使用 wx:if、wx:elif、wx:else 属性组控制元素的隐藏和控制 -->
<view wx:if="{{ num === 1 }}">num 等于 {{ num }}</view>
<view wx:elif="{{ num === 2 }}">num 等于 {{ num }}</view>
<view wx:else>大于 2</view>

<!-- 使用hidden属性组控制元素的隐藏和控制 -->
<view hidden="{{ num !== 1 && num !== 2 && num !== 3 && num < 3}}">
  {{ num < 3 ? 'num 等于' + num : '大于 2' }}
</view>

<button type="primary" bindtap="updateNum">修改数据</button>
```

```js
Page({
  // 页面的初始数据
  data: {
    num: 1
  },
  // 更新数据
  updateNum() {
    this.setData({
      num: this.data.num + 1
    })
  }
}
```
## 小程序的生命周期
### 小程序运行机制
1. 冷启动与热启动：
小程序启动可以分为两种情况，一种是冷启动，一种是热启动
1) 冷启动：如果用户首次打开，或小程序销毁后被用户再次打开，此时小程序需要重新加载启动

2) 热启动：如果用户已经打开过某小程序，然后在一定时间内再次打开该小程序，此时小程序并未被销毁，只是从后台状态进入前台状态
2. 前台与后台状态：
1) 小程序启动后，界面被展示给用户，此时小程序处于「前台」状态。

2) 当用户「关闭」小程序时，小程序并没有真正被关闭，而是进入了「后台」状态，当用户再次进入微信并打开小程序，小程序又会重新进入「前台」状态

> 切后台的方式包括但不限于以下几种：
> - 点击右上角胶囊按钮离开小程
> - 安卓点击返回键离开小程序
> - 屏幕左侧右滑离开小程序
3. 挂起：
小程序进入「后台」状态一段时间后（5 秒），微信停止小程序 JS 线程执行，小程序进入「挂起」状态，当开发者使用了后台播放音乐、后台地理位置等能力时，小程序可以在后台持续运行，不会进入到挂起状态
4. 销毁：
如果用户很久没有使用小程序，或者系统资源紧张，小程序会被销毁，即完全终止运行。

当小程序进入后台并被「挂起」后，如果很长时间（目前是 30 分钟）都未再次进入前台，小程序会被销毁

当小程序占用系统资源过高，可能会被系统销毁或被微信客户端主动回收。
### 小程序更新机制
1. 理解
在访问小程序时，微信会将小程序代码包缓存到本地。
开发者在发布了新的小程序版本以后，微信客户端会检查本地缓存的小程序有没有新版本，并进行小程序代码包的更新。
2. 小程序的更新机制有两种：启动时同步更新和启动时异步更新
1) 启动时同步更新（能覆盖%99的用户）：
微信运行时，会定期检查最近使用的小程序是否有更新。如果有更新，下次小程序启动时会同步进行更新，更新到最新版本后再打开小程序。如果 用户长时间未使用小程序时，会强制同步检查版本更新
2) 启动时异步更新（同步更新没被覆盖到的）
启动时异步更新：在启动前没有发现更新，小程序每次 冷启动 时，都会异步检查是否有更新版本。如果发现有新版本，将会异步下载新版本的代码包，**将新版本的小程序在下一次冷启动进行使用**，当前访问使用的依然是本地的旧版本代码

3. 在启动时异步更新的情况下，如果开发者希望立刻进行版本更新，可以使用API 进行处理。在有新版本时提示用户重启小程序更新新版本。API[wx.getUpdateManager](https://developers.weixin.qq.com/miniprogram/dev/api/base/update/wx.getUpdateManager.html) 
视频有举例的代码，但是具体怎么搞还是要看官方文档

### 小程序生命周期
1. 初步理解
应用生命周期是指应用程序进程从创建到消亡的整个过程
小程序的生命周期指的是 小程序从启动到销毁的整个过程
2. 仔细理解
在打开一个小程序应用的时候都需要经历一系列的初始化步骤，比如页面是否加载完成、页面是否初次渲染完成等等。
在此过程中，小程序会运行生命周期钩子的函数，这些函数由小程序框架本身提供，被称为生命周期函数，生命周期函数会按照顺序依次自动触发调用，帮助程序员在特定的时机执行特定的操作，辅助程序员完成一些比较复杂的逻辑。让开发者有机会在特定阶段运行自己的代码。
3. 小程序的生命周期分类：
分为三类：应用别级、页面级别和组件级别种类型
#### 应用生命周期
1. 简单理解：
应用生命周期通常是指一个小程序从 启动 → 运行 → 销毁的整个过程
2. 应用生命周期函数理解
应用生命周期伴随着一些函数，称为应用生命周期函数，应用生命周期函数需要 在 app.js 文件的 App() 方法中定义
理解：当整个小程序应用运行到某个时机的时候，我们需要做一些事情。例如：当小程序启动成功之后，我们要获取小程序的一些信息，就可以在小程序启动成功时的钩子函数中写代码获取我们想要的信息
3. 应用生命周期函数组成
应用生命周期函数由 onLaunch（小程序初始化，只会在冷启动的时候执行一次）、onShow（小程序冷启动或切前台执行）、onHide（小程序切后台执行）三个函数组成。
启动小程序 → onLaunch → onShow → onHide
注意：当小程序切后台被挂起后，如果在三分钟以内切回前台（热启动），那么会再次执行onShow；如果是小程序被销毁或者挂起的事件太久（30分钟以上），那么切回前台会重新启动小程序然后执行onLaunch再执行onShow
4. 代码如何写
在app.js文件中输入app，选带方框的App按回车，会自动生成上面这三个钩子函数
如：app.js
```js
App({
  /**
   * 当小程序初始化完成时，会触发 onLaunch（全局只触发一次）
   */
  onLaunch: function () {
    // 监听小程序初始化
    console.log('onLaunch: 当小程序初始化完成时，会触发 onLaunch')
  },

  /**
   * 当小程序启动，或从后台进入前台显示，会触发 onShow
   */
  onShow: function (options) {
    // 监听小程序的显示
    console.log('onShow: 当小程序启动，或从后台进入前台显示')
  },

  /**
   * 当小程序从前台进入后台，会触发 onHide
   */
  onHide: function () {
    // 监听小程序的隐藏
    console.log('onHide: 小程序从前台进入后台')
  }
})

```
#### 页面生命周期
1. 简单理解：
页面生命周期就是指小程序页面从 加载 → 运行 → 销毁的整个过程
2. 页面生命周期函数理解：
当某个页面运行到某个时机的时候，我们需要做一些事情，例如: 当某个页面加载完毕之后，需要发请求获取当前页面所需的数据，就可以在对应的页面加载完成后的钩子函数中执行发送请求的代码。
小程序中的一个页面都需要在对应页面的 `.js` 文件中调用 `Page()` 方法来注册。`Page()` 接受一个 `Object` 类型参数，其指定页面的初始数据、生命周期回调、事件处理函数等。
3. 应用生命周期函数组成：
1) [onLoad](https://developers.weixin.qq.com/miniprogram/dev/reference/api/Page.html#onLoad-Object-query) 页面加载时触发 (一个页面只会调用一次) 
2) [onShow](https://developers.weixin.qq.com/miniprogram/dev/reference/api/Page.html#onShow) 页面显示时触发，页面显示/切入前台时触发    
3) [onReady](https://developers.weixin.qq.com/miniprogram/dev/reference/api/Page.html#onReady)  页面初次渲染完成时触发(一个页面只会调用一次)<br />代表页面已经准备妥当，可以和视图层进行交互 
4)  [onHide](https://developers.weixin.qq.com/miniprogram/dev/reference/api/Page.html#onHide)  页面隐藏/切入后台时触发             |
5) [onUnload](https://developers.weixin.qq.com/miniprogram/dev/reference/api/Page.html#onUnload)     页面卸载时触发                    

4. 代码演示
```js
// pages/home/home.js
Page({
   
  // coding...
    
  // 生命周期函数--监听页面加载
  onLoad: function (options) {
    console.log('页面加载完毕')
  },

  // 生命周期函数--监听页面显示
  onShow: function () {
    console.log('监听页面显示，此时页面处于显示状态')
  },

  // 生命周期函数--监听页面初次渲染完成
  onReady: function () {
    console.log('页面初次渲染已经完成')
  },

  // 生命周期函数--监听页面隐藏
  onHide: function () {
    console.log('当前页面处于隐藏状态')
  },

  // 生命周期函数--监听页面卸载
  onUnload: function () {
    console.log('页面卸载时触发')
  }
})
```
#### 生命周期补充说明（两个细节）
1. tabBar 页面之间相互切换，页面不会被销毁
2. 点击左上角，返回上一个页面，会销毁当前页面(被打开页面)

## 小程序的API
### API 基础
[小程序 API 介绍](https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/api.html)
[微信小程序 API 文档](https://developers.weixin.qq.com/miniprogram/dev/api/)
1. 小程序API通常有以下几种类型：
1) 事件监听 API：
约定以 `on` 开头 API 用来监听某个事件是否触发，例如：`wx.onThemeChange()`
2) 同步 API：
约定以 `Sync` 结尾的 API 都是同步 API，例如：`wx.setStorageSync()`
3) 异步 API：
大多数 API 都是异步 API，例如：`wx.setStorage()`
2. 异步 API 支持 callback & Promise 两种调用方式：
1) 当接口参数 Object 对象中不包含 success/fail/complete 时将默认返回 Promise

2) 部分接口如 request, uploadFile 本身就有返回值，因此不支持 Promise 风格的调用方式，它们的 promisify 需要开发者自行封装。
### 网络请求
1. wx.request()
在微信小程序中,发起 HTTPS 网络请求需要使用：`wx.request()`，语法如下：
```js
wx.request({
  // 接口地址，仅为示例
  url: 'https://jsonplaceholder.typicode.com/posts/1',
  // 请求的参数
  data: { x: '' },
  // 请求方式
  method: 'GET|POST|PUT|DELETE',
  success (res) {
    console.log(res.data)
  },
  fail(err) {
    console.log(err)
  }
})
```
2. 注意：
wx.request() 请求的域名需要在小程序管理平台进行配置(打开微信公众后台：点击左侧 开发 → 开发管理 → 开发设置 → 服务器域名。域名只支持 `https` 而且要求已备案)，如果小程序正式版使用wx.request请求未配置的域名，在控制台会有相应的报错。

3. 开发阶段设置：
处于开发阶段的服务器接口可能还没部署到对应的域名下，开发者工具、小程序的开发版和小程序的体验版在某些情况下允许 `wx.request` 请求任意域名 (只适用于开发环境，只能在小程序开发者工具中生效)，在开发工具中设置步骤如下：
打开微信开发者工具-右上角详情-本地设置-将`不校验合法域名、web-view (业务域名)、TLS版本以及HTTPS证书`勾选
### 界面交互
小程序提供了一些用于界面交互的API，如消息提示框、模态对话框、 loading 提示框等等
#### loading 提示框
1. loading提示框api和官方文档
loading 提示框常配合网络请求来使用，用于增加用户体验，对应的 API 有两个：
1) `wx.showLoading` 显示加载提示框
2) `wx.hideLoading` 隐藏加载提示框
[wx.showLoading 官方文档](https://developers.weixin.qq.com/miniprogram/dev/api/ui/interaction/wx.showLoading.html)

[wx.hideLoading 官方文档](https://developers.weixin.qq.com/miniprogram/dev/api/ui/interaction/wx.hideLoading.html)

```js
wx.showLoading({
  title: '提示内容', // 提示的内容
  mask: true, // 是否显示透明蒙层，防止触摸穿透
  success() {}, // 接口调用成功的回调函数
  fail() {} // 接口调用失败的回调函数
})
```

2. 代码示例
```js
Page({

  data: {
    list: []
  },

  // 获取数据
  getData () {

+     // 显示 loading 提示框
+     wx.showLoading({
+       // 用来显示提示的内容
+       // 提示的内容不会自动换行，如果提示的内容比较多，因为在同一行展示
+       // 多出来的内容就会被隐藏
+       title: '数据加载中...',
+       // 是否展示透明蒙层，防止触摸穿透
+       mask: true
+     })

    // 如果需要发起网络请求，需要使用 wx.request API
    wx.request({
      // 接口地址
      url: 'https://gmall-prod.atguigu.cn/mall-api/index/findBanner',
      // 请求方式
      method: 'GET',
      // 请求参数
      data: {},
      // 请求头
      header: {},
      // API 调用成功以后，执行的回调
      success: (res) => {
        // console.log(res)
        if (res.data.code === 200) {
          this.setData({
            list: res.data.data
          })
        }
      },
      // API 调用失败以后，执行的回调
      fail: (err) => {
        console.log(err)
      },
      // API 不管调用成功还是失败以后，执行的回调
      complete: (res) => {
        // console.log(res)

+         // 关掉 loading 提示框
+         // hideLoading 和 showLoading 必须结合、配对使用才可以
+         wx.hideLoading()
      }
    })

  }

})

```
#### 模态对话框以及消息提示框
1. 模态提示框api和官方文档
1) `wx.showToast()`：消息提示框用来根据用户的某些操作来告知操作的结果，如退出成功给用户提示，提示删除成功等，语法如下：
```js
wx.showToast({
  title: '标题', // 提示的内容
  duration: 2000, // 提示的延迟时间
  mask: true, // 是否显示透明蒙层，防止触摸穿透
  icon: 'success', // 	图标
  success() {}, // 接口调用成功的回调函数
  fail() {} // 接口调用失败的回调函数
})
```

2) `wx.showModal()` 模态对话框也是在项目中频繁使用的一个小程序 `API`，通常用于向用户询问是否执行一些操作，例如：点击退出登录，显示模态对话框，询问用户是否真的需要退出等等

```js
wx.showModal({
  title: '提示', // 提示的标题
  content: '您确定执行该操作吗？', // 提示的内容
  confirmColor: '#f3514f',
  // 接口调用结束的回调函数（调用成功、失败都会执行）
  success({ confirm }) {
    confirm && consle.log('点击了确定')
  }
})
```

官方文档：
[wx.showToast 官方文档](https://developers.weixin.qq.com/miniprogram/dev/api/ui/interaction/wx.showToast.html)

[wx.showModal 官方文档](https://developers.weixin.qq.com/miniprogram/dev/api/ui/interaction/wx.showModal.html)

2. 代码示例
```js
Page({
  // 删除商品
  async delHandler () {
    // showModal 显示模态对话框
    const { confirm } = await wx.showModal({
      title: '提示',
      content: '是否删除该商品 ?'
    })

    if (confirm) {
      // showToast 消息提示框
      wx.showToast({
        title: '删除成功',
        icon: 'none',
        duration: 2000
      })
    } else {
      wx.showToast({
        title: '取消删除',
        icon: 'error',
        duration: 2000
      })
    }

  }
})
```
### 本地存储
1. 理解
小程序中也能够像网页一样支持本地数据缓存，本地数据缓存是小程序存储在当前设备上硬盘上的数据，本地数据缓存有非常多的用途，我们可以利用本地数据缓存来存储用户在小程序上产生的操作，在用户关闭小程序重新打开时可以恢复之前的状态。我们还可以利用本地缓存一些服务端非实时的数据提高小程序获取数据的速度，在特定的场景下可以提高页面的渲染速度，减少用户的等待时间。其包含以下 8个主要的 API



| 同步 API               | 异步 API              | 作用                                |
| ---------------------- | --------------------- | ----------------------------------- |
| `wx.setStorageSync`    | `wx.setStorage`       | 将数据存储在本地缓存中指定的 key 中 |
| `wx.getStorageSync`    | `wx.getStorage`       | 从本地缓存中同步获取指定 key 的内容 |
| `wx.removeStorageSync` | `wx.removeStorage`    | 从本地缓存中移除指定 key            |
| `wx.clearStorageSync`  | `wx.clearStorageSync` | 清理本地数据缓存                    |
2. 注意:
1) 异步方式的 `API`，在调用的时候都需要传入对象类型的参数
2) 同步方式执行的 API 在使用时简洁比较好，缺点是同步会阻塞程序执行，执行效率相较异步版本要差一些。
3) 对象类型的数据，可以直接进行存储，无需使用 `JSON.stringify` 转换
4) 对象类型的数据存的时候没有使用转换，因此获取的时候也不需要使用 `JSON.parse` 转换
3. 代码示例

```html
<button type="primary" bindtap="handler" size="mini" plain bindtap="setData">
  存储数据
</button>

<button type="primary" bindtap="handler" size="mini" plain bindtap="getData">
  获取数据
</button>

<button type="warn" bindtap="handler" size="mini" plain bindtap="delData">
  删除数据
</button>

<button type="warn" bindtap="handler" size="mini" plain bindtap="clearData">
  移除数据
</button>
```



```js
Page({

  // 将数据存储到本地
  setStorage () {

    // 第一个参数：本地存储中指定的 key
    // 第二个参数：需要存储的数据
    // wx.setStorageSync('num', 1)

    // 在小程序中
    // 如果存储的是对象类型数据，不需要使用 JSON.stringify 和 JSON.parse 进行转换
    // 直接进行存储和获取即可
    // wx.setStorageSync('obj', { name: 'tom', age: 10 })

    // ------------------- 异步 API -------------------
 
    wx.setStorage({
      key: 'num',
      data: 1
    })

    wx.setStorage({
      key: 'obj',
      data: { name: 'jerry', age: 18 }
    })

  },

  // 获取本地存储的数据
  async getStorage () {

    // 从本地存储的数据中获取指定 key 的数据、内容
    // const num = wx.getStorageSync('num')
    // const obj = wx.getStorageSync('obj')

    // console.log(num)
    // console.log(obj)

    // ------------------- 异步 API -------------------

    const { data } = await wx.getStorage({
      key: 'obj'
    })

    console.log(data)

  },

  // 删除本地存储的数据
  removeStorage () {

    // 从本地移除指定 key 的数据、内容
    // wx.removeStorageSync('num')

    // ------------------- 异步 API -------------------

    wx.removeStorage({
      key: 'num'
    })

  },

  // 清空本地存储的全部数据
  clearStorage () {
    // wx.clearStorageSync()
      
    // ------------------- 异步 API -------------------

    wx.clearStorage()
  },

})

```
### 路由与通信
在小程序中实现页面的跳转，有两种方式：
1. 声明式导航：`navigator` 组件
2. 编程式导航：使用小程序提供的 `API`
   - `wx.navigateTo()`：保留当前页面，跳转到应用内的某个页面，但是不能跳到 tabbar 页面
   - `wx.redirectTo()`：关闭当前页面，跳转到应用内的某个页面。但是不允许跳转到 tabbar 页面
   - `wx.switchTab()`：跳转到 tabBar 页面，路径后不能带参数
   - `wx.navigateBack()`：关闭当前页面，返回上一页面或多级页面
3. 路径后可以带参数，参数需要在跳转到的页面的 `onLoad` 钩子函数中通过形参进行接收
   - 参数与路径之间使用 `?` 分隔
   - 参数键与参数值用 `=` 相连
   - 不同参数用 `&` 分隔
   - 例如 `path?key=value&key2=value2`

4. 代码示例

```js
Page({


  navigateTo() {

    // 保留当前页面，跳转到应用中其他页面，不能跳转到 tabBar 页面
    wx.navigateTo({
      url: '/pages/list/list?id=1&name=tom'
      // url: '/pages/cate/cate'
    })

  },

  redirectTo() {

    // 关闭(销毁)当前页面，跳转到应用中其他页面，不能跳转到 tabBar 页面
    wx.redirectTo({
      url: '/pages/list/list?id=1&name=tom'
      // url: '/pages/cate/cate'
    })

  },

  switchTab() {

    // 跳转到 tabBar 页面，不能跳转到 非 tabBar 页面，路径后面不能传递参数
    wx.switchTab({
      // url: '/pages/list/list'
      url: '/pages/cate/cate?id=1&name=tom'
    })

  },

  reLaunch() {

    // 关闭所有的页面，然后跳转到应用中某一个页面
    wx.reLaunch({
      url: '/pages/list/list?id=1&name=tom'
      // url: '/pages/cate/cate?id=1&name=tom'
    })

  }

})
```



```js
// list.js
Page({

  navigateBack() {

    // 关闭当前页面，返回上一页或者返回多级页面
    // 默认返回上一页
    wx.navigateBack({
      delta: 1
    })

  },

  onLoad(options) {
    console.log(options)
  }

})

```

### 事件监听-上拉加载更多
当用户滑动页面到底部时，会自动加载更多的内容，以便用户继续浏览
1. 小程序中实现上拉加载的方式：
1) 在 app.json 或者 page.json 中配置距离页面底部距离： onReachBottomDistance；默认 50px
2) 在 页面.js 中定义 onReachBottom 事件监听用户上拉加载
2. 代码示例

```html
<view wx:for="{{ numList }}" wx:key="*this">{{ item }}</view>
```



```scss
/* pages/market/market.wxss */

view {
  height: 400rpx;
  display: flex;
  align-items: center;
  justify-content: center;
}

view:nth-child(odd) {
  background-color: lightskyblue;
}

view:nth-child(even) {
  background-color: lightsalmon;
}
```



```js
Page({

  data: {
    numList: [1, 2, 3]
  },

  // 监听用户上拉加载
  onReachBottom() {
    // console.log('监听用户上拉加载')
    // 产品需求：
    // 当用户上拉，需要数字进行累加

    // 当用户上拉加载时，需要对数字进行累加，每次累加 3 个数字
    // 目前是 [1, 2, 3]，[1, 2, 3, 4, 5, 6]
    // 怎么进行追加 ？
    // 获取目前数组中最后一项 n，n + 1, n + 2, n + 3

    wx.showLoading({
      title: '数据加载中...'
    })

    setTimeout(() => {
      // 获取数组的最后一项
      const lastNum = this.data.numList[this.data.numList.length - 1]
      // 定义需要追加的元素
      const newArr = [lastNum + 1, lastNum + 2, lastNum + 3]

      this.setData({
        numList: [...this.data.numList, ...newArr]
      })

      wx.hideLoading()
    }, 1500)

  }

})

```
### 事件监听-下拉刷新
当用户下拉页面时，页面会自动刷新，以便用户获取最新的内容
1. 小程序中实现下拉刷新的方式
1) 在 app.json 或者 page.json 中开启允许下拉，同时可以配置 窗口、loading 样式等 

2) 在页面.js 中定义 onPullDownRefresh 事件监听用户下拉刷新
2. 代码示例


```html
<view wx:for="{{ numList }}" wx:key="*this">{{ item }}</view>
```



```scss
/* pages/market/market.wxss */

view {
  height: 400rpx;
  display: flex;
  align-items: center;
  justify-content: center;
}

view:nth-child(odd) {
  background-color: lightskyblue;
}

view:nth-child(even) {
  background-color: lightsalmon;
}
```



```js
Page({

  data: {
    numList: [1, 2, 3]
  },

  // 监听用户上拉加载
  onReachBottom() {
    
     // coding...

  },

  // 监听用户下拉刷新
  onPullDownRefresh () {
    // console.log('监听用户下拉刷新')

    // 产品需求：
    // 当用户上拉加载更多以后，如果用户进行了下拉刷新
    // 需要将数据进行重置
    this.setData({
      numList: [1, 2, 3]
    })

    // 在下拉刷新以后，loading 效果有可能不会回弹回去
    if (this.data.numList.length === 3) {
      wx.stopPullDownRefresh()
    }
  }

})

```

### 增强 scroll-view

#### scroll-view 上拉加载
1. 语法
bindscrolltolower：滚动到底部/右边时触发
lower-threshold：距底部/右边多远时，触发 scrolltolower 事件
enable-back-to-top：**让滚动条返回顶部**，iOS 点击顶部状态栏、安卓双击标题栏时，只支持竖向

2. 代码示例
```html
<scroll-view
  class="scroll-y"
  scroll-y
  lower-threshold="100"
  bindscrolltolower="getMore"
  enable-back-to-top
>

  <view wx:for="{{ arr }}" wx:key="*this">{{ item }}</view>

</scroll-view>
```



```js
// index.js
Page({

  data: {
    arr: [1, 2, 3]
  },

  // 上拉加载更多
  getMore() {

    wx.showLoading({
      title: '数据正在加载中...'
    })

    setTimeout(() => {

      // 记录当前数组的最后一个元素
      let lastNum = this.data.arr[this.data.arr.length - 1]
      // 最后一个元素加 1
      lastNum++
      // 每次向数组中新增三项
      const newArr = [lastNum, lastNum + 1, lastNum + 2]

      this.setData({
        arr: [...this.data.arr, ...newArr]
      })

     // 数据返回，隐藏 Loading
     wx.hideLoading()

     wx.showToast({
       title: '数字请求完毕，上滑继续浏览',
       icon: 'none'
     })

    }, 1000)

  }
})
```
#### scroll-view 下拉刷新
1. 语法
refresher-enabled：开启自定义下拉刷新
refresher-default-style自定义下拉刷新默认样式支持设置 `black | white | none`， none 表示不使用默认样式
refresher-background：自定义下拉刷新区域背景颜色
bindrefresherrefresh：自定义下拉刷新状态回调
refresher-triggered：设置当前下拉刷新状态，(true 下拉刷新被触发，false 表示下拉刷新未被触发，**用来关闭下拉效果**)

2. 代码示例

```html
<scroll-view
  class="scroll-y"
  scroll-y
  lower-threshold="100"
  bindscrolltolower="getMore"
  enable-back-to-top
             
  refresher-enabled
  refresher-default-style="black"
  refresher-background="#f7f7f8"
  refresher-triggered
  bindrefresherrefresh="onrefresh"
  refresher-triggered="{{ triggered }}"
>

  <view wx:for="{{ arr }}" wx:key="*this">{{ item }}</view>

</scroll-view>
```

```js
// index.js
Page({

  data: {
    triggered: false, // 控制 scroll-view 下拉刷新效果
    arr: [1, 2, 3]
  },

  // scroll-view 下拉刷新回调函数
  onrefresh() {

    wx.showLoading({
      title: '数据正在加载中...'
    })

    // 定时器模拟网络请求，1 秒后数据返回
    setTimeout(() => {

      // 重置数据
      this.setData({
        arr: [1, 2, 3]
      })

      // 数据返回，隐藏 Loading
      wx.hideLoading()

      wx.showToast({
        title: '下拉刷新完成，数据已重置...',
        icon: 'none'
      })

      // 数据返回，关闭 scroll-view 下拉刷新效果
      this.setData({
        triggered: false
      })

    }, 1000)
  }
})
```

#### 增强 scroll-view 完整代码


```html
<scroll-view
  scroll-y
  class="scroll-y"

  lower-threshold="100"
  bindscrolltolower="getMore"
  enable-back-to-top

  refresher-enabled
  refresher-default-style="black"
  refresher-background="#f7f7f8"
  bindrefresherrefresh="refreshHandler"
  refresher-triggered="{{isTriggered}}"
>
  
  <view wx:for="{{ numList }}" wx:key="*this">{{ item }}</view>

</scroll-view>
```



```scss
/* pages/index/index.wxss */

.scroll-y {
  height: 100vh;
  background-color: #efefef;
}

view {
  height: 500rpx;
  display: flex;
  align-items: center;
  justify-content: center;
}

view:nth-child(odd) {
  background-color: skyblue;
} 

view:nth-child(even) {
  background-color: lightsalmon;
}

```



```js

Page({

  data: {
    numList: [1, 2, 3],
    isTriggered: false
  },

  // 下拉刷新
  refreshHandler () {

    wx.showToast({
      title: '下拉刷新...'
    })
    
    setTimeout(() => {
      this.setData({
        numList: [1, 2, 3],
        isTriggered: false
      })
    }, 2000)

  },


  // scroll-view 上拉加载更多事件的事件处理函数
  getMore () {

    
    wx.showLoading({
      title: '数据加载中...'
    })

    setTimeout(() => {
      // 获取数组的最后一项
      const lastNum = this.data.numList[this.data.numList.length - 1]
      // 定义需要追加的元素
      const newArr = [lastNum + 1, lastNum + 2, lastNum + 3]

      this.setData({
        numList: [...this.data.numList, ...newArr]
      })

      wx.hideLoading()
    }, 1500)
  }

})

```
## 自定义组件
### 理解自定义组件
1. 组件化开发可以将页面中的功能模块抽取成自定义组件，以便在不同的页面中重复使用，也可以将复杂的页面拆分成多个低耦合的模块，有助于代码维护。
2. 开发中常见的组件有两种:
公共组件：将页面内的功能模块抽象成自定义组件，以便在不同的页面中重复使用
页面组件：将复杂的页面拆分成多个低耦合的模块，有助于代码维护
3. 书写位置
公共组件，建议将其放在小程序的目录下的 `components` 文件夹中
页面组件，建议将其放在小程序对应页面目录下，（也可以放到页面的 `components` 文件夹中）
4. 注意：
1) 自定义组件的需要在 `json` 文件中需要配置 `component` 字段设为 `true` 
2) 自定义组件通过 `Component` 构造器进行构建，在构造器中可以指定组件的属性、数据、方法等
### 使用自定义组件
1. 创建自定义组件
以公共组件为例，创建的步骤如下：
1) 在小程序的目录下新建 `components` 文件夹
2) 在 `components` 文件夹上，点击右键，选择`新建文件夹 `，然后输入文件夹名称，我们建议文件夹的名称和组件的名称保持一致，这样方便后期对组件进行维护。我们这里新的的组件名称叫做：`custom-checkbox`
3) 在新建的组件文件夹上，点击右键，选择`新建 Component`，然后输入组件的名称，组件的名称建议和文件夹保持一致
4. 使用自定义组件
开发中常见的组件主要分为 公共组件 和 页面组件 两种，因此注册组件的方式也分为两种：
1) 全局注册：在 `app.json` 文件中配置 `usingComponents` 节点进行引用声明，注册后可在任意页面使用
2) 局部注册：在页面的 `json` 文件中配置 `usingComponents` 节点进行引用声明，只可在当前页面使用
在配置 `usingComponents` 节点进行引用声明时，需要提供自定义组件的标签名和对应的自定义组件文件路径，语法如下：
```json
{
  "usingComponents": {
    "自定义组件的标签名": "自定义组件文件路径"
  }
}
```
这样，在页面的 `wxml` 中就可以像使用基础组件一样使用自定义组件。节点名即自定义组件的标签名，节点属性即传递给组件的属性值。
```json
{
  "usingComponents": {
    "custom-checkbox": "/components/custom-checkbox/custom-checkbox"
  }
}
```
```html
<!--pages/index/index.wxml-->
<view>
  <!-- 将导入的自定义组件当成标签使用 -->
  <custom-checkbox
                   />
</view>
```
### 自定义组件-数据和方法
1. 理解
在组件的 .js 中，需要调用 `Component` 方法创建自定义组件，`Component` 中有以下两个属性：
`data` 数据：组件的内部数据
`methods` 方法：在组件中事件处理程序需要写到 `methods` 中才可以

2. 落地代码：

`➡️ components/custom-checkbox/custom-checkbox.wxml`

```html
<!--components/custom-checkbox/custom-checkbox.wxml-->
<!-- <text>我是自定义组件</text> -->

<view class="custom-checkbox-container">
  <view class="custom-checkbox-box">
    <checkbox checked="{{ isChecked }}" bindtap="updateChecked" />
  </view>
</view>
```



`➡️ components/custom-checkbox/custom-checkbox.wxss`

```css
/* components/custom-checkbox/custom-checkbox.wxss */

.custom-checkbox-container {
  display: inline-block;
}
```



`➡️ components/custom-checkbox/custom-checkbox.js`

```js
Component({

  /**
   * 组件的初始数据：用来定义当前组件内部所需要使用的数据
   */
  data: {
    isChecked: false
  },

  /**
   * 组件的方法列表：在组件中，所有的事件处理程序都需要写到 methods 方法中
   */
  methods: {
    
    // 更新复选框的状态
    updateChecked () {

      this.setData({
        isChecked: !this.data.isChecked
      })

      console.log(this.data.isChecked)
    }

  }
  
})
```



`➡️ app.json`

```json
{
  "usingComponents": {
    "custom-checkbox": "./components/custom-checkbox/custom-checkbox"
  }
}
```





`➡️ index.wxml`

```html
<custom-checkbox />
<view class="line"></view>
<custom-checkbox />
```

###  自定义组件-属性
1. 语法
属性 Properties 是指组件的对外属性，主要用来接收组件使用者传递给组件内部的数据，和 data 一同用于组件的模板渲染


>  注意：
> 1) 设置属性类型需要使用 type 属性，属性类型是必填项，value 属性为默认值
> 2) 属性类型可以为 String、Number、Boolean、Object、Array ，也可以为 null 表示不限制类型

2. 代码示例
3. 
`➡️ index.wxml`

```html
<!-- label 文本显示的内容 -->
<!-- position 控制文本显示的位置 -->

<custom-checkbox label="我已阅读并同意 用户协议 和 隐私协议" position="right" />

<view class="line"></view>

<custom-checkbox label="匿名提交" position="left" />

```


` components/custom-checkbox/custom-checkbox.wxml`

```html
<!--components/custom-checkbox/custom-checkbox.wxml-->
<!-- <text>我是自定义组件</text> -->

<view class="custom-checkbox-container">
+   <view class="custom-checkbox-box {{ position === 'right' ? 'right' : 'left' }}">
+     <checkbox class="custom-checkbox" checked="{{ isChecked }}" bindtap="updateChecked" />
+ 
+     <view>
+       <text>{{ label }}</text>
+     </view>
  </view>
</view>

```



` components/custom-checkbox/custom-checkbox.wxss`

```css
/* components/custom-checkbox/custom-checkbox.wxss */

.custom-checkbox-container {
  display: inline-block;
}

.custom-checkbox-box {
  display: flex;
  align-items: center;
}

.custom-checkbox-box.left {
  flex-direction: row-reverse;
}

.custom-checkbox-box.right {
  flex-direction: row;
}

.custom-checkbox {
  margin-left: 10rpx;
}

```



`➡️ components/custom-checkbox/custom-checkbox.js`

```js
Component({

+   /**
+    * 组件的属性列表：组件的对外属性，主要用来接收组件使用者传递给组件内部的属性以及数据
+    */
+   properties: {
+     // 如果需要接收传递的属性，有两种方式：全写、简写
+     // label: String
+ 
+     label: {
+       // type 组件使用者传递的数据类型
+       // 数据类型：String、Number、Boolean、Object、Array
+       // 也可以设置为 null，表示不限制类型
+       type: String,
+       value: ''
+     },
+ 
+     // 文字显示位置
+     position: {
+       type: String,
+       value: 'right'
+     }
+   },

  /**
   * 组件的初始数据：用来定义当前组件内部所需要使用的数据
   */
  data: {
    isChecked: false
  },

  /**
   * 组件的方法列表：在组件中，所有的事件处理程序都需要写到 methods 方法中
   */
  methods: {
    
    // 更新复选框的状态
    updateChecked () {

      this.setData({
        isChecked: !this.data.isChecked,
+        // label: '在组件内部也可以修改 properties 中的数据'
      })

+       // 在 JS 中可以访问和获取 properties 中的数据
+       // 但是一般情况下，不建议修改，因为会造成数据流的混乱
+       // console.log(this.properties.label)
      // console.log(this.data.isChecked)
    }

  }
  
})
```
###  组件 wxml 的 slot
1. 在使用基础组件时，可以给组件传递子节点传递内容，从而将内容展示到页面中，自定义组件也可以接收子节点内容
但是在组件模板中需要定义 `<slot />` 节点，用于承载组件引用时提供的子节点

默认情况下，一个组件的 wxml 中只能有一个 slot 。需要使用多 slot 时，可以在组件 js 中声明启用。

同时需要给 slot 添加 name 来区分不同的 slot，给子节点内容添加 slot 属性来将节点插入到 对应的 slot 中

<img src="http://8.131.91.46:6677/mina/base/组件-具名插槽.png" style="zoom:80%; border: 1px solid #ccc" />
知识点讲解：

`custom01.html`
```html
<view>
  <slot name="slot-top" />
  <!-- slot 就是用来接收、承载子节点内容 -->
  <!-- slot 只是一个占位符，子节点内容会将 slot 进行替换 -->
  <!-- 默认插槽 -->
  <view><slot /></view>

  <slot name="slot-bottom" />
</view>
```

` custom01.js`
```js
// components/custom01/custom01.js

Component({

  options: {
    // 启用多 slot 支持
    multipleSlots: true
  }

})
```
` cart.wxml`
```html
<custom01>
  <text slot="slot-top">我需要显示到顶部</text>
  <!-- 默认情况下，自定义组件的子节点内容不会进行展示 -->
  <!-- 如果想内容进行展示，需要再组件模板中定义 slot 节点 -->
  我是子节点内容
  <text slot="slot-bottom">我需要显示到低部</text>
</custom01>

```
2. 完善复选框案例
` custom-checkbox.html`
```html
<!--components/custom-checkbox/custom-checkbox.wxml-->
<!-- <text>我是自定义组件</text> -->

<view class="custom-checkbox-container">
  <view class="custom-checkbox-box {{ position === 'right' ? 'right' : 'left' }}">
    <checkbox class="custom-checkbox" checked="{{ isChecked }}" bindtap="updateChecked" />

+     <view>
+       <!-- lable 和 子节点内容都进行了展示 -->
+       <!-- 要么展示 lable 要么展示 子节点内容 -->
+       <!-- 如果用户传递了 lable 属性，就展示 lable -->
+       <!-- 如果用户没有传递 lable 属性，就展示 子节点内容 -->
+       <text wx:if="{{ label !== '' }}">{{ label }}</text>
+ 
+       <slot wx:else />
+     </view>
  </view>
</view>
```
` index.html`
```html
<!-- label 文本显示的内容 -->
<!-- position 控制文本显示的位置 -->
<custom-checkbox label="我已阅读并同意 用户协议 和 隐私协议" position="right">
  我已阅读并同意 用户协议 和 隐私协议 - 111
</custom-checkbox>

<view class="line"></view>

<custom-checkbox label="匿名提交" position="left">
  匿名提交 - 222
</custom-checkbox>

```
###  组件样式以及注意事项
类似于页面，自定义组件拥有自己的 `wxss` 样式，组件对应 `wxss` 文件的样式，只对组件wxml内的节点生效。
编写组件样式时，需要注意以下几点：
1. app.wxss 或页面的 wxss 中使用了标签名（view）选择器（或一些其他特殊选择器）来直接指定样式
    这些选择器会影响到页面和全部组件，通常情况下这是不推荐的做法
2. 组件和引用组件的页面不能使用 id 选择器(#a)、属性选择器([a]) 和 标签名选择器，请改用 class 选择器
3. 组件和引用组件的页面中使用后代选择器（.a .b）在一些极端情况下会有非预期的表现，如遇，请避免使用
4. 子元素选择器（.a>.b）只能用于 view 组件与其子节点之间，用于其他组件可能导致非预期的情况。
5. 继承样式，如 font 、 color ，会从组件外继承到组件内。
6. 除继承样式外， 全局中的样式、组件所在页面的的样式对自定义组件无效 (除非更改组件样式隔离选项)
```css
#a { } /* 在组件中不能使用 */
[a] { } /* 在组件中不能使用 */
button { } /* 在组件中不能使用 */
.a > .b { } /* 除非 .a 是 view 组件节点，否则不一定会生效 */
```
7. 代码：
`custom02.wxml`

```html
<text id="content" class="content son">
  <text class="label">给自定义组件设置样式</text>
</text>
```

` custom02.wxss`

```scss
/* components/custom02/custom02.wxss */

/* 第一个注意事项：在自定义的 wxss 文件中，不允许使用标签选择器，ID 选择器，属性选择器 */
/* 请改为 class 选择器 */
/* text {
  color: lightseagreen;
} */

/* #content {
  color: lightseagreen;
} */

/* [id=content] {
  color: lightseagreen;
} */

/* .content {
  color: lightseagreen;
} */

/* 第二个注意事项：子选择器，只能用于 view 和 子组件，用于其他组件可能会出现样式失效的问题 */
/* .content > .label {
  color: lightseagreen;
} */

/* 第三个注意事项：继承样式，例如：color\font 都会从组件外继承 */

/* 第四个注意事项：全局样式、组件所在页面的样式文件中的样式都对自定义组件无效 */

/* 第五个注意事项：官方不推荐做法 */
/* 不建议在 全局样式文件 以及 父级页面之间使用标签选择器设置样式 */
/* 如果是在全局样式文件中设置样式，会影响项目中全部的相同组件 */
/* 如果是再页面样式文件中设置样式，会影响当前页面所有的相同组件 */

/* 第六个注意事项： */
/* 组件和组件使用者，如果使用了后代选择器，可能会出现一些非预期情况 */
/* 如果出现，请避免 */
```
`cate.wxml`

```html
<view class="custom parent">
  <view>
    <custom02 />

    <view class="son test">我是父级页面中的结构</view>
  </view>
</view>
```
` cate.wxss`
```scss
/* pages/cate/cate.wxss */

/* .custom  {
  color: lightseagreen;
  font-size: 50rpx;
} */

/* .label {
  color: lightseagreen;
} */

/* text {
  color: lightseagreen;
} */

.parent .son.test {
  color: lightsalmon;
}
```
`app.wxss`
```scss
/* .label {
  color: lightseagreen;
} */

/* text {
  color: lightseagreen;
} */

```
### 组件样式隔离

默认情况下，自定义组件的样式只受到自定义组件 wxss 的影响。除非以下两种情况：

1. `app.wxss` 或页面的 `wxss` 中使用了标签名（view）选择器（或一些其他特殊选择器）来直接指定样式，这些选择器会影响到页面和全部组件。通常情况下这是不推荐的做法。

2. 指定特殊的样式隔离选项 `styleIsolation` 

   ```js
   Component({
     options: {
       styleIsolation: 'isolated'
     }
   })
   ```

3. `styleIsolation` 选项它支持以下取值：

- `isolated` 表示启用样式隔离，在自定义组件内外，使用 class 指定的样式将不会相互影响（一般情况下的默认值）；
- `apply-shared` 表示页面 wxss 样式将影响到自定义组件，但自定义组件 wxss 中指定的样式不会影响页面；
- `shared` 表示页面 wxss 样式将影响到自定义组件，自定义组件 wxss 中指定的样式也会影响页面和其他设置了 `apply-shared` 或 `shared` 的自定义组件。

4. 代码：
` custom03.wxml`

```html
<!--components/custom03/custom03.wxml-->

<text class="label">演示组件样式隔离</text>
```
`custom03.wxss`

```scss
/* components/custom03/custom03.wxss */

.test {
  color: lightseagreen;
  font-size: 50rpx;
}
```
`custom03.js`

```js
// components/custom03/custom03.js
Component({

  options: {

    // styleIsolation：配置组件样式隔离

    // isolated：开启样式隔离，默认值
    // 在默认情况下，自定义组件和组件使用者如果存在相同的类名，类名不会相互影响

    // apply-shared：表示组件使用者、页面的 wxss 样式能够影响到自定义组件
    // 但是自定义组件的样式不会影响组件使用者、页面的 wxss 样式
    // styleIsolation: "apply-shared"

    // shared：表示组件使用者、页面的 wxss 样式能够影响到自定义组件
    // 自定义组件的样式会影响组件使用者、页面的 wxss 样式
    // 和其他使用了 apply-share 以及 share 属性的自定义组件
    styleIsolation: 'shared'

  }
    
})
```

` cate.wxml`

```html
<custom03 />
```
` cate.wxss`

```scss
.label {
  color: lightsalmon;
}
```




