<template>
  <view class="text-page">

    <view class="page-nav">
      <image class="nav-back" @click="goBack" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill" />

      <text class="page-title">积分奖励规则</text>
    </view>

    <text class="h1">我是规则说明</text>
    <text class="p">
      我是规则说明我是规则说明我是规则说明我是规则说明我是规则说明我是规则说明我是规则说明我是规则说明我是规则说明我是规则说明。
      我是规则说明我是规则说明我是规则说明我是规则说明我是规则说明我是规则说明我是规则说明我是规则说明我是规则说明。
    </text>
  </view>
</template>

<script>
export default {
  methods: {
    goBack() {
      uni.navigateBack({
        delta: 1
      })
    }
  }
}
</script>

<style scoped>
.text-page{min-height:100vh;background:#000;color:#fff;padding:20px 16px;background-image:url('@/static/icons/background.svg');background-size:cover;background-position:center;background-repeat:no-repeat}
.h1{display:block;font-size:20px;font-weight:800;margin:6px 0 12px}
.p{line-height:1.8;color:#cfcfcf;font-size: 24rpx;}

.page-nav {
  position: sticky;
  top: 0;
  text-align: center;
  padding: 16px 0;
  z-index: 2;
}

.page-title {
  font-size: 20px;
  color: #fff;
}

.nav-back {
  position: absolute;
  width: 40rpx;
  height: 40rpx;
  display: flex;
  top: 44rpx;
}

.back-icon {
  font-size: 22pt;
  line-height: 1;
}
</style>

