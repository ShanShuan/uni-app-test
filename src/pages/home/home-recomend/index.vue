<template>
  <scroll-view @scrolltolower="handletolower" scroll-y  class="recomends_view" v-if="recomends.length>0">

  <!-- 推荐开始 -->
  <view class="commend">
      <view class="item" v-for="item in recomends" :key="item.id">
          <img :src="item.thumb" mode="widthFix" />
      </view>

  </view>
  <!-- 推荐结束 -->

  <!-- 月份开始 -->
  <view class="month">
      <view class="month_title">
          <view class="month_title_info">
              <view class="month_info">
                  <text class="ss">8 /01月 </text>
              
              </view>
               <view class="text">你负责美丽就好</view>
          </view>
          <view class="month_title_more">更多</view>
      </view>
      <view class="month_content">
            <view class="month_content_item"  v-for="item in content.items" :key="item.id" >
               <img mode="aspectFill" :src="item.thumb+item.rule.replace('$<Height>',360)" >
            </view>
      </view>
  </view>
  <!-- 月份结束 -->

<!-- 热门开始 -->
<view class="hot">
    <view class="hot_title">
          <text >热门</text>
    </view>
     <view class="hot_contents">
        <view class="hot_item" v-for="item in hots" :key="item.id">
            <img mode="aspectFill" :src="item.thumb" >
        </view>
     </view>
</view>
<!-- 热门结束 -->

</scroll-view>
</template>

<script>
export default {
    data(){
        return{
            recomends:[],
            content:{},
            hots:[],
            params:{
                limit:30,
                order:'hot',
                skip:0
            },
    
        }
    },
    mounted(){
     this.getList()
    },
    methods:{
        // 滚动到底部
        handletolower(){
            console.log("為什麼超人救人的時候要穿緊身褲？？ 因為救人要緊！！")
            this.params.skip+=this.params.limit
            this.getList()
        },
        getList(){
            this.request({
                url:"http://157.122.54.189:9088/image/v3/homepage/vertical",
                data: this.params 
            }).then(res=>{
                this.recomends=res.res.homepage[1].items;
                this.content=res.res.homepage[2];
                this.hots=[...this.hots,...res.res.vertical];
            })
        } 
    }  
    
}
</script>

<style lang="scss">
    .recomends_view{
        height: 600px
    }
.commend{
    display: flex;
    flex-wrap:wrap ;
    .item{
        width: 50%;
        border: 5rpx solid white;
    }
}

.month {
  .month_title {
      display: flex;
      justify-content: space-between;
      padding: 20rpx;;
    .month_title_info {
        display: flex;
        color: #e01358;
        font-weight: 600;
      .month_info {
       font-size: 36rpx;
       margin-left: 30rpx;
        color: #666;
      }

      .text {
        font-size: 36rpx;
        margin-right: 36rpx;
      }
    }

    .month_title_more {

    }
  }

  .month_content {
      display: flex;
      flex-wrap:wrap;
      .month_content_item{
         width: 33.33%;
         border: 5rpx solid #fff;;   
      }
  }

   
}

.hot{
      .hot_title{
           color: #e01358;
      }
      .hot_contents{
          display: flex;
            flex-wrap:wrap;
          .hot_item{
            width: 33.33%;
             border: 5rpx solid #fff;  
          }
        
      }
  }
</style>