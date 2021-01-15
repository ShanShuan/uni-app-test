<template>
<!-- <view>
  <home-ablum></home-ablum>
  <home-category></home-category>
  <home-new></home-new>
  <home-recomend></home-recomend>
</view> -->

<view class="home_tab"> 
        <view class="home_tittle">
          <view class="home_inner">
              <uni-segmented-control :current="current" :values="items" @clickItem="onClickItem" style-type="text" active-color="#d4237a"></uni-segmented-control>
          </view>
        <view class="inconfont iconwxbdingwei">
             <span class="c">🔍</span>
        </view>
          
        </view>
        <view class="content">
            <view v-if="current === 0">
                <home-ablum></home-ablum>
            </view>
            <view v-if="current === 1">
                <home-category></home-category>
            </view>
            <view v-if="current === 2">
                <home-new></home-new>
            </view>
            <view v-if="current === 3">
               <home-recomend></home-recomend>
            </view>
        </view>
    </view>
</template>

<script>
import homeAblum from './home-ablum';
import homeCategory from './home-category';
import homeNew from './home-new';
import homeRecomend from './home-recomend';


import {uniSegmentedControl } from '@dcloudio/uni-ui'
export default {
 components:{
   homeAblum,
   homeCategory,
   homeNew,
   homeRecomend,
   uniSegmentedControl 
 }
 ,data() {
        return {
            items: ['相册','分类','最新','推荐'],
            current: 0
        }
    },
    methods: {
        onClickItem(e) {
            if (this.current !== e.currentIndex) {
                this.current = e.currentIndex;
            }
        }
    }  
}
</script>

<style lang="scss">
.home_tab{
  .home_tittle{
    position: relative;
    .home_inner{
     width: 60%;
     margin: 0 auto;
    }
    .inconfont{
      position: absolute;
      top: 50%;
      transform: translateY(-50%);//垂直居中
      right: 5%;
    }
  }
  .content{
   
  }
}

</style>