<template>
	<view class="home-page">
		<!-- 顶部头图+标题区 -->
		<view class="hero">
			<view class="hero-inner">
				<!-- 顶部标题 -->
				<!--        <view class="hero-top">
          <text class="app-title">智能汽车灯</text>
        </view> -->
				<!-- 操作行：添加设备（左） 开关（右） -->
				<view class="ops-row">
					<image src="@/static/icons/home/add-device2x.png" class="add-active-icon" alt="" srcset="" mode="aspectFill" />
					<text class="add-device" @click="goAddDevice">添加设备</text>
					<image class="close" src="@/static/icons/home/close2x.png" alt="" srcset="" mode="aspectFill" />
				</view>

				<!-- 顶部设备标签 -->
				<scroll-view class="chip-scroll" scroll-x>
					<view class="chip" v-for="(c,i) in deviceChips" :key="i" :class="{active: currentChip===i}"
						@click="selectChip(i)">{{ c }}</view>
					<view class="chip add" @click="goAddDevice">＋</view>
				</scroll-view>

				<!-- LED 行下：左灯泡 右加号 -->
				<view class="light-row">
					<image class="light-icon" src="@/static/icons/home/light-bulb-icon.png" alt="" srcset="" mode="aspectFill" />
					<text class="light-plus" @click="onAddLight">＋</text>
				</view>
			</view>
		</view>

		<!-- 模式卡片栅格 -->
		<view class="mode-grid">
			<view class="mode-card" v-for="(m,idx) in modes" :key="m.id" @click="openMode(m)">

				<image class="mode-icon" :src="m.icon" alt="" srcset="" mode="aspectFill" />
				<view class="mode-head">
					<text class="mode-name">{{ m.name }}</text>
					<image class="mode-arrow" src="@/static/icons/my/back2x.png" alt="" srcset=""  mode="aspectFill"/>
				</view>
				<view class="mode-color" :style="{background:m.bg}"></view>

			</view>
		</view>
		<CustomTabBar />
	</view>
</template>

<script>
import CustomTabBar   from "../../../custom-tab-bar/index.vue";

import mode1 from "@/static/icons/home/mode-1-icon2x.png"
	import mode2 from "@/static/icons/home/mode-2-icon2x.png"
	import mode3 from "@/static/icons/home/mode-3-icon2x.png"
	import mode4 from "@/static/icons/home/mode-4-icon2x.png"
	export default {
		name: 'HomePage',
		components: {CustomTabBar},
		data() {
			return {
				powerOn: true,
				currentChip: 0,
				deviceChips: ['LED 1', 'LED 2', 'LED 3', 'LED 4', 'LED 5'],
				modes: [{
						id: 1,
						name: '模式名称1',
						bg: 'linear-gradient(90deg,#ff6aa6,#60d3ff)',
						icon: mode1
					},
					{
						id: 2,
						name: '模式名称2',
						bg: 'linear-gradient(90deg,#ff9a3c,#f0de62)',
						icon: mode2
					},
					{
						id: 3,
						name: '模式名称3',
						bg: 'linear-gradient(90deg,#40e0a1,#36a3a3)',
						icon: mode3
					},
					{
						id: 4,
						name: '模式名称4',
						bg: 'linear-gradient(90deg,#7c5cff,#ff3b6b)',
						icon: mode4
					}
				]
			}
		},
		onLoad() {
			console.log('首页加载')
		},
		methods: {
			goAddDevice() {
				uni.navigateTo({
					url: '/pages/device/connect/connect'
				})
			},
			togglePower() {
				this.powerOn = !this.powerOn
				uni.showToast({
					title: this.powerOn ? '已开启' : '已关闭',
					icon: 'none'
				})
			},
			onAddLight() {
				uni.showToast({
					title: '添加灯组',
					icon: 'none'
				})
			},
			selectChip(i) {
				this.currentChip = i
			},
			openMode(m) {
				uni.switchTab({
					url: '/pages/tabBar/mode/mode'
				})
			}
		}
	}
