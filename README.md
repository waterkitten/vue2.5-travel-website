# mytravel
> A Vue.js project

Vuejs开发旅游页项目

## 项目相关 npm 依赖包
- fastClick: 用来处理移动端 `click` 事件 300毫秒延迟
- stylus: CSS 预处理框架
- stylus-loader
- vue-awesome-swiper: 轮播插件
- axios: 实现 `ajax`

- better-scroll: scroll插件
- vuex: 实现数据共享

## 设置样式变量
通过 variable.styl 设置样式变量，抽离出公用样式。以方便维护

# 首页
## HomeSwiper 组件
### 使用 vue-awesome-swiper 轮播插件
使用 2.6.7 版本
```
npm install vue-awesome-swiper@2.6.7 --save
```
具体参考 [vue-awesome-swiper](https://github.com/surmon-china/vue-awesome-swiper)

轮播图当中的 `CSS` 样式重点
该样式主要是防止网速过慢时页面布局的抖动，其含义是，`wrapper` 宽度 `100%`，高度由宽度的 `27%` 自动撑开。
```CSS
.wrapper {
  overflow: hidden;
  width: 100%;
  height: 0;
  padding-bottom: 27%;  
}
```
或者写成
```CSS
.wrapper {
  width: 100%;
  height: 27vw;
}
```

## HomeIcons 组件
### iconsList 分页
同样使用 `swiper` 进行分页，并利用以下方式实现自动构建多页切换的功能
```JavaScript
computed: {
  //根据数据项目的不同，自动构建icons多页切换功能
  pages () {
    const pages = []
    this.iconsList.forEach((item, index) => {
      const page = Math.floor(index / 8)
      if (!pages[page]) {
        pages[page] = []
      }
      pages[page].push(item)
    })
    return pages
  }
}
```
### ellipsis()样式封装
将 `ellipsis` 封装在 `mixins.styl` 文件中
```JavaScript
ellipsis()
  overflow: hidden
  white-space: nowrap
  text-overflow: ellipsis
```

## Recommend / Weekend 组件
设置 `min-width` 是为了让 `ellipsis()` 生效
```css
.item-info {
  flex: 1;
  padding: .1rem;
  min-width: 0;
}
```

## index-ajax
使用 `axios` 进行 ajax 请求
```
npm install axios --save
```
### .gitignore 设置
添加 `staitc/mock`，防止被推送到仓库

### 设置 mock数据 开发环境转发代理
设置 `config` 文件夹下的 `index.js`

设置 `module.exports` 下 `dev` 的 `proxyTable` 代理

webpack-dev-server 工具会自动将 `/api` 替换成 `/static/mock`
```JavaScript
proxyTable: {
  '/api': {
    target: 'http://localhost:8080',
    pathRewrite: {
      '^/api': '/static/mock'
    }
  }
}
```


# 城市页
## router-link
通过路由实现页面间跳转，在外层添加 `router-link`。`to` 后面跟需要跳转的 path 。
```HTML
    <router-link to="/city">
      <div class="header-right">
        {{this.city}}
        <span class="iconfont icon-jiantou"></span>
      </div>
    </router-link>
```

然后在 router 文件夹的相应 `index.js` 路由配置文件中进行 path、name 和 `component` 的声明，并进行 `import from`。即完成了路由配置。
```JavaScript
import Vue from 'vue'
import Router from 'vue-router'
import Home from '@/pages/home/Home'
import City from '@/pages/city/City'

Vue.use(Router)

export default new Router({
  routes: [{
      path: '/',
      name: 'Home',
      component: Home
    }, {
      path: '/city',
      name: 'City',
      component: City
    }]
})
```

## city-List
修改一像素边框 `.border-topbottom` 的颜色
```
.border-topbottom
  &:before
    border-color: #ccc
  &:after
    border-color: #ccc
```

将页面固定住，后续搭配 `better-scroll` 插件实现类似于原生 app 的页面上下拖动效果
```CSS
.list {
  overflow: hidden;
  position: absolute;
  top: 1.58rem;
  left: 0;
  right: 0;
  bottom: 0;
}
```

### better-scroll 插件
```
npm install better-scroll --save
```
将 HTML DOM 结构调整成文档中规定的结构，在外层取 `wrapper`，引用插件之后，在 `mounted ()` 生命周期钩子里面新建一个这个 DOM 引用的实例。

```JavaScript
import Bscroll from 'better-scroll'
export default {
  name: 'CityList',
  //生命周期函数 挂载之后执行
  mounted () {
    //引用 wrapper DOM
    this.scroll = new Bscroll(this.$refs.wrapper)
  }
}
```

具体用法，请查看文档  [better-scroll](https://github.com/ustbhuangyi/better-scroll/blob/master/README_zh-CN.md)

### alphabet
是一个显示在右的 a-z 字母缩略指引

## city-ajax
按照 `index-ajax` 一样的方式进行 `axios` 数据获取
- 包括 热门城市、字母表排序城市列表、Alphabet 在内的部分都通过 `axios` 获取数据

在 `v-for` 循环输出 cities 的时候，需要注意，cities 是一个 `Object`
```JavaScript
props: {
  hot: Array,
  cities: Object
}
```
因此后面用 `v-for="(item, key) of cities"`，和 `v-for="innerItem of item"` 做循环输出
```HTML
<div class="area" v-for="(item, key) of cities" :key="key">
  <div class="title border-topbottom">{{key}}</div>
  <div class="item-list">
    <div class="item border-bottom" v-for="innerItem of item" :key="innerItem.id">{{innerItem.name}}</div>
  </div>
</div>
```

## city-components
兄弟组件间联动，这里没有采用 `bus`。
而是采用 `Alphabet.vue`(子组件) 传递给 `City.vue`(父组件) ，然后再通过 `City.vue`(父组件) 传递给 `List.vue`(子组件)。


在 `Alphabet.vue` 的 template 的循环展示中绑定 `@click` ，并在 methods 中使用 `$emit` 向外( `City.vue` 父组件 )发送 `change` 事件。

```HTML
<template>
  <ul class="list">
    <li class="item"
        v-for="(item, key) of cities"
        :key="key"
        @click="handleLetterClick"
    >
      {{key}}
    </li>
  </ul>
</template>
```

```JavaScript
methods: {
  handleLetterClick (e) {
    this.$emit('change', e.target.innerText)
  }
}
```


在 `City.vue` 的 template 中设置 `@change="handleLetterClick"` 监听 change 事件。
```HTML
<city-alphabet :cities="cities" @change="handleLetterClick"></city-alphabet>
```

在 `methods` 中定义事件 `handleLetterClick`，传递 `letter` 参数。
```JavaScript
methods: {
  handleLetterClick (letter) {
    this.letter = letter
  }
}
```

并在 `data` 中定义数据 `letter`。
```JavaScript
data () {
  return {
    cities: {},
    hotCities: [],
    letter: ''  // Alphabet 通过 change 事件传递过来的数据
  }
}
```

并传递给 `List.vue`。
```HTML
<city-list :cities="cities" :hot="hotCities" :letter="letter"></city-list>
```

然后在 `List.vue` 子组件 props 接收 `letter`
```JavaScript
props: {
  hot: Array,
  cities: Object,
  letter: String  // 接收 letter
}
```

通过侦听器 watch，侦听 `letter` 的变化。在此之前先用 `ref` 引用找到相应的 DOM
```HTML
<div class="area" v-for="(item, key) of cities" :key="key" :ref="key">
  <div class="title border-topbottom">{{key}}</div>
  <div class="item-list">
    <div class="item border-bottom" v-for="innerItem of item" :key="innerItem.id">{{innerItem.name}}</div>
  </div>
</div>
```

使用 `better-scroll` 中的 `scrollToElement` 方法进行点击跳转效果的实现
```JavaScript
watch: {
  letter () {
    if (this.letter) {
      const element = this.$refs[this.letter][0]
      this.scroll.scrollToElement(element)
    }
  }
}
```

## alphabet 滑动逻辑
上下滑动时，取字母位置逻辑：
- 获取 A 字母距离顶部高度
- 滑动时，取当前位置距离顶部高度
- 计算差值，得到当前手指位置与 A 字母顶部差值
- 除以每个字母高度，得出当前字母，触发 change 事件给外部

在 `Alphabet.vue` 中进行代码的编写
```HTML
<template>
  <ul class="list">
    <li class="item"
        v-for="item of letters"
        :key="item"
        :ref="item"
        @touchstart="handleTouchStart"
        @touchmove="handleTouchMove"
        @touchend="handleTouchEnd"
        @click="handleLetterClick"
    >
      {{item}}
    </li>
  </ul>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    cities: Object
  },
  // 计算属性中定义 letters 是一个数组，从 cities 数据中遍历得到数据
  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      return letters
    }
  },
  data () {
    return {
      touchStatus: false  // 标识位
    }
  },
  methods: {
    handleLetterClick (e) {
      this.$emit('change', e.target.innerText)
    },
    handleTouchStart () {
      this.touchStatus = true
    },
    handleTouchMove (e) {
      if (this.touchStatus) {
        const startY = this.$refs['A'][0].offsetTop       // A 字母距离 header区域下沿 高度
        const touchY = e.touches[0].clientY - 79          // 手指距离 header区域下沿 高高度
        const index = Math.floor((touchY - startY) / 20)  // 当前字母下标
        if (index >= 0 && index < this.letters.length) {
          this.$emit('change', this.letters[index])       // 也通过 $emit 向外发送事件
        }
      }
    },
    handleTouchEnd () {
      this.touchStatus = false
    }
  }
}
</script>
```

实现效果解析图
![](https://upload-images.jianshu.io/upload_images/12904618-452638a279c6ce49.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 函数节流优化
使用函数节流优化 `handleTouchMove`，提高性能
```JavaScript
handleTouchMove (e) {
  if (this.touchStatus) {
    // 使用函数节流优化性能
    if (this.timer) {
      clearTimeout(this.timer)
    }
    this.timer = setTimeout(() => {
      const startY = this.startY  
      const touchY = e.touches[0].clientY - 79  
      const index = Math.floor((touchY - startY) / 20)
      if (index >= 0 && index < this.letters.length) {
        this.$emit('change', this.letters[index])     
      }
    }, 16)
  }
}
```


## city-search 搜索功能逻辑
在 `template` 的 `input` 中做 `v-model="keyword"` 双向绑定。
```HTML
<template>
  <div>
    <div class="search">
      <input v-model="keyword" class="search-input" type="text" placeholder="输入城市名或拼音">
    </div>
    <div class="search-content">
      <ul>
        <li v-for="item of list">{{item.name}}</li>
      </ul>
    </div>
  </div>
</template>
```

在 `data ()` 中定义 `keyword`、`list` 和 `timer`。

在侦听器 `watch` 中侦听 `keyword` 的改变。

并使用函数节流进行优化。
```HTML
<script>
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      keyword: '',
      list: [],
      timer: null
    }
  },
  watch: {
    keyword () {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      this.timer = setTimeout(() => {
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach((value) => {
            if (value.spell.indexOf(this.keyword) > -1 ||
                value.name.indexOf(this.keyword) > -1) {
                  result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    }
  }
}
</script>
```


### 输入逻辑优化
#### 清空 input
由于数据是双向绑定的，所以在 `watch` 当中添加条件判断，当 `!this.keyword` 时，清空 `list`。
```JavaScript
if (!this.keyword) {
  this.list = []
  return
}
```

这样就实现了清空 `input` 搜索栏时，同时清空下面搜索结果的逻辑。

#### 没有找到匹配
添加 `li` ，其内容为 `没有找到匹配` 。同时用 `v-show` 指令，完成在没有匹配时候(`!list.length`)。显示该 `li` 内容，即 **没有找到匹配** 的功能。
```HTML
<li class="search-item border-bottom" v-show="!list.length">没有找到匹配</li>
```

#### search-content 显示与否
同样的使用 `v-show` 指令，决定是否显示 `class="search-content"` 这个 div 元素。决定的值为 `keyword`，这容易理解。
```HTML
<div class="search-content" ref="search" v-show="keyword">
  <ul>
    <li class="search-item border-bottom" v-for="item of list">{{item.name}}</li>
    <li class="search-item border-bottom" v-show="!list.length">没有找到匹配</li>
  </ul>
</div>
```


### 给 search-item 添加 better-scroll
给搜索结果页面也添加 `better-scroll` 使其多结果超出页面显示时，可以进行同样的 `better-scroll` 插件效果的滑动。

首先引入 `better-scroll`
``` JavaScript
import Bscroll from 'better-scroll'
```

使用 `ref` 引用 `search-content` 的元素
```HTML
<div class="search-content" ref="search">
  <ul>
    <li class="search-item border-bottom" v-for="item of list">{{item.name}}</li>
  </ul>
</div>
```

同样使用 `mounted` 生命周期钩子，传递的内容是 `this.$refs.search`
```JavaScript
mounted () {
  this.scroll = new Bscroll(this.$refs.search)
}
```

这样搜索结果页面结果过多超出页面时，也可以拥有 `better-scroll` 的滑动效果。


## 使用 Vuex 实现数据共享
需要实现 city 页面的数据传递给 index 首页。由于 `City.vue` 和 `Home.vue` 没有公用父级组件，这样就无法通过一个公用的父级组件进行数据的中转。这里我们使用 `Vuex` 数据层框架来实现。
[Vuex官方文档](https://vuex.vuejs.org/zh/)

### 安装并配置 Vuex
```
npm install vuex --save
```

创建 `store` 文件夹，建立 `index.js`，`state` 里放置全局公用数据 `city`。
```JavaScript
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    city: '重庆'
  },
  mutations: {
    changeCity (state, city) {
      state.city = city
    }
  }
})
```


在 `main.js` 的根实例下，将 `store` 传递进去。在其他子组件中使用 `this.$store` 进行派发。
```JavaScript
import store from './store'  //引入 store

new Vue({
  el: '#app',
  router: router,
  store: store,  //传递进入根实例的 store
  components: { App },
  template: '<App/>'
})
```

在 `List.vue` 和 `Search.vue` 组件中包含城市循环输出项的元素标签上定义 `@click="handleCityClick(item.name)"`。

并在相应的 `methods` 中执行 `Vuex` 的 `commit` 方法( 数据共享 ) 和 `Vue-router` 的 `push` 方法( 页面跳转 )
```JavaScript
methods: {
  handleCityClick (city) {
    this.$store.commit('changeCity', city)
    this.$router.push('/')
  }
}
```

### localStorage
使用 `localStorage` 实现城市保存的功能，在 `store` 的 `index.js` 文件中配置  `localStorage`
```JavaScript
export default new Vuex.Store({
  state: {
    city: localStorage.city || '重庆'
  },
  mutations: {
    changeCity (state, city) {
      state.city = city
      localStorage.city = city
    }
  }
})
```

有可能当用户使用隐身模式或禁用 `localStorage`，会导致浏览器报错。所以建议使用 `try catch` 进行优化
```JavaScript
let defalutCity = '重庆'
try {
  if (localStorage.city) {
    defaultCity = localStorage.city
  }
} catch (e) {}

export default new Vuex.Store({
  state: {
    city: defaultCity
  },
  mutations: {
    changeCity (state, city) {
      state.city = city
      try {
        localStorage.city = city
      } catch (e) {}
    }
  }
})
```


## keep-alive 优化
当查看 network 时候，可以看到从首页到城市选择页切换过程中每次切换都会发送 `ajax` 请求。所以我们对此进行优化。
![](https://upload-images.jianshu.io/upload_images/12904618-47ee5023f3389f10.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在 `App.vue` 中给 `<router-view/>` 外部添加一个 `<keep-alive>` 标签。其含义是路由的内容被加载过一次之后，就把路由的内容放置到内存中，下一次再使用路由的时候，无需重新加载组件、执行钩子函数。只需要从内存中拿出以前的内容显示就可以了。

![](https://upload-images.jianshu.io/upload_images/12904618-fb76f7866aa5c2d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### activated 生命周期钩子
结合 keep-alive 新增的 `activated` 生命周期钩子，实现每次点击曾经选中过的城市，不发送 `ajax`，城市选择变化的时候再进行 `ajax` 请求的优化。

![](https://upload-images.jianshu.io/upload_images/12904618-bb8ebd7a2578bbb9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
