# Q&A

这里收集了过去使用者在 QQ 群经常遇到的问题，如果有其他问题可以添加QQ群：747809274 进行交流

### 引入组件后不显示弹幕

组件需要的最小配置条件仅为 v-model:danmus 和设置组件的宽高，如果配置了这两者还不显示弹幕，那建议逐一排查以下问题：

- 查看控制台有无报错
- 异步加载的弹幕需要手动调用 play() 方法
- 默认弹幕的颜色太淡了，可能无法注意到

如果仍然还没有弹幕的话，可以加群或者提交 issue 反馈问题

### 窗口尺寸改变后弹幕会错位

需要在外部监听 resize 事件，触发时调用 refName.value.resize() 方法即可

### 在项目中引入后弹幕重叠在一起

这个大概率是父级和祖先元素的某些css影响到了弹幕组件，建议逐一排查，尤其是使用了 transform 的地方

### 弹幕太长的情况下弹幕条会忽大忽小

这个是弹幕绘制机制的问题，暂时无法解决，建议在输入前判断弹幕的长度，过长的弹幕进行屏蔽处理（后期可能会考虑增加API解决该问题）

### 部分低端机型上弹幕会卡顿

- 一个思路是降低弹幕绘制的频率（即 debounce 设置的大一点）
- 也可以开启性能模式 :performance="true" （TODO 暂未实现）

### 怎么设置固定顶部和底部的弹幕

有这种需求的基本都是需要做视频弹幕的，建议使用 [DPlayer](https://dplayer.diygod.dev) 解决视频弹幕的问题

### 如何在 nuxt 中使用

跟正常用法一致，不过需要按照 nuxt 文档中的说明，在组件外层包裹 `<client-only></client-only>`

### 直播场景该使用什么方法

建议直接使用 insert() ，同时不要使用 push() 或 add()，否则会导致v-model绑定的数组越来越大

### 如何从 vue2 升级到 vue3

目前 vue2 和 vue3 的版本功能是保持同步的（包括API），所以你只需要升级 vue 本身的语法，然后从 vue-danmaku 升级为 vue3-danmaku 即可

### 支持小程序吗

不打算支持，建议自己实现

### 其他定制化需求

vue-danmaku 的代码非常简单，核心代码在 [src/lib/Danmaku.vue](https://github.com/hellodigua/vue-danmaku/blob/vue3/src/lib/Danmaku.vue) 中，你可以直接拷贝该文件到自己的项目中进行定制化修改。（之后会出一个文档详细介绍弹幕绘制的原理）