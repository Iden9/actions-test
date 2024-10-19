---
title: "uniapp 中使用 u-swipe-action"
date: 2024-10-19
categories: ["uniapp"]

---

### uniapp中使用u-swipe-action

在开发移动端应用时我们通常需要对单元格进行左划编辑，或者删除操作，此时就可以使用`u-swiper-action`组件

#### 基本使用
```vue
<template>
	<view>
      <up-swipe-action>
        <up-swipe-action-item
          v-model:show="show"
          :options="options1"
        >
          <view class="swipe-action up-border-top up-border-bottom">
            <view class="swipe-action__content">
              <text class="swipe-action__content__text">基础使用</text>
            </view>
          </view>
        </up-swipe-action-item>
      </up-swipe-action>
	</view>
</template>

<script>
	export default {
		data() {
			return {
                options1: [{
                    text: '删除'
                }]
			};
		},
	};
</script>

<style lang="scss">
    .u-page {
        padding: 0;
    }

    .u-demo-block__title {
        padding: 10px 0 2px 15px;
    }

    .swipe-action {
        &__content {
             padding: 25rpx 0;
    
            &__text {
                 font-size: 15px;
                 color: $up-main-color;
                 padding-left: 30rpx;
             }
        }
    }
</style>
```

当你需要设置左划后的点击操作可以给 `u-swipe-action-item`中设置点击事件 @click 就可以设置点击事件了

``` vue
<up-swipe-action-item
          v-model:show="show"
          :options="options1"
          @click = "del()"
        >
          <view class="swipe-action up-border-top up-border-bottom">
            <view class="swipe-action__content">
              <text class="swipe-action__content__text">基础使用</text>
            </view>
          </view>
</up-swipe-action-item>

<script>

export default{
    methods:{
        del(){
            // 这里设置具体的操作
        }
    }
}
</script>
```