<template>
	<view class="lang-page">
		<view class="page-nav">
			<image class="nav-back" @click="goBack" src="@/static/icons/my/back2x.png" alt="" mode="aspectFill" srcset="" />
			<text class="page-title">语言</text>
		</view>
		<view class="lang-card">
			<view class="lang-item" :class="{active: current==='zh-CN'}" @click="setLang('zh-CN')">
				<text class="lang-name">简体中文</text>
				<image class="ok" v-if="current==='zh-CN'" src="@/static/icons/my/check.png" alt="" mode="aspectFill" srcset="" />
			</view>
			<view class="lang-item" :class="{active: current==='en-US'}" @click="setLang('en-US')">
				<text class="lang-name">英文</text>

				<image class="ok" v-if="current==='en-US'" src="@/static/icons/my/check.png" alt="" srcset=""  mode="aspectFill"/>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'LanguageSettings',
		data() {
			return {
				current: 'zh-CN'
			}
		},
		methods: {
			goBack() {
				uni.navigateBack({
					delta: 1
				})
			},
			setLang(v) {
				this.current = v
				uni.showToast({
					title: '已保存',
					icon: 'success'
				})
			}
		}
	}
</script>

<style scoped>
	.lang-page {
		position: relative;
		background: #000;
		min-height: 100vh;
		color: #fff;
		padding: 20px;
	}

	.lang-page::before {
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

	.back-icon {
		font-size: 22pt;
		line-height: 1;
	}

	.lang-card {
		position: relative;
		z-index: 1;
		padding: 8px 0;
		background: rgba(26, 26, 26, 1);
		border-radius: 16px;
		backdrop-filter: blur(18px);
	}

	.lang-item {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 26rpx 32rpx;
	}



	.lang-item.active {
		background: transparent;
	}

	.lang-name {

		font-family: PingFang SC, PingFang SC;
		font-weight: 500;
		font-size: 28rpx;
		color: rgba(255, 255, 255, 0.9);
		text-align: left;
		font-style: normal;
		text-transform: none;
	}

	.ok {
		width: 32rpx;
		height: 32rpx;
	}
</style>