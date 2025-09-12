<template>
	<view class="avatar-page">
		<view class="page-nav">
			<image class="nav-back" @click="goBack" src="@/static/icons/my/back2x.png" mode="aspectFill" alt="" srcset="" />
		</view>
		<view class="avatar-area">
			<image class="avatar-display" :src="avatar" mode="aspectFill" @click="selectAvatar"></image>
		</view>
		<view class="submit-area">
			<button class="submit-btn" @click="selectAvatar">更换头像</button>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'AvatarPage',
		data() {
			return {
				avatar: ''
			}
		},
		methods: {
			goBack() {
				uni.navigateBack({
					delta: 1
				})
			},
			selectAvatar() {
				uni.chooseImage({
					count: 1,
					sizeType: ['compressed'],
					sourceType: ['album', 'camera'],
					success: (res) => {
						this.avatar = res.tempFilePaths[0]
						uni.$emit('updateAvatar', {
							avatar: this.avatar
						})
						uni.showToast({
							title: '头像更新成功',
							icon: 'success'
						})
						setTimeout(() => {
							uni.navigateBack({
								delta: 1
							})
						}, 800)
					}
				})
			}
		},
		onLoad(options) {
			if (options.current) {
				this.avatar = decodeURIComponent(options.current)
			}
		}
	}
</script>

<style scoped>
	.avatar-page {
		position: relative;
		background: #000;
		min-height: 100vh;
		color: #fff;
		padding: 20px;
	}

	.avatar-page::before {
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
		top: 48rpx;
		width: 40rpx;
		height: 40rpx;
		display: flex;

		color: #fff;
	}

	.back-icon {
		font-size: 22pt;
		line-height: 1;
	}

	.avatar-area {
		position: relative;
		z-index: 1;
		display: flex;
		justify-content: center;
		margin-top: 80px;
		margin-bottom: 60px;
	}

	.avatar-display {
		width: 240rpx;
		height: 240rpx;
		border-radius: 50%;
		border: 3px solid rgba(255, 255, 255, .8);
	}

	.submit-area {
		position: relative;
		z-index: 1;
		margin: 0 20px;
	}

	.submit-btn {

		height: 96rpx;
		line-height: 96rpx;
		background: #3F3F3F;
		border-radius: 20rpx;


		font-family: PingFang SC, PingFang SC;
		font-weight: 600;
		font-size: 28rpx;
		color: #FFFFFF;

		text-align: center;
		font-style: normal;
		text-transform: none;

	}
</style>