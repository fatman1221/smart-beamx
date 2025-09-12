<template>
	<view class="phone-page">
		<view class="page-nav">
			<image class="nav-back" @click="goBack" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill" />
		</view>
		<view class="content-title">请输入新的手机号</view>
		<view class="input-area">
			<input class="phone-input" v-model="phoneNumber" placeholder="188 8888 8888" type="tel" maxlength="13"
				@input="formatPhone" confirm-type="done" />
		</view>
		<view class="submit-area">
			<button class="submit-btn" @click="submit">下一步</button>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'PhonePage',
		data() {
			return {
				phoneNumber: ''
			}
		},
		methods: {
			goBack() {
				uni.navigateBack({
					delta: 1
				})
			},
			formatPhone(e) {
				let value = e.detail.value.replace(/\D/g, '')
				if (value.length > 11) value = value.slice(0, 11)
				// 格式化为 188 8888 8888
				if (value.length > 3 && value.length <= 7) {
					value = value.slice(0, 3) + ' ' + value.slice(3)
				} else if (value.length > 7) {
					value = value.slice(0, 3) + ' ' + value.slice(3, 7) + ' ' + value.slice(7)
				}
				this.phoneNumber = value
			},
			submit() {
				const cleanPhone = this.phoneNumber.replace(/\s/g, '')
				if (!cleanPhone || cleanPhone.length !== 11) {
					uni.showToast({
						title: '请输入正确的手机号',
						icon: 'none'
					})
					return
				}
				uni.$emit('updatePhone', {
					phone: cleanPhone.replace(/(\d{3})(\d{4})(\d{4})/, '$1****$3')
				})
				uni.showToast({
					title: '手机号修改成功',
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
				this.currentPhone = decodeURIComponent(options.current)
			}
		}
	}
</script>

<style scoped>
	.phone-page {
		position: relative;
		background: #000;
		min-height: 100vh;
		color: #fff;
		padding: 20px;
	}

	.phone-page::before {
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
		z-index: 2;
	}

	.nav-back {
		position: absolute;
		top: 48rpx;
		width: 40rpx;
		height: 40rpx;
		display: flex;
		align-items: center;
		justify-content: center;
		color: #fff;
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
		margin: 72rpx 0 124rpx;
	}

	.input-area {
	position: relative;
		z-index: 1;
		margin: 0 24rpx 144rpx;
	}

	.phone-input {
		width: 100%;

		height: 96rpx;
		line-height: 96rpx;
		background: rgba(26, 26, 26, 1);
		border-radius: 24rpx;
		text-align: center;

		font-family: PingFang SC, PingFang SC;
		font-weight: 400;
		font-size: 28rpx;
		color: #FFFFFF;

		font-style: normal;
		text-transform: none;
	}

	.phone-input:focus {
		border-color: rgba(255, 255, 255, .4);
		background: rgba(255, 255, 255, .18);
	}

	.phone-input::placeholder {
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
		border: none;
		background: #3F3F3F;
		border-radius: 20rpx;
		font-weight: 600;
		font-size: 28rpx;
		color: #FFFFFF;
		text-align: center;
		font-style: normal;
		text-transform: none;
	}
</style>