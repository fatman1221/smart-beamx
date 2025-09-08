<template>

	<view class="custom-navbar" :style="{ paddingTop: statusBarHeight + 'rpx', height: navBarHeight + 'rpx' }">
		<view class="left" @click="goBack">
			<image class="nav-back" @click="goBack" src="@/static/icons/my/back2x.png" alt="" srcset=""
				mode="aspectFill" />
		</view>
		<view class="title" v-if="title">{{ title }}</view>
	</view>
</template>

<script>
	export default {
		name: "index",
		props: {
			title: {
				type: String,
				default: '标题'
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
				uni.navigateBack({
					delta: 1
				})
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
		width: 100%;
		position: fixed;
		z-index: 9999999;
		display: flex;
		justify-content: space-between;
		align-items: center;
		background-color:rgba(0, 0, 0, 0.5) !important;
		box-sizing: border-box;
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
	}
</style>