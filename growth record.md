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
