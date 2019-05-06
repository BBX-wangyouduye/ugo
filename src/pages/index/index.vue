<template>
  <div>
    <!-- 搜索 -->
    <div class="search">
      <!-- 搜索框 -->
      <div class="search-box">
        <input type="text">
      </div>
      <!-- 搜索结果 -->
      <div class="reault"></div>
    </div>
    <!-- 轮播图 -->
    <swiper class="banner" indicator-dots indicator-color="rgba(255,255,255,0.6)" indicator-active-color="#fff" autoplay>
      <swiper-item :key="key" v-for="(list, key) in bannerList">
        <navigator :url="list.navigator_url">
          <image :src="list.image_src"></image>
        </navigator>
      </swiper-item>
    </swiper>
    <!-- 导航 -->
    <div class="navs">
      <navigator :key="key" v-for="(list , key) in navsList">
        <image :src="list.image_src"></image>
      </navigator>
    </div>
    <!-- 楼层 -->
    <div class="floor" :key="key" v-for="(list, key) in foolList">
      <div class="title">
        <image :src="list.floor_title.image_src"></image>
      </div>
      <div class="pics">
        <navigator :url="item.navigator_url" :key="k" v-for="(item, k) in list.product_list">
          <image :src="item.image_src"></image>
        </navigator>
      </div>
    </div>
  </div>
</template>

<script>
// 引入 request 请求封装
import request from '@/utils/request'
// import request from '@/utils/request'

export default {
  data () {
    return {
      bannerList:[],
      navsList: [],
      foolList: []
    }
  },
  methods: {
    // 轮播图接口
    async getBanner () {
      /****** 普通写法 *******/
      // let that = this
      // mpvue.request({
      //   url:'https://www.zhengzhicheng.cn/api/public/v1/home/swiperdata',
      //   method:'get',
      //   success (info) {
      //     // console.log(info)
      //     that.bannerList = info.data.message
      //   }
      // })
      /****** 封装后写法 *******/
      let { message } = await request({
        url: '/api/public/v1/home/swiperdata'
      })
      this.bannerList = message
    },
    // 导航接口
    async getNavs () {
      /****** 普通写法 *******/
      // let that = this
      // mpvue.request({
      //   url:'https://www.zhengzhicheng.cn/api/public/v1/home/catitems',
      //   method:'get',
      //   success (info) {
      //     // console.log(info)
      //     that.navsList = info.data.message
      //   }
      // })
      /****** 封装后写法 *******/
      let { message } = await request({
        url: '/api/public/v1/home/catitems'
      })
      this.navsList = message
    },
    // 楼层接口
    async getFloors () {
      let { message } = await request({
        url: '/api/public/v1/home/floordata'
      })
      this.foolList = message
    },
    // 回到顶部
    goTop () {

    }

  },
  mounted () {
    // 获取轮播图
    this.getBanner()
    // 获取导航
    this.getNavs()
    // 获取楼层
    this.getFloors()
  },
  // 下拉刷新
  onPullDownRefresh () {
    console.log('111')
    this.getNavs()
    this.getFloors()
    this.getBanner()
    // 停止下接的动态效果
    mpvue.stopPullDownRefresh();
  }

}
</script>

<style scoped lang="less">
.search .search-box{
  background-color: #ea4451;
  padding: 21rpx 30rpx;
  input {
    height: 60rpx;
    padding: 0 15rpx;
    background-color: #fff;
    border-radius: 10rpx;
    font-size: 24rpx;
    color: #666;
  }
}
.banner{
  height: 340rpx;
  width: 750rpx;
  image{
    height: 340rpx;
    width: 750rpx;
  }
}
.navs{
  display: flex;
  justify-content: space-between;
  padding: 30rpx 29rpx;
  navigator{
    width: 128rpx;
    height: 140rpx;
    image{
      width: 128rpx;
      height: 140rpx;
    }
  }
}
.floor {
  .title {
    padding-top: 28rpx;
    background-color: #f4f4f4;
    image{
      height: 60rpx;
      width: 750rpx;
    }
  }
  .pics{
    padding: 22rpx;
    overflow: hidden;
    navigator{
      image {
        float: left;
        width: 232rpx;
        height: 188rpx;
        margin-right: 10rpx;
        margin-bottom: 10rpx;
      }
    }
    :nth-child(2n-1) image{
      margin-right: 0;
    }
    :first-child image{
      height: 386rpx;
      margin-right: 10rpx;
    }
  }
}
</style>
