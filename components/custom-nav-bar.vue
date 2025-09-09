<template>

	<view class="custom-navbar" :style="{ paddingTop: statusBarHeight + 'rpx', height: navBarHeight + 'rpx' }">
		<view class="left" @click="goBack">
			<image class="nav-back" @click="goBack" src="@/static/icons/my/back2x.png" alt="" srcset=""
				mode="aspectFill" />
		</view>
		<view class="title" v-if="title">{{ title }}</view>
		<view class="right" v-if="showSave">
			<button class="save-btn" @click="handleSave">保存</button>
		</view>
	</view>
</template>

<script>
	export default {
		name: "index",
		props: {
			title: {
				type: String,
				default: '标题'
			},
			onBack: {
				type: Function,
				default: null
			},
			showSave: {
				type: Boolean,
				default: false
			}
		},
		data() {
			return {
				statusBarHeight: 0,
				navBarHeight: 0
			};
		},

		mounted() {
			this.getHeight()

		},
		methods: {
			goBack() {
				if (this.onBack && typeof this.onBack === 'function') {
					this.onBack()
				} else {
					uni.navigateBack({
						delta: 1
					})
				}
			},
			handleSave() {
				this.$emit('save')
			},
			getHeight() {
				const systemInfo = uni.getSystemInfoSync();
				this.statusBarHeight = systemInfo.statusBarHeight; // 获取状态栏高度
				if (systemInfo.platform === 'android') {
					this.navBarHeight = this.statusBarHeight + 96; // Android 导航栏高度
				} else {
					this.navBarHeight = this.statusBarHeight + 88; // iOS 导航栏高度
				}
			},
		}
	}
</script>

<style scoped>
	.navBarBox {
		position: fixed;
		z-index: 999999;
	}

	.nav-back {
		position: absolute;
		width: 40rpx;
		height: 40rpx;
		top: 34%;
		left: 48rpx;
	
	}

	.custom-navbar {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    background: transparent; /* 完全透明 */

    backdrop-filter: blur(20px);
    border-bottom: none;
    z-index: 999;
	}

	.left,
	.right {
		width: 60rpx;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.title {
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
		/* 50%为自身尺寸的一半 */
		text-align: center;
		font-size: 36rpx;
		font-weight: bold;
		color: #ffffff;
		text-shadow: 0 1px 3px rgba(0, 0, 0, 0.5);
	}

	.right {
		position: absolute;
		right: 48rpx;
		top: 50%;
		transform: translateY(-50%);
	}

	.save-btn {
		background: transparent;
		color: rgba(255, 255, 255, 1);
		border: none;
		font-size: 24rpx;
		font-weight: 500;
		white-space: nowrap;
		padding: 8rpx 16rpx;
		min-width: 60rpx;
	}
</style>