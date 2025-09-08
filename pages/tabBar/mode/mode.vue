<template>
	<view class="mode-page">
		<view class="top-card">
			<image class="mode-icon" src="@/static/icons/home/mode-1-icon2x.png" alt="" srcset=""  mode="aspectFill"/>
			<view class="mode-head">
				<text class="mode-title">模式名称1</text>
				<image class="mode-arrow" src="@/static/icons/my/back2x.png" alt="" srcset=""  mode="aspectFill"/>
			</view>
			<view class="mode-color" style="background:linear-gradient(90deg,#ff6aa6,#60d3ff)"></view>
		</view>
		<button class="add-btn" @click="goCreate"> <image src="@/static/icons/model/add-icon.png" class="add-active-icon" mode="aspectFill"
				alt="" srcset="" /> 添加</button>

		<text class="subtitle">预设</text>
		<view class="grid">
			<view class="mode-card" v-for="m in presets" :key="m.id" @click="open(m)">
				<image class="mode-icon" :src="m.icon" alt="" srcset=""  mode="aspectFill"/>
				<view class="mode-head">
					<text class="mode-title">{{ m.name }}</text>
					<image class="mode-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill"  />
				</view>
				<view class="mode-color" :style="{background:m.bg}"></view>
			</view>
		</view>
	</view>
</template>

<script>
	import mode1 from "@/static/icons/home/mode-1-icon2x.png"
	import mode2 from "@/static/icons/home/mode-2-icon2x.png"
	import mode3 from "@/static/icons/home/mode-3-icon2x.png"
	import mode4 from "@/static/icons/home/mode-4-icon2x.png"
	export default {
		name: 'ModePage',
		data() {
			return {
				presets: [{
						id: 1,
						name: '模式名称1',
						bg: 'linear-gradient(90deg,#ff6aa6,#60d3ff)',
						icon: mode1
					},
					{
						id: 2,
						name: '模式名称1',
						bg: 'linear-gradient(90deg,#ff9a3c,#f0de62)',
						icon: mode2
					},
					{
						id: 3,
						name: '模式名称1',
						bg: 'linear-gradient(90deg,#40e0a1,#36a3a3)',
						icon: mode3
					},
					{
						id: 4,
						name: '模式名称1',
						bg: 'linear-gradient(90deg,#7c5cff,#ff3b6b)',
						icon: mode4
					}
				]
			}
		},
		methods: {
			goCreate() {
				uni.navigateTo({
					url: '/pages/mode/setting'
				})
			},
			open(m) {
				uni.navigateTo({
					url: '/pages/mode/setting'
				})
			}
		}
	}
</script>

<style scoped>
	.mode-page {
		background: #000;
		min-height: 100vh;
		color: #fff;
		padding: 16px
	}

	.top-card {
		background: #171717;
	
		border-radius: 16px;
		padding: 16px;
		margin-bottom: 14px
	}

	.mode-head {
		display: flex;
		align-items: center
	}

	.mode-icon {
		width: 60rpx;
		height: 60rpx;
		opacity: .8
	}

	.mode-title {
		font-size: 16px;
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
		height: 76rpx;
		border-radius: 8rpx;
		margin-top: 26rpx
	}

	.add-btn {
    margin-left: 24rpx;
    margin-right: 24rpx;
		color: #fff;
		border: none;
		height: 80rpx;
		line-height: 80rpx;
		background: #F04D1A;
		border-radius: 999rpx;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.subtitle {
		display: block;
		color: #bdbdbd;
		margin: 44rpx 0;
	}

	.grid {
		display: grid;
		grid-template-columns: repeat(2, 1fr);
		gap: 12px
	}

	.mode-card {
		background: #171717;

		border-radius: 16px;
		padding: 14px
	}

	.mode-card:active {
		transform: scale(.98)
	}

	.add-active-icon {
		width: 48rpx;
		height: 48rpx;
		color: #fff;
		margin-right: 8rpx;

	}
</style>