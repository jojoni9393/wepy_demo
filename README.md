# wepy_demo

## 安装

```javascript
npm install -g wepy-cli
wepy --version // 查看版本
1、wepy init standard my-project （带事例，比较复杂）
2、wepy init empty my-project（简易，推荐）
```

## npm run dev（开发期间）

`会生成dist目录,导入小程序开发工具`
`微信开发者工具详情需要进行一些设置(否则会报错）`
`全部取消，只保留不校验合法域名。。。`

## 新增页面

```javascript
//需要在app.wpy ,添加新页面路径
config = {
    pages: ['pages/index'],
}
```

## 引入样式

```javascript
<style>
@import 'assets/style/weui.wxss';
</style>
```

## async await（请求配置）

```javascript
//原来回调函数失效(success)
//1、安装
npm install wepy-async-function --save


//2、修改wepy.config.js加入runtime配置
        babel: {
            "presets": [
                "env"
            ],
            "plugins": [
                "transform-export-extensions",
                "syntax-export-extensions"
            ]
        }

//3、在app.wpy中引入引入runtime包
import 'wepy-async-function';

//4、在app.wpy中使API promise化

export default class extends wepy.app {
    constructor () {
        super();
        this.use('promisify');
    }
}

//参考资料
//https://github.com/Tencent/wepy/wiki/wepy%E9%A1%B9%E7%9B%AE%E4%B8%AD%E4%BD%BF%E7%94%A8async-await
```

## data（数据）

```javascript
  data = {
        v_shelf_banner: [],
    app_list: []
  };
```

## methods（只能通过在html绑定触发,如@tap）

```javascript
  methods = {
    // 选择收货地址
    async chooseAddress() {
      const res = await wepy.chooseAddress()
      // 设置收货地址
      this.setAddress(res)
      this.$apply()


      // 将 收货地址 存储到本地缓存中
      wepy.setStorageSync('address', res)
    }
  };
```

## 改变数据

```javascript
//同步设置数据
this.list = [1,2,3]

//异步设置数据
this.list = [1,2,3]
this.$apply()   //异步修改数据需要增加，才会生效
```

## wxParse（html解析wxhtml插件）

```javascript
//同步设置数据
//git clone https://github.com/icindy/wxParse
```

## 轮播图

```javascript
  <swiper
    class="swiper"
    indicator-dots="{{ true }}"
    indicator-color="rgba(255,255,255,.5)"
    indicator-active-color="#ffffff"
    interval="2500"
    autoplay="true"
    circular="true"
  >
    <block wx:for="{{ detail.pics }}" wx:key="{{ pics_id }}">
      <swiper-item>
        <image class="swiper-img" src="{{ item.pics_mid_url }}" />
      </swiper-item>
    </block>
  </swiper>
```

## 获取用户信息+登录

```javascript
<template>
  <button @getuserinfo="getuserinfo" open-type="getUserInfo">获取用户信息+登录</button>
</template>
<script>
  methods = {
    getuserinfo(e) {
      wx.login({
        success(res) {
          console.log(res, 'code')
        }
      })
    }
  }
```


