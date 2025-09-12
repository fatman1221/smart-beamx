<template>
	<view class="setting-page">

    <view class="page-nav">
      <image class="nav-back" @click="goBack" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill" />

      <text class="page-title">模式设置</text>
      <view class="nav-actions">
        <image class="nav-share" src="@/static/icons/model/share.svg" mode="aspectFill" />
        <text class="nav-save" @click="save">保存</text>
      </view>

    </view>

		<view class="canvas"></view>

		<text class="label">闪烁模式</text>
		<view class="pattern-grid">
			<view class="pbtn" v-for="i in 8" :key="i">
				<image class="star" src="@/static/icons/model/star.png" alt="" srcset="" />
			</view>
		</view>

		<text class="label">亮度</text>
		<view class="slider-row">
			<image class="sicon" src="@/static/icons/model/light-left.svg" mode="aspectFit" />
			<slider class="custom-slider" :value="brightness" @change="e=>brightness=e.detail.value" min="0" max="100" 
				active-color="rgba(255, 255, 255, 1)" backgroundColor="#111" 
				block-color="#ffffff" block-size="24" />
			<image class="sicon" src="@/static/icons/model/light-right.svg" mode="aspectFit" />
		</view>

		<text class="label">频率</text>
		<view class="slider-row">
			<image class="sicon" src="@/static/icons/model/once-left.svg" mode="aspectFit" />
			<slider class="custom-slider" :value="speed" @change="e=>speed=e.detail.value" min="0" max="100" 
				active-color="rgba(255, 255, 255, 1)" backgroundColor="#111" 
				block-color="#ffffff" block-size="24" />
			<image class="sicon" src="@/static/icons/model/once-right.svg" mode="aspectFit" />
		</view>

		<view class="palette">
			<view class="colors-group">
				<view v-for="(c,i) in colors" :key="i" class="dot" :style="{background:c}" @click="pick(c)"></view>
			</view>
			<view class="ops">
				<button class="op del">
					<image src="@/static/icons/model/delete.svg" mode="aspectFit" />
				</button>
				<button class="op add">
					<image src="@/static/icons/model/add.svg" mode="aspectFit" />
				</button>
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

    width: 100% ;
    height: 520rpx;
    background:
        linear-gradient(to right, rgba(43, 0, 255, 1), rgba(0, 170, 255, 1), rgba(0, 255, 128, 1), rgba(255, 214, 0, 1), rgba(255, 149, 0, 1), rgba(255, 0, 0, 1)),
        linear-gradient(to bottom, rgba(255, 255, 255, 0), white);
    background-blend-mode: screen;
  }

	.label {
		display: block;
    margin-left: 32rpx;
    margin-top: 62rpx;
    margin-bottom: 24rpx;


		color: #cfcfcf
	}

	.pattern-grid {
		display: grid;
		grid-template-columns: repeat(4, 159.5rpx);
		gap: 16rpx;
		padding: 0 32rpx;
		justify-content: start;
	}

	.pbtn {
		background: #1a1a1a;
		border-radius: 12rpx;
		height: 80rpx;
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
		gap: 24rpx;
		padding: 0 32rpx;
		margin-bottom: 20rpx;
		height: 48rpx;
	}
	
	/* 确保滑动条与图标在同一水平线 */
	.custom-slider {
		width: 526rpx;
		height: 48rpx;
	}

	.sicon {
		opacity: .7;
		width: 48rpx;
		height: 48rpx;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.custom-slider {
		width: 526rpx;
		height: 48rpx;
	}
	
	/* 滑块轨道样式 */
	.custom-slider ::v-deep .uni-slider-track {
		height: 48rpx !important;
		border-radius: 999rpx !important;
	}
	
	/* 进度部分样式 */
	.custom-slider ::v-deep .uni-slider-track-active {
		border-radius: 999rpx !important;
		background-color: #ffffff !important;
	}
	
	/* 未滑过部分的背景色 */
	.custom-slider ::v-deep .uni-slider-track-background {
    position: fixed;

		background-color: rgba(26, 26, 26, 1) !important;
	}
	
	.custom-slider ::v-deep .uni-slider-handle {
		display: none !important;
		visibility: hidden !important;
		opacity: 0 !important;
		width: 0 !important;
		height: 0 !important;
	}
	
	/* 尝试其他可能的选择器 */
	.custom-slider ::v-deep .uni-slider-thumb {
		display: none !important;
		visibility: hidden !important;
		opacity: 0 !important;
		width: 0 !important;
		height: 0 !important;
	}
	
	.custom-slider ::v-deep .uni-slider-button {
		display: none !important;
		visibility: hidden !important;
		opacity: 0 !important;
		width: 0 !important;
		height: 0 !important;
	}
	
	/* 确保滑块可以正常交互 */
	.custom-slider ::v-deep .uni-slider {
		height: 48rpx !important;
	}
	
	/* 确保滑动条轨道与图标对齐 */
	.custom-slider ::v-deep .uni-slider-track {
		height: 48rpx !important;
		border-radius: 999rpx !important;
	}

	.palette {
		position: fixed;
		left: 0;
		right: 0;
		bottom: 0;
    height: 128rpx;
		background: #111;
		border-top: 1px solid #2a2a2a;
    border-radius: 24rpx;
		display: flex;
		align-items: center;
		padding-left: 32rpx;
		padding-right: 32rpx;
		justify-content: space-between
	}

	.colors-group {
		display: flex;
		gap: 16rpx;
	}

	.dot {
		width: 80rpx;
		height: 80rpx;
		border-radius: 12rpx
	}

	.ops {
		display: flex;
		gap: 24rpx
	}

	.op {
		width: 80rpx;
		height: 80rpx;
		border-radius: 12rpx;
		background: rgba(255, 255, 255, 0.20);
		border: 1px solid #444;
		display: flex;
		align-items: center;
		justify-content: center;
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

	.op image {
		width: 48rpx;
		height: 48rpx;
	}

  .page-nav {
    position: sticky;
    top: 44rpx;
    text-align: center;
    padding: 16rpx 0;
    margin-bottom: 44rpx;
    z-index: 2;
  }

  .page-title {
    font-size: 36rpx;
    color: #ffffff;
  }

  .nav-back {
    position: absolute;
    width: 40rpx;
    height: 40rpx;
    display: flex;
    margin-top: 8rpx;
    margin-left: 24rpx;
  }

  .nav-actions {
    position: absolute;
    right: 24rpx;
    top: 50%;
    transform: translateY(-50%);
    display: flex;
    align-items: center;
    gap: 52rpx;
  }

  .nav-share {
    width: 24rpx;
    height: 24rpx;
  }

  .nav-save {
    color: #ffffff;
    font-size: 24rpx;
    padding: 8rpx 0;
    font-family: "PingFang SC", PingFang SC;
  }

</style>