<template>
	<view class="email-page">
		<view class="page-nav">
			<image class="nav-back" @click="goBack" mode="aspectFill" src="@/static/icons/my/back2x.png" alt="" srcset="" />

		</view>
		<view class="content-title">设置邮箱</view>
		<view class="subtitle">{{ currentEmail }}</view>
		<view class="input-area">
			<input class="main-input" v-model="email" placeholder="user@gmail.com" type="email" confirm-type="done" />
		</view>
		<view class="submit-area">
			<button class="submit-btn" @click="submit">完成</button>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'EmailPage',
		data() {
			return {
				email: '',
				currentEmail: '188****5678@gmail.com'
			}
		},
		methods: {
			goBack() {
				uni.navigateBack({
					delta: 1
				})
			},
			submit() {
				if (!this.email || !/\S+@\S+\.\S+/.test(this.email)) {
					uni.showToast({
						title: '请输入正确的邮箱',
						icon: 'none'
					})
					return
				}
				uni.$emit('updateEmail', {
					email: this.email.replace(/(.{3}).+(@.+)/, '$1****$2')
				})
				uni.showToast({
					title: '邮箱修改成功',
					icon: 'success'
				})
				setTimeout(() => {
					uni.navigateBack({
						delta: 1
					})
				}, 800)
			}
		},
		onLoad(options) {
			if (options.current) {
				this.currentEmail = decodeURIComponent(options.current)
			}
		}
	}
</script>

<style scoped>
	.email-page {
		position: relative;
		background: #000;
		min-height: 100vh;
		color: #fff;
		padding: 20px;
	}

	.email-page::before {
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
		top: 48rpx;
	}

	.back-icon {
		font-size: 22pt;
		line-height: 1;
	}

	.content-title {
		position: relative;
		z-index: 1;
		text-align: left;
		color: #fff;
		height: 72rpx;
		font-family: PingFang SC, PingFang SC;
		font-weight: 600;
		font-size: 56rpx;
		color: #FFFFFF;
		line-height: 72rpx;
		text-align: left;
		font-style: normal;
		text-transform: none;
		margin: 72rpx 0 52rpx;
	}

	.subtitle {
		position: relative;
		z-index: 1;
		text-align: left;
		color: #ccc;
		font-size: 16px;


		font-family: PingFang SC, PingFang SC;
		font-weight: 400;
		font-size: 24rpx;
		color: rgba(255, 255, 255, 0.9);

		text-align: left;
		font-style: normal;
		text-transform: none;
		
		margin: 52rpx 0 24rpx 26rpx;
	}

	.input-area {
		position: relative;
		z-index: 1;
		margin: 0 24rpx 152rpx 26rpx;
	}

	.main-input {
		width: 100%;

		height: 96rpx;
		line-height: 96rpx;
		background: #1A1A1A;
		border-radius: 24rpx;
		text-align: center;

		font-family: PingFang SC, PingFang SC;
		font-weight: 400;
		font-size: 14px;
		color: #FFFFFF;

		font-style: normal;
		text-transform: none;
	}

	.main-input:focus {
		border-color: rgba(255, 255, 255, .4);
		background: rgba(255, 255, 255, .18);
	}

	.main-input::placeholder {
		color: rgba(255, 255, 255, .5);
	}

	.submit-area {
		position: relative;
		z-index: 1;
		margin: 0 26rpx;
	}

	.submit-btn {
		width: 100%;
		height: 96rpx;
		line-height: 96rpx;
		color: #fff;
		border: none;
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