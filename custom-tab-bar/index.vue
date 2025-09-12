<template>
  <view class="custom-tab-bar">
    <view 
      v-for="(item, index) in tabList" 
      :key="index"
      class="tab-item"
      :class="{ active: activeTab === index }"
      @click="switchTab(index)"
    >
      <view class="tab-icon">
        <image 
          :src="activeTab === index ? item.selectedIcon : item.icon" 
          class="icon-image" 
          mode="aspectFit"
          @error="handleImageError"
        />
      </view>
      <text class="tab-text">{{ item.text }}</text>
    </view>
  </view>
</template>

<script>
export default {
  name: 'CustomTabBar',
  data() {
    return {
      activeTab: 0,
      tabList: [
        {
          pagePath: 'pages/tabBar/home/home',
          text: '首页',
          icon: '/static/tabbar/home.png',
          selectedIcon: '/static/tabbar/home-active.png'
        },
        {
          pagePath: 'pages/tabBar/mode/mode',
          text: '模式',
          icon: '/static/tabbar/mode.png',
          selectedIcon: '/static/tabbar/mode-active.png'
        },
        {
          pagePath: 'pages/tabBar/scene/scene',
          text: '场景',
          icon: '/static/tabbar/scene.png',
          selectedIcon: '/static/tabbar/scene-active.png'
        },
        {
          pagePath: 'pages/tabBar/shop/shop',
          text: '商城',
          icon: '/static/tabbar/shop.png',
          selectedIcon: '/static/tabbar/shop-active.png'
        },
        {
          pagePath: 'pages/tabBar/my/my',
          text: '我的',
          icon: '/static/tabbar/my.png',
          selectedIcon: '/static/tabbar/my-active.png'
        }
      ]
    }
  },
  methods: {
    switchTab(index) {
      if (this.activeTab === index) return
      
      this.activeTab = index
      const item = this.tabList[index]
      
      console.log('切换到页面:', item.pagePath)
      
      // 使用 redirectTo 替代 switchTab，因为已经删除了 tabBar 配置
      uni.redirectTo({
        url: `/${item.pagePath}`,
        success: () => {
          console.log('页面跳转成功:', item.pagePath)
        },
        fail: (err) => {
          console.error('页面跳转失败:', err)
        }
      })
    },
    
    updateActiveTab() {
      const pages = getCurrentPages()
      if (pages.length === 0) return
      
      const currentPage = pages[pages.length - 1]
      const route = currentPage.route
      
      const index = this.tabList.findIndex(item => item.pagePath === route)
      if (index !== -1) {
        this.activeTab = index
      }
    },
    
    handleImageError(e) {
      console.error('图标加载失败:', e)
    }
  },
  
  mounted() {
    console.log('自定义tabBar已加载')
    console.log('tabList:', this.tabList)
    console.log('图标路径检查:')
    this.tabList.forEach((item, index) => {
      console.log(`Tab ${index}:`, {
        text: item.text,
        icon: item.icon,
        selectedIcon: item.selectedIcon
      })
    })
    this.updateActiveTab()
  },
  
  onShow() {
    console.log('自定义tabBar显示')
    this.updateActiveTab()
  }
}
</script>

<style scoped>
.custom-tab-bar {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  height: 144rpx;
  background-color: rgba(26, 26, 26, 1);
  border-top: 1rpx solid #333333;
  border-radius: 24rpx 24rpx 0 0;
  display: flex;
  z-index: 1000;
  padding-bottom: env(safe-area-inset-bottom);

}

.tab-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  gap: 8rpx;
  transition: all 0.3s ease;
  color: #666666;
  padding: 16rpx 0 8rpx 0;
  cursor: pointer;

}

.tab-item:active {
  transform: scale(0.95);
}

.tab-item.active {
  color: #ffffff;
}

.tab-icon {
  width: 48rpx;
  height: 48rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 24rpx;
  transition: all 0.3s ease;
  margin-bottom: 10rpx;
}

.tab-item.active .tab-icon {
  background-color: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10rpx);
}

.icon-image {
  width: 48rpx;
  height: 48rpx;
  display: block;

}

.tab-text {
  font-size: 24rpx;
  line-height: 1;
  font-weight: 500;
}

/* 适配不同屏幕 */


</style>
