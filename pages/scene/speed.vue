<template>
  <view class="speed-detail-page">
    <view class="page-nav">
      <image class="nav-back" @click="goBack" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill" />
    </view>
    
    <view class="content">
      <view class="measurement-display">
        <text class="value">0</text>
        <text class="unit">mph</text>
      </view>
      <text class="label">速度</text>
    </view>
  </view>
</template>

<script>
export default {
  name: 'SpeedDetailPage',
  data() {
    return {
      speed: 0
    }
  },
  methods: {
    goBack() {
      uni.navigateBack()
    }
  }
}
</script>

<style scoped>
.speed-detail-page {
  background: #000;
  min-height: 100vh;
  color: #fff;
  position: relative;
}

.page-nav {
  position: sticky;
  top: 48rpx;
  text-align: center;
  padding: 16rpx 0;
  margin-bottom: 44rpx;
  z-index: 2;
}

.page-title {
  font-size: 36rpx;
  color: #ffffff;
}

.nav-back {
  position: absolute;
  width: 40rpx;
  height: 40rpx;
  display: flex;
  margin-top: 8rpx;
  margin-left: 24rpx;
}

.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.measurement-display {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 40rpx;
}

.value {
  font-size: 128rpx;
  font-weight: 300;
  color: #ffffff;
  line-height: 1;
}

.unit {
  font-size: 32rpx;
  font-weight: 300;
  color: #ffffff;
  margin-left: 20rpx;
  line-height: 1;
}

.label {
  font-size: 32rpx;
  color: #ffffff;
  font-weight: 400;
}
</style>
