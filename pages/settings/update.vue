<template>
	<view class="update-page">
		<view class="page-nav">
			<image class="nav-back" @click="goBack" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill" />
			<text class="page-title">版本号</text>
		</view>
		<view class="update-card">
			<view class="icon"></view>
			<view class="tip">
				发现新版本
			</view>
			<view class="row">
				<view class="info">
					<view class="version-header">
						<text class="ver">新版本</text>
						<view class="update-dot"></view>
					</view>
					<view class="size">1.0.123</view>
				</view>
				<image class="setting-arrow" src="@/static/icons/my/back2x.png" alt="" srcset=""  mode="aspectFill"/>
			</view>
		</view>
		<view class="btn-wrap">
			<button class="btn" @click="install">检查更新</button>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'UpdatePage',
		data() {
			return {
				version: '1.0.2',
				sizeMB: '32.25'
			}
		},
		methods: {
			goBack() {
				uni.navigateBack({
					delta: 1
				})
			},
			install() {
				uni.showToast({
					title: '开始安装…',
					icon: 'success'
				})
			}
		}
	}
</script>

<style scoped>
	.update-page {
		position: relative;
		background: #000;
		min-height: 100vh;
		color: #fff;
		padding: 20px;
	}

	.update-page::before {
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

	/* 居中留位，不显示文案 */
	.nav-back {
		position: absolute;
		width: 40rpx;
		height: 40rpx;
		display: flex;
		margin-top: 8rpx;
	}

	.setting-arrow {
		margin-left: auto;
		width: 36rpx;
		height: 36rpx;
		transform: rotateY(180deg);
		opacity: 0.5;
		margin-top: 20rpx;
		margin-right: 34rpx;
	}

	.back-icon {
		font-size: 22pt;
		line-height: 1;
	}

	.update-card {
    margin-left: 12rpx;
    margin-right: 12rpx;

		background: rgba(255, 255, 255, .06);
		border: 1px solid rgba(255, 255, 255, .12);
		border-radius: 24rpx;
		backdrop-filter: blur(18px);
		position: relative;
		z-index: 1;
	}

	.row {
		display: flex;
		margin-top: 20rpx;
		margin-bottom: 32rpx;
		padding-left: 32rpx;
	}

	.icon {
		width: 200rpx;
		height: 200rpx;
		background: #D9D9D9;
		border-radius: 24rpx;
		opacity: 0.5;
		margin-top: 26rpx;
    margin-left: 236rpx;

	}

	.tip {
		width: 100%;
		text-align: center;
		font-family: PingFang SC, PingFang SC;
		font-weight: 500;
		font-size: 28rpx;
		color: rgba(255, 255, 255, 0.9);
		font-style: normal;
		text-transform: none;
    margin-top: 20rpx;
	}

	.info {
		display: flex;
		flex-direction: column;
		flex: 1;
	}

	.version-header {
		display: flex;
		align-items: center;
		gap: 12rpx;
		margin-bottom: 8rpx;
	}

	.ver {
		font-family: PingFang SC, PingFang SC;
		font-weight: 500;
		font-size: 28rpx;
		color: #FFFFFF;
		text-align: left;
		font-style: normal;
		text-transform: none;
	}

	.update-dot {
		width: 12rpx;
		height: 12rpx;
		background: #FF3B30;
		border-radius: 50%;
		flex-shrink: 0;
	}

	.size {
		font-family: PingFang SC, PingFang SC;
		font-weight: 400;
		font-size: 24rpx;
		color: #FFFFFF;
		text-align: left;
		font-style: normal;
		text-transform: none;
		opacity: 0.6;
	}

	.desc-title {
		margin-top: 12px;
		font-size: 16px;
		color: #ccc;
	}

	.btn-wrap {
		position: relative;
		z-index: 1;
		display: flex;
		justify-content: center;
		align-items: center;
    margin-top: 74rpx;
	}

	.btn {
		width: 100%;
		background: rgba(255, 255, 255, .18);
		height: 96rpx;
		border: none;
		border-radius: 20rpx;
		font-family: PingFang SC, PingFang SC;
		font-weight: 600;
		font-size: 28rpx;
		color: #FFFFFF;
		text-align: center;
		font-style: normal;
		text-transform: none;
		padding: 0 !important;
		display: flex;
		align-items: center;
		justify-content: center;
	}
</style>