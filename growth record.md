# 个人日常工作采坑成长记录

## 2018-11-03

1. `form`提交时，如果`input`框设置了`disabled`，那么不会提交该`input`框的值。这个以前真没意识到。。。网上说用`readonly`替代，但是我试了下并不符合我的预期，我加了一个`<input type="hidden" name="Data[type]" :value="tupe">`（vue）。

## 2018-11-04

1. `form`默认是`get`提交，我曾经看过，但是真的忘了，还是这两天的一个bug提醒了我。

## 2018-11-06

1. 接手的项目中有这么一段代码引发了兼容性问题：
    ```js
    $(this.$refs.tab).find("li[data-index=" + index + "]").get(0).scrollIntoView({
      behavior: 'smooth',
      block: 'nearest',
      inline: 'nearest'
    });
    ```
    一直用的chrome开发调试，没在意，直到测试在firefox上发现这里存在兼容性问题，随后去MDN上看`scrollIntoView`这个api，果然还是实验中的属性。firefox不支持"block" 设置项的值"nearest" 或 "center"，也不支持 "inline" 设置项。具体看：https://developer.mozilla.org/zh-CN/docs/Web/API/Element/scrollIntoView

## 2018-11-12

1. 以前没用过vue的`slot`api，直到目前接手的项目中用到，才发现其实自己不怎么会，后来百度了下才算了解：https://laboo.top/2018/11/07/vue/

## 2018-11-17
> 其实是11.15号工作时了解到的内容，但由于当天通宵加班，今天才想起来。

1. 关于 Flexbox 布局（偏向各个属性实现原理讲解）：
  - https://github.com/xitu/gold-miner/blob/master/TODO1/flexbox-display-flex-container.md
  - https://github.com/xitu/gold-miner/blob/master/TODO1/flexbox-alignment.md
  
 2. <a href="https://github.com/xitu/gold-miner/blob/master/TODO1/adaptive-serving-using-javascript-and-the-network-information-api.md">使用 JavaScript 和网络信息 API 实现自适应服务</a>
 
 3. <a href="https://github.com/xitu/gold-miner/blob/master/TODO1/three-input-element-properties-that-i-discovered-while-reading-mdn.md">我在阅读 MDN 时发现的 3 个 Input 元素属性</a>
 
## 2018-11-20
今天遇到了个很不解问题，想了起码3小时愣是没想明白，是一个vue写的模拟table列表的组件，这里贴出部分代码：
```js
<template>
  <div class="panel-default">
    <div class="panel-head panelFixedWidth">
      <ul>
        <li class="toggle" >
          <label><input type="checkbox" v-model="checkAll"></label>
        </li>
        <li v-for="(item, index) in titleList" :key="index" :class="'wid-' + item.key">
          <select v-if="item.key==='MediaType'" v-model="adMediaType" @change="changeTitle" class="box-select">
            <option v-for="(opt, opt_index) of item.options" :key="opt_index" :value="opt.value" v-text="opt.title"></option>
          </select>
          <select v-else-if="item.key==='DayNums'" v-model="adDayNums" @change="changeTitle" class="box-select">
            <option v-for="(opt, opt_index) of item.options" :key="opt_index" :value="opt.value" v-text="opt.title"></option>
          </select>
          <select v-else-if="item.key==='IsActive'" v-model="adIsActive" class="box-select" disabled>
            <option v-for="(opt, opt_index) of item.options" :key="opt_index" :value="opt.value" v-text="opt.title"></option>
          </select>
          <span v-else v-text="item.title"></span>
        </li>
      </ul>
    </div>
    <div class="panel-body">
      <ul class="panel-content-ul">
        <li class="clearfix" v-for="(item, index) in dataList" :key="index" class="panelFixedWidth">
          <span class="toggle" >
            <label><input type="checkbox" :value="item.ID" v-model="checkList"></label>
          </span>
          <span 
            v-for="(item_value, item_key) in item" 
            :key="item_key + '-' + index" 
            :class="'wid-' + item_key" 
            :style="{width: 100 / nShowCount + '%'}" 
            :title="item_value" 
            v-if="item_key !== 'ID'"
            v-text="item_value">
          </span>
        </li>
      </ul>
    </div>
  </div>
</template>
```

> 省略了一些无关的代码，核心渲染代码就这么多。

- 问题是什么？
  - 如上面代码可见，这个模拟的table，表头和表中的数据我竟然不知道它如何保证一一对应的！！！
  - 起初我以为根据`key`来对应，但是也不对啊，vue中`key`应该是唯一的，而且表中的`key`后面都加上了`index`！这就很奇怪了，我也一度以为和后台约定好顺序它才能一一对应的，的确，在其他页面，后台返回的例如`BidMode`如果夹在三个`select`之中，那么列表渲染时数据没有一一对应，改变数据顺序就正常了，可是`Size`默认放在最后，而页面上`Size`却第4个展示，它还是一定程度上保证一一对应的！神烦，今天记录下来，明天继续搞！！！
