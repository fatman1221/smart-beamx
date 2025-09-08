<template>
	<view class="settings-page">
		<view class="page-nav">

			<image class="nav-back" @click="goBack" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill" />

			<text class="page-title">设置</text>
		</view>
		<!-- 语言和通知设置容器 -->
		<view class="settings-group">
			<!-- 语言设置 -->
			<view class="setting-item" @click="goLanguage">
				<view class="setting-info">
					<text class="setting-label">语言</text>
				</view>
				<view class="setting-control">

					<image class="setting-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill" />
				</view>
			</view>

			<!-- 消息通知 -->
			<view class="setting-item notification-item">
				<view class="setting-info">
					<text class="setting-label">消息通知</text>
				</view>
				<view class="setting-control notification-control">
					<switch :checked="notificationEnabled" @change="toggleNotification" color="#FE7E00"
                  style="transform:scale(0.7) ;  "



          />
				</view>
			</view>
		</view>

		<!-- 版本信息容器 -->
		<view class="settings-group">
			<!-- 版本信息 -->
			<view class="setting-item" @click="goUpdate">
				<view class="setting-info">
					<text class="setting-label">版本号</text>
				</view>
				<view class="setting-control">
					<text class="version-number">{{ appVersion }}</text>
					<image class="setting-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill" />
				</view>
			</view>
		</view>

		<!-- 退出登录按钮 -->
		<view class="logout-section">
			<view class="logout-button" @click="logout">
				<text class="logout-text">退出登录</text>
			</view>
		</view>

		<!-- 语言选择弹窗 -->
		<view v-if="showLanguageModal" class="modal-overlay" @click="closeLanguageModal">
			<view class="modal-content" @click.stop>
				<view class="modal-header">
					<text class="modal-title">选择语言</text>
					<text class="modal-close" @click="closeLanguageModal">×</text>
				</view>
				<view class="modal-body">
					<view v-for="language in languages" :key="language.value" class="language-item"
						:class="{ active: currentLanguage === language.value }" @click="switchLanguage(language.value)">
						<text class="language-name">{{ language.label }}</text>
						<text v-if="currentLanguage === language.value" class="selected-icon">✓</text>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'SettingsPage',
		data() {
			return {
				currentLanguage: 'zh-CN',
				languages: [{
						label: '简体中文',
						value: 'zh-CN'
					},
					{
						label: 'English',
						value: 'en-US'
					}
				],
				notificationEnabled: true,
				appVersion: '1.0.0',
				showLanguageModal: false
			}
		},
		computed: {
			currentLanguageLabel() {
				const language = this.languages.find(lang => lang.value === this.currentLanguage)
				return language ? language.label : '简体中文'
			}
		},
		methods: {
			goBack() {
				const pages = getCurrentPages && getCurrentPages()
				if (pages && pages.length > 1) {
					uni.navigateBack({
						delta: 1
					})
				} else {
					uni.switchTab({
						url: '/pages/tabBar/my/my'
					})
				}
			},
			goLanguage() {
				uni.navigateTo({
					url: '/pages/settings/language'
				})
			},
			goUpdate() {
				uni.navigateTo({
					url: '/pages/settings/update'
				})
			},
			switchLanguage(language) {
				this.currentLanguage = language
				this.closeLanguageModal()
				uni.showToast({
					title: '语言设置已保存',
					icon: 'success'
				})
			},
			closeLanguageModal() {
				this.showLanguageModal = false
			},
			toggleNotification(e) {
				this.notificationEnabled = e.detail.value
				uni.showToast({
					title: this.notificationEnabled ? '已开启消息通知' : '已关闭消息通知',
					icon: 'success'
				})
			},
			checkUpdate() {
				uni.showLoading({
					title: '检查更新中...'
				})

				setTimeout(() => {
					uni.hideLoading()
					uni.showModal({
						title: '检查更新',
						content: '当前已是最新版本',
						showCancel: false
					})
				}, 2000)
			},
			logout() {
				uni.showModal({
					title: '退出登录',
					content: '确定要退出登录吗？',
					confirmText: '退出',
					cancelText: '取消',
					confirmColor: '#FF3B30',
					success: (res) => {
						if (res.confirm) {
							// 清除本地存储的用户信息
							uni.removeStorageSync('userInfo')
							uni.removeStorageSync('token')
							uni.removeStorageSync('isLoggedIn')
							
							// 显示退出成功提示
							uni.showToast({
								title: '已退出登录',
								icon: 'success',
								duration: 1500
							})
							
							// 延迟跳转到登录页面
							setTimeout(() => {
								uni.reLaunch({
									url: '/pages/login/login'
								})
							}, 1500)
						}
					}
				})
			}
		},
		onLoad() {
			console.log('设置页面加载')
		}
	}
</script>

