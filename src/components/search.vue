<template>
  <!-- 搜索 -->
  <div class="search">
    <!-- 搜索框 -->
    <div class="search-box">
      <input type="text">
    </div>
    <!-- 搜索结果 -->
    <div class="reault"></div>
  </div>
</template>

<script>
  export default {
    data () {
      return {}
    },
    methods: {
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

</style>
