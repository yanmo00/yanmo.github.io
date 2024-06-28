# uni-app组件

## 视图容器

### view

> hover-class:规定按下去的样式类
>
> hover-start-time：按住后多久出现点击态，单位毫秒
>
> hover-stay-time：手指松开后点击态保留时间，单位毫秒

### scroll-view

> 即滚动条设置：
>
> | scroll-x |      |      | 允许横向滚动 |      |
> | -------- | ---- | ---- | ------------ | ---- |
> | scroll-y |      |      | 允许纵向滚动 |      |
>
> | refresher-enabled   |      |      | 开启自定义下拉刷新     |      |
> | ------------------- | ---- | ---- | ---------------------- | ---- |
> | refresher-threshold |      |      | 设置自定义下拉刷新阈值 |      |
>
> | refresher-background |      |      | 设置自定义下拉刷新区域背景颜色                               |      |
> | -------------------- | ---- | ---- | ------------------------------------------------------------ | ---- |
> | refresher-triggered  |      |      | 设置当前下拉刷新状态，true 表示下拉刷新已经被触发，false 表示下拉刷新未被触发 |      |

### swiper

> 滑块视图容器,左右滑动或上下滑动,比如banner轮播图。
>
> ##### swiper-item
>
> | item-id | String |      | 该 swiper-item 的标识符 |
> | ------- | ------ | ---- | ----------------------- |
> |         |        |      |                         |

### match-media

> 适合多端调配

```vue
<match-media :min-width="375" :max-width="800" >
    <view>当页面最小宽度 375px， 页面宽度最大 800px 时显示	</view>
</match-media>

<match-media :min-height="400" :orientation="landscape">
   <view>当页面高度不小于 400px 且屏幕方向为横向时展示这里	</view>
</match-media>
```

### movable-area

> 可拖动区域
>
> | scale-area |      |      | 当里面的 movable-view 设置为支持双指缩放时，设置此值可将缩放手势生效区域修改为整个 movable-area |
> | ---------- | ---- | ---- | ------------------------------------------------------------ |
> |            |      |      |                                                              |
>
> ```vue
> <movable-area>
> 	<movable-view :x="x" :y="y" direction="all" @change="onChange">text</movable-view>
> </movable-area>
> ```

### cover-view/cover-image

>  覆盖在原生组件上的文本/图片视图。

## 基础内容

### icon

| type  | String |      | icon的类型               |
| ----- | ------ | ---- | ------------------------ |
| size  | Number |      | icon的大小，单位px       |
| color | Color  |      | icon的颜色，同css的color |

### text

| selectable  | Boolean |      | 文本是否可选 |      |
| ----------- | ------- | ---- | ------------ | ---- |
| user-select | Boolean |      | 文本是否可选 |      |
| space       | String  |      | 显示连续空格 |      |
| decode      | Boolean |      | 是否解码     |      |

空格

| ensp | 中文字符空格一半大小   |
| ---- | ---------------------- |
| emsp | 中文字符空格大小       |
| nbsp | 根据字体设置的空格大小 |

**Tips**

- 支持 `\n` 方式换行
- <span>组件编译时会被转换为 <text>
- 在app-nvue下，只有`<text>`才能包裹文本内容。无法在`<view>`组件包裹文本。

### rich-text

| 属性名             |      |      | 说明                                           |      |
| :----------------- | :--- | :--- | :--------------------------------------------- | :--- |
| nodes              |      |      | 节点列表 / HTML String                         |      |
| space              |      |      | 显示连续空格                                   |      |
| selectable         |      |      | 富文本是否可以长按选中，可用于复制，粘贴等场景 |      |
| image-menu-prevent |      |      | 阻止长按图片时弹起默认菜单                     |      |
| preview            |      |      | 富文本中的图片是否可点击预览。                 |      |
| @itemclick         |      |      | 拦截点击事件（只支持 `a`、`img`标签）          |      |

### progress

| 属性名          | 类型          | 默认值                   | 说明                                                    |      |
| :-------------- | :------------ | :----------------------- | :------------------------------------------------------ | :--- |
| percent         | Number        | 无                       | 百分比0~100                                             |      |
| show-info       | Boolean       | false                    | 在进度条右侧显示百分比                                  |      |
| border-radius   | Number/String | 0                        | 圆角大小                                                |      |
| stroke-width    | Number        | 6                        | 进度条线的宽度，单位px                                  |      |
| activeColor     | Color         | #09BB07（百度为#E6E6E6） | 已选择的进度条的颜色                                    |      |
| backgroundColor | Color         | #EBEBEB                  | 未选择的进度条的颜色                                    |      |
| active          | Boolean       | false                    | 进度条从左往右的动画                                    |      |
| active-mode     | String        | backwards                | backwards: 动画从头播；forwards：动画从上次结束点接着播 |      |
| duration        | Number        | 30                       | 进度增加1%所需毫秒数                                    |      |
| @activeend      | EventHandle   |                          | 动画完成事件                                            |      |