<style scoped>
	.settings-page {
		position: relative;
		background: #000;
		min-height: 100vh;
		color: #fff;
		padding: 20px;
	}

	.settings-page::before {
		content: '';
		position: absolute;
		inset: 0;
		background: url('/static/icons/background.svg') center/cover no-repeat;
		opacity: .99;
		pointer-events: none;
		z-index: 0;
	}

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
		margin-top: 8rpx;
	}


  /* container：把顶部间距放在容器 padding 上（统一管理） */
  .settings-group {
    position: relative;
    z-index: 1;
    margin-bottom: 24rpx;
    background: #1A1A1A;
    border-radius: 32rpx;
    box-sizing: border-box;

    /* 关键：顶部 12rpx，右 20rpx，底部 16rpx，左 32rpx（你要的左内边距） */
    padding: 12rpx 20rpx 16rpx 32rpx;
  }

  /* 每个 item 固定高度 92rpx，去掉垂直内边距，靠 flex 垂直居中 */
  .setting-item {
    display: flex;
    justify-content: space-between;
    align-items: center;

    /* 固定高度 */
    height: 92rpx;

    /* 很重要：不要再用 vertical padding，否则会超高 */
    padding: 0;

    /* 让 item 内部的宽度按容器内边距来布局 */
    box-sizing: border-box;
    border-bottom: none;
    margin: 0; /* 清除多余外边距 */
  }

  /* 如果你之前用了 first-child 的 margin-top，请移除它（下行可删） */
  /* .setting-item:first-child { margin-top: 12rpx; }  <-- 不需要了 */

  /* 左侧信息区域保持伸缩 */
  .setting-info {
    display: flex;
    align-items: center;
    flex: 1;
  }

  /* label 不要用绝对定位，移除 height/left，交给 flex 居中 */
  .setting-label {
    /* 移除 height/line-height 的强制值以避免布局冲突 */
    height: auto;
    line-height: normal;

    font-family: "PingFang SC", PingFang SC;
    font-weight: 500;
    font-size: 28rpx;
    color: rgba(255, 255, 255, 0.9);
    text-align: left;
    margin: 0; /* 避免浏览器默认间距 */
  }

  /* 右侧控制（箭头 / switch）如果需要微调位置可以用 margin-right */
  .setting-control {
    display: flex;
    align-items: center;
    gap: 8rpx; /* 控件之间的间距 */
    margin-right: 0; /* 已由容器右 padding 控制距离 */
  }

  /* 消息通知按钮特殊样式 - 与上方前进按钮对齐 */
  .notification-control {
    margin-right: 0;
    padding-right: 0;
  }

  /* 你的 image 箭头或 icon 大小 */
  .setting-arrow {
    width: 28rpx;
    height: 28rpx;
  }

  /* switch 缩放会影响其视觉大小，但不改变父高度（父高度固定） */


	.version-info {
		display: flex;
		flex-direction: column;
	}

	.version-number {
		font-size: 12px;
		color: #666666;
		margin-top: 2px;
	}

	.setting-control {
		display: flex;
		align-items: center;
		gap: 8px;
	}



	.setting-value {
		font-size: 14px;
		color: #999999;
	}

	.setting-arrow {
		width: 36rpx;
		height: 36rpx;

		transform: rotateY(180deg);
		opacity: 0.5;
	}

	/* 弹窗样式 */
	.modal-overlay {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background-color: rgba(0, 0, 0, 0.7);
		display: flex;
		align-items: center;
		justify-content: center;
		z-index: 1000;
	}

	.modal-content {
		background-color: #1a1a1a;
		border-radius: 12px;
		width: 80%;
		max-width: 400px;
		border: 1px solid #333333;
	}

	.modal-header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 20px;
		border-bottom: 1px solid #333333;
	}

	.modal-title {
		font-size: 18px;
		font-weight: bold;
		color: #ffffff;
	}

	.modal-close {
		font-size: 24px;
		color: #666666;
	}

	.modal-body {
		padding: 20px;
	}

	.language-item {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 16px 0;
		border-bottom: 1px solid #333333;
	}

	.language-item:last-child {
		border-bottom: none;
	}

	.language-item.active {
		background-color: rgba(0, 122, 255, 0.1);
	}

	.language-name {
		font-size: 16px;
		color: #ffffff;
	}

	.selected-icon {
		font-size: 16px;
		color: #007AFF;
	}

	/* 退出登录按钮样式 */
	.logout-section {
		position: relative;
		z-index: 1;
		margin-top: 864rpx;
		margin-left: 12rpx;
		margin-right: 12rpx;
		padding: 0;
	}

	.logout-button {
		width: 100%;
		height: 88rpx;
		background: rgba(63, 63, 63, 1);
		border-radius: 20rpx;
		display: flex;
		align-items: center;
		justify-content: center;
		cursor: pointer;
		transition: all 0.3s ease;
	}

	.logout-button:active {
		transform: scale(0.98);
		background: rgba(63, 63, 63, 0.8);
	}

	.logout-text {
		font-size: 32rpx;
		color: #ffffff;
		font-weight: 500;
		text-align: center;
	}
</style>