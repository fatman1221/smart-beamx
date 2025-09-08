<template>
  <view class="invite-page">
    <!-- 背景遮罩 -->
    <view class="overlay" @click="goBack"></view>
    
    <!-- 分享面板 -->
    <view class="share-panel">
      <!-- 分享标题 -->
      <view class="share-title">分享</view>
      
      <!-- 分享平台网格 -->
      <view class="share-grid">
        <view class="platform-item" @click="shareToTwitter">
          <view class="platform-icon twitter">
            <image src="/static/icons/Twitter.svg" mode="aspectFit"></image>
          </view>
          <text class="platform-name">Twitter</text>
        </view>
        
        <view class="platform-item" @click="shareToFacebook">
          <view class="platform-icon facebook">
            <image src="/static/icons/Facebook.svg" mode="aspectFit"></image>
          </view>
          <text class="platform-name">Facebook</text>
        </view>
        
        <view class="platform-item" @click="shareToWeChat">
          <view class="platform-icon wechat">
            <image src="/static/icons/wechat.svg" mode="aspectFit"></image>
          </view>
          <text class="platform-name">微信</text>
        </view>
        
        <view class="platform-item" @click="shareToLine">
          <view class="platform-icon line">
            <image src="/static/icons/LIne.svg" mode="aspectFit"></image>
          </view>
          <text class="platform-name">Line</text>
        </view>
        
        <view class="platform-item" @click="shareToWhatsApp">
          <view class="platform-icon whatsapp">
            <image src="/static/icons/Whatapp.svg" mode="aspectFit"></image>
          </view>
          <text class="platform-name">WhatsApp</text>
        </view>
        
        <view class="platform-item" @click="shareToSMS">
          <view class="platform-icon sms">
            <image src="/static/icons/SMS.svg" mode="aspectFit"></image>
          </view>
          <text class="platform-name">短信</text>
        </view>
      </view>
      
      <!-- 分割线 -->
      <view class="divider"></view>
      
      <!-- 取消按钮 -->
      <view class="cancel-area">
        <button class="cancel-btn" @click="goBack">取消</button>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  name: 'InvitePage',
  data() {
    return {}
  },
  methods: {
    goBack() {
      uni.switchTab({
        url: '/pages/tabBar/my/my'
      })
    },
    shareToTwitter() {
      this.performShare('Twitter', 'twitter')
    },
    shareToFacebook() {
      this.performShare('Facebook', 'facebook')
    },
    shareToWeChat() {
      this.performShare('微信', 'wechat')
    },
    shareToLine() {
      this.performShare('Line', 'line')
    },
    shareToWhatsApp() {
      this.performShare('WhatsApp', 'whatsapp')
    },
    shareToSMS() {
      this.performShare('短信', 'sms')
    },
    performShare(platform, type) {
      // 这里可以集成真实的分享SDK
      uni.showToast({ 
        title: `分享到${platform}`, 
        icon: 'success',
        duration: 1500
      })
      
      // 模拟分享成功后的操作
      setTimeout(() => {
        this.goBack()
      }, 1500)
    }
  },
  onLoad() {
    console.log('邀请好友页面加载')
  }
}
</script>

<style scoped>
.invite-page { 
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 1000;
  display: flex;
  align-items: flex-end;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

.share-panel {
  width: 100%;
  background: #1a1a1a;
  border-radius: 24rpx 24rpx 0 0;
  padding: 32rpx 0 0;
  position: relative;
  z-index: 1001;
  animation: slideUp 0.3s ease-out;
}

@keyframes slideUp {
  from {
    transform: translateY(100%);
  }
  to {
    transform: translateY(0);
  }
}

.share-title { 
  text-align: center; 
  color: #fff;
  font-size: 36rpx; 
  font-weight: 600; 
  margin: 0 0 40rpx 0;
  padding: 0 32rpx;
}

.share-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32rpx;
  padding: 0 32rpx 40rpx;
}

.platform-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 24rpx 16rpx;
  background: transparent;
  border-radius: 16rpx;
  transition: all 0.2s ease;
  cursor: pointer;
}

.platform-item:active {
  background: rgba(255, 255, 255, 0.1);
  transform: scale(0.95);
}

.platform-icon {
  width: 80rpx;
  height: 80rpx;
  margin-bottom: 16rpx;
  border-radius: 20rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.1);
}

.platform-icon.twitter {
  background: #1da1f2;
}

.platform-icon.facebook {
  background: #1877f2;
}

.platform-icon.wechat {
  background: #07c160;
}

.platform-icon.line {
  background: #00c300;
}

.platform-icon.whatsapp {
  background: #25d366;
}

.platform-icon.sms {
  background: #34c759;
}

.platform-icon image {
  width: 40rpx;
  height: 40rpx;
}

.platform-name {
  font-size: 24rpx;
  color: #fff;
  text-align: center;
  font-weight: 500;
}

.divider {
  height: 1rpx;
  background: rgba(255, 255, 255, 0.1);
  margin: 0 32rpx 24rpx;
}



.cancel-btn {
  width: 100%;
  padding: 24rpx;
  background: #1a1a1a;
  color: #fff;
  border: none;
  font-size: 32rpx;
  font-weight: 500;
  transition: all 0.2s ease;
  outline: none;
  box-shadow: none;
}

.cancel-btn:active {
  background: rgba(255, 255, 255, 0.2);
  transform: scale(0.98);
}
</style>