<template>
	<view class="setting-page">
		<custom-nav-bar title="模式设置" :onBack="goBack" :showSave="true" @save="save" />
		<view class="canvas"></view>

		<text class="label">闪烁模式</text>
		<view class="pattern-grid">
			<view class="pbtn" v-for="i in 8" :key="i">
				<img class="star" src="@/static/icons/model/star.png" alt="" srcset="" />
			</view>
		</view>

		<text class="label">亮度</text>
		<view class="slider-row">
			<text class="sicon">☼</text>
			<slider :value="brightness" @change="e=>brightness=e.detail.value" min="0" max="100" active-color="#fff"
				backgroundColor="#333" />
			<text class="sicon">☀︎</text>
		</view>

		<text class="label">频率</text>
		<view class="slider-row">
			<text class="sicon">~</text>
			<slider :value="speed" @change="e=>speed=e.detail.value" min="0" max="100" active-color="#fff"
				backgroundColor="#333" />
			<text class="sicon">~</text>
		</view>

		<view class="palette">
			<view v-for="(c,i) in colors" :key="i" class="dot" :style="{background:c}" @click="pick(c)"></view>
			<view class="ops">
				<button class="op del">🗑</button>
				<button class="op add">＋</button>
			</view>
		</view>
	</view>
</template>

<script>
	import CustomNavBar from "@/components/custom-nav-bar.vue"
	
	export default {
		name: 'ModeSettingPage',
		components: {
			CustomNavBar
		},
		data() {
			return {
				brightness: 70,
				speed: 40,
				colors: ['#2d4bff', '#7a38b4', '#e22658']
			}
		},
		methods: {
			goBack() {
				uni.navigateBack()
			},
			pick(c) {
				uni.showToast({
					title: '选择颜色',
					icon: 'none'
				})
			},
			save() {
				uni.showLoading({
					title: '保存中...'
				})
				
				// 模拟保存过程
				setTimeout(() => {
					uni.hideLoading()
					uni.showToast({
						title: '保存成功',
						icon: 'success'
					})
					
					// 保存成功后返回上一页
					setTimeout(() => {
						uni.navigateBack()
					}, 1500)
				}, 1000)
			}
		}
	}
</script>

<style scoped>
	.setting-page {
		background: #000;
		min-height: 100vh;
		color: #fff
	}

	.canvas {
		height: 220px;
		background: linear-gradient(90deg, red, orange, yellow, green, cyan, blue, purple)
	}

	.label {
		display: block;
		margin: 12px 16px 6px;
		color: #cfcfcf
	}

	.pattern-grid {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 10px;
		padding: 0 16px
	}

	.pbtn {
		background: #1a1a1a;
		border-radius: 10px;
		height: 44px;
		display: flex;
		align-items: center;
		justify-content: center
	}

	.star {
		width: 48rpx;
		height: 48rpx;
	}

	.slider-row {
		display: flex;
		align-items: center;
		gap: 10px;
		padding: 0 16px
	}

	.sicon {
		opacity: .7
	}

	.palette {
		position: fixed;
		left: 0;
		right: 0;
		bottom: 0;
		background: #111;
		border-top: 1px solid #2a2a2a;
		padding: 12rpx 16rpx;
		display: flex;
		align-items: center;
		gap: 12px
	}

	.dot {
		width: 80rpx;
		height: 80rpx;
		border-radius: 12rpx
	}

	.ops {
		margin-left: auto;
		display: flex;
		gap: 10px
	}

	.op {
		width: 80rpx;
		height: 80rpx;
		border-radius: 12rpx;
		background: rgba(255, 255, 255, 0.20);
		border: 1px solid #444;
	}

	.op.del {
		width: 80rpx;
		height: 80rpx;
		background: rgba(255, 69, 92, 0.2);
		color: red;
		border: none;
	}

	.op.add {
		width: 80rpx;
		height: 80rpx;
		background: rgba(255, 255, 255, 0.2);
		font-weight: 800;
		border: none;
	}

</style>