</script>

<style scoped>
	.home-page {
		background: #000;
		min-height: 100vh;
		color: #fff;
		padding: 0 16px 24px
	}

	.hero {
		position: relative;
		margin: 0 -16px 16px -16px;
		padding: 28px 16px 16px;
		background: radial-gradient(80% 60% at 100% 0%, rgba(255, 255, 255, 0.04), rgba(255, 255, 255, 0) 60%), radial-gradient(70% 60% at 0% 0%, rgba(255, 255, 255, 0.04), rgba(255, 255, 255, 0) 60%)
	}

	.hero::before {
		content: '';
		position: absolute;
		inset: 0;
		background: repeating-linear-gradient(140deg, rgba(255, 255, 255, 0.04) 0, rgba(255, 255, 255, 0.04) 2px, transparent 2px, transparent 12px);
		opacity: .25;
		pointer-events: none
	}

	.hero-inner {
		position: relative
	}

	.hero-top {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 16px
	}

	.app-title {
		font-size: 20px;
		font-weight: 600
	}

	.ops-row {
		display: flex;
		align-items: center;
		height: 100rpx;
		margin-bottom: 20rpx;
	}

	.ops-row .close {
		width: 60rpx;
		height: 60rpx;
		margin-left: auto;
	}

	.ops-left {
		display: flex;
		align-items: center;
	}

	.hero-actions {
		display: flex;
		align-items: center;
		gap: 12px
	}

	.add-device {
		width: 128rpx;

		font-family: PingFang SC, PingFang SC;
		font-weight: 600;
		font-size: 32rpx;
		color: #FF9759;
		font-style: normal;
		text-transform: none;
		margin-left: 8rpx;
	}

	.add-active-icon {
		width: 40rpx;
		height: 40rpx;
		margin-top: 6rpx;
	}

	.power-btn {
		width: 28px;
		height: 28px;
		border-radius: 14px;
		background: #1a1a1a;
		border: 1px solid #333;
		display: flex;
		align-items: center;
		justify-content: center
	}


	.chip-scroll {
		white-space: nowrap
	}

	.chip {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		padding: 8rpx 20rpx;
		margin-right: 16rpx;

		width: 128rpx;
		height: 64rpx;
		background: #38393B;
		border-radius: 6px 6px 6px 6px;

		border-radius: 12rpx;



		font-family: PingFang SC, PingFang SC;
		font-weight: 600;
		font-size: 32rpx;
		color: #FFFFFF;
		line-height: 48rpx;
		text-align: center;
		font-style: normal;
		text-transform: none;
	}

	.chip.active {
		background: #2a2a2a;
		border-color: #444
	}

	.chip.add {
		color: #ff6a2a
	}

	.light-row {
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-top: 40rpx
	}

	.light-icon {
		width: 40rpx;
		height: 42rpx;
	}

	.light-plus {
		font-size: 48rpx;
		color: #fff;
		font-weight: 800;
	}

	.mode-grid {
		display: grid;
		grid-template-columns: repeat(2, 1fr);
		gap: 14px;
		margin-top: 10px
	}

	.mode-card {
		background: #171717;
		border-radius: 14px;
		padding: 24rpx 32rpx;
	}

	.mode-card:active {
		transform: scale(.98)
	}

	.mode-head {
		display: flex;
		align-items: center
	}

	.mode-icon {
		width: 60rpx;
		height: 60rpx;
	}

	.mode-name {
		font-family: PingFang SC, PingFang SC;
		font-size: 28rpx;
		font-weight: 600;
		flex: 1
	}

	.mode-arrow {
		width: 36rpx;
		height: 36rpx;
		transform: rotateY(180deg);
		opacity: 0.5;
	}

	.mode-color {
		height: 66rpx;
		border-radius: 8rpx;
		margin-top: 26rpx
	}
</style>