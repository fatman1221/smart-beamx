<template>
	<view class="nickname-page">
		<view class="page-nav">
			<image class="nav-back" @click="goBack" src="@/static/icons/my/back2x.png" alt="" mode="aspectFill" srcset="" />
		</view>
		<view class="content-title">设置昵称</view>
		<view class="input-area">
			<input class="main-input" v-model="nickname" placeholder="请输入昵称" maxlength="20" confirm-type="done" />
		</view>
		<view class="submit-area">
			<button class="submit-btn" @click="submit">完成</button>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'NicknamePage',
		data() {
			return {
				nickname: ''
			}
		},
		methods: {
			goBack() {
				uni.navigateBack({
					delta: 1
				})
			},
			submit() {
				const name = (this.nickname || '').trim()
				if (!name) {
					uni.showToast({
						title: '请输入昵称',
						icon: 'none'
					})
					return
				}
				// 通过事件传递昵称更新
				uni.$emit('updateNickname', {
					nickname: name
				})
				uni.showToast({
					title: '昵称修改成功',
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
				this.nickname = decodeURIComponent(options.current)
			}
		}
	}
</script>

<style scoped>
	.nickname-page {
		position: relative;
		background: #000;
		min-height: 100vh;
		color: #fff;
		padding: 20px;
	}

	.nickname-page::before {
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
		padding: 16px 0;

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

	.content-title {
		width: 100%;
		position: relative;
		z-index: 1;
		text-align: left;
		color: #fff;
		font-size: 28px;
		font-weight: 600;
		margin: 60px 0 0 0;
	}

	.input-area {
		position: relative;
		z-index: 1;
		margin: 124rpx 24rpx 0;
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
		margin: 144rpx 24rpx;
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