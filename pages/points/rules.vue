<template>
  <view class="rules-page">
    <view class="tabs">
      <view class="tab" :class="{active: cur===0}" @click="cur=0">获取积分</view>
      <view class="tab" :class="{active: cur===1}" @click="cur=1">消耗积分</view>
    </view>
    <scroll-view scroll-y class="list">
      <view class="item" v-for="i in 6" :key="i">
        <view class="left">
          <text class="title">签到</text>
          <text class="time">07月05日12:25</text>
        </view>
        <text class="delta">+150</text>
      </view>
    </scroll-view>
  </view>
</template>

<script>
export default {data: () => ({cur: 0})}
</script>

<style scoped>
.rules-page {
  background: #000;
  min-height: 100vh;
  color: #fff
}

.tabs {
  display: flex;
  justify-content: space-around;
  padding: 14px 0;
  border-bottom: 1px solid #222
}

.tab {
  color: #bdbdbd;
  position: relative;
  padding-bottom: 6px
}

.tab.active {
  color: #fff
}

.tab.active::after {
  content: '';
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  bottom: 0;
  width: 16px;
  height: 3px;
  background: #fff;
  border-radius: 2px
}

.list {
  padding: 14px 16px 24px
}

.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #1A1A1A;;
  border: 1px solid #2f2f2f;
  border-radius: 12rpx;
  padding: 16px;
  margin-bottom: 12px
}

.title {
  font-size: 16px;
  font-weight: 700
}

.time {
  display: block;
  color: #9a9a9a;
  margin-top: 6px
}

.delta {
  font-size: 20px;
  font-weight: 800
}
</style>

