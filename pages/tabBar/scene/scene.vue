<template>
	<view class="scene-page">
		
		<!-- 顶部切换 速度/加速度 + LED 标签 + 电源 -->
		<view class="top-bar">
			<view class="switches">
				<view class="switch-item" :class="{active: currentMode === 'speed'}" @click="switchMode('speed')">
					<image class="switch-icon" src="@/static/icons/sense/speed.png" mode="aspectFit" />
				</view>
				<view class="separator"></view>
				<view class="switch-item" :class="{active: currentMode === 'acceleration'}" @click="switchMode('acceleration')">
					<image class="switch-icon" src="@/static/icons/sense/phone.png" mode="aspectFit" />
				</view>
			</view>
			<text class="title">{{ currentMode === 'speed' ? '速度' : '加速度' }}</text>
      <image class="close" src="@/static/icons/home/close2x.png" alt="" srcset="" mode="aspectFill" />
		</view>
		<scroll-view class="chips" scroll-x>
			<view class="chip" v-for="(c,i) in chips" :key="i" :class="{active: curChip===i}" @click="curChip=i">{{ c }}
			</view>
		</scroll-view>
    <view class="light-row">
    <image class="light-icon" src="@/static/icons/home/light-bulb-icon.png" alt="" srcset="" mode="aspectFill" />
      <view class="seg">
        <view :class="['seg-btn',{on: seg===0}]" @click="seg=0">单色</view>
        <view :class="['seg-btn',{on: seg===1}]" @click="seg=1">模式</view>
      </view>
    </view>


		<view class="canvas" @click="onColorPick" @touchstart="onTouchStart" @touchmove="onTouchMove" @touchend="onTouchEnd">
			<view class="color-indicator" :style="{left: selectedPosition.x + 'px', top: selectedPosition.y + 'px'}" v-if="selectedPosition.x > 0"></view>
		</view>

		<view class="speed-panel">
			<text class="now">{{ currentMode === 'speed' ? '当前速度' : '当前加速度' }}</text>
			<text class="val">{{ currentMode === 'speed' ? '0 mph' : '0 G' }}</text>
			<image class="expand-btn" src="@/static/icons/sense/double.svg" mode="aspectFit" @click="goToDetail" />
		</view>
		<CustomTabBar />
	</view>
</template>

<script>
	import CustomNavBar from "@/components/custom-nav-bar.vue"
	import Idx from "@/components/index.vue"
  import CustomTabBar   from "../../../custom-tab-bar/index.vue";
	export default {
		name: 'ScenePage',
		components: {
      CustomTabBar,
			"i-d-x": Idx,
      'custom-tab-bar': () => import('@/custom-tab-bar/index.vue')
		},
		data() {
			return {
				chips: ['LED 1', 'LED 2', 'LED 3', 'LED 4', 'LED 5'],
				curChip: 0,
				seg: 0,
				currentMode: 'speed', // 'speed' 或 'acceleration'
				selectedColor: '#ff0000',
				selectedPosition: { x: 0, y: 0 }, // 初始不显示圆圈
				isDragging: false
			}
		},
		methods: {
			selectScene(index) {},
			switchMode(mode) {
				this.currentMode = mode;
				uni.showToast({
					title: mode === 'speed' ? '切换到速度模式' : '切换到加速度模式',
					icon: 'none'
				});
			},
			goToDetail() {
				if (this.currentMode === 'speed') {
					uni.navigateTo({
						url: '/pages/scene/speed'
					});
				} else {
					uni.navigateTo({
						url: '/pages/scene/acceleration'
					});
				}
			},
			onColorPick(e) {
				this.updateColorPosition(e);
			},
			onTouchStart(e) {
				this.isDragging = true;
				this.updateColorPosition(e);
			},
			onTouchMove(e) {
				if (this.isDragging) {
					this.updateColorPosition(e);
				}
			},
			onTouchEnd(e) {
				this.isDragging = false;
			},
			updateColorPosition(e) {
				const canvas = e.currentTarget;
				const rect = canvas.getBoundingClientRect();
				const x = e.touches ? e.touches[0].clientX - rect.left : e.clientX - rect.left;
				const y = e.touches ? e.touches[0].clientY - rect.top : e.clientY - rect.top;
				
				// 限制在调色盘范围内
				const clampedX = Math.max(0, Math.min(x, rect.width));
				const clampedY = Math.max(0, Math.min(y, rect.height));
				
				this.selectedPosition = { x: clampedX, y: clampedY };
				
				// 根据蓝湖设计稿的实际颜色计算
				// 水平方向：从左到右的颜色变化
				const horizontalColors = [
					{ r: 43, g: 0, b: 255 },    // #2B00FF
					{ r: 0, g: 170, b: 255 },   // #00AAFF
					{ r: 0, g: 255, b: 128 },   // #00FF80
					{ r: 255, g: 214, b: 0 },   // #FFD600
					{ r: 255, g: 149, b: 0 },   // #FF9500
					{ r: 255, g: 0, b: 0 }      // #FF0000
				];
				
				// 计算水平位置对应的颜色
				const horizontalRatio = clampedX / rect.width;
				const colorIndex = horizontalRatio * (horizontalColors.length - 1);
				const colorIndexFloor = Math.floor(colorIndex);
				const colorIndexCeil = Math.min(colorIndexFloor + 1, horizontalColors.length - 1);
				const colorRatio = colorIndex - colorIndexFloor;
				
				const color1 = horizontalColors[colorIndexFloor];
				const color2 = horizontalColors[colorIndexCeil];
				
				// 插值计算水平颜色
				const baseR = Math.round(color1.r + (color2.r - color1.r) * colorRatio);
				const baseG = Math.round(color1.g + (color2.g - color1.g) * colorRatio);
				const baseB = Math.round(color1.b + (color2.b - color1.b) * colorRatio);
				
				// 垂直方向：从下到上的透明度变化
				const verticalRatio = clampedY / rect.height;
				const alpha = 1 - verticalRatio; // 底部完全不透明，顶部完全透明
				
				// 计算最终颜色
				const finalR = Math.round(baseR * alpha + 245 * (1 - alpha));
				const finalG = Math.round(baseG * alpha + 245 * (1 - alpha));
				const finalB = Math.round(baseB * alpha + 245 * (1 - alpha));
				
				this.selectedColor = `rgb(${finalR}, ${finalG}, ${finalB})`;
				
				// 显示选中的颜色
				uni.showToast({
					title: `选中颜色: ${this.selectedColor}`,
					icon: 'none',
					duration: 1000
				});
			},
			goMusic() {
				uni.navigateTo({
					url: '/pages/scene/music/music'
				})
			}
		},
		onLoad() {
			console.log('场景页面加载')
		}
	}
</script>

<style scoped>
	.scene-page {
		background: #000;
		min-height: 100vh;
		color: #fff
	}

	.top-bar {
		display: flex;
		align-items: center;
		justify-content: space-between;
    margin-top: 48rpx;
		padding: 14px 12px;
		backdrop-filter: saturate(160%) blur(8px)
	}

	.switches {
		display: flex;
		align-items: center;
		gap: 16rpx
	}

	.switch-item {
		width: 48rpx;
		height: 48rpx;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 8rpx;
		transition: all 0.3s ease;
	}

	.switch-item.active {
		background: rgba(255, 255, 255, 0.1);
		border: 1px solid rgba(255, 255, 255, 0.3);
	}

	.switch-icon {
		width: 32rpx;
		height: 32rpx;
		opacity: 0.7;
		transition: opacity 0.3s ease;
	}

	.switch-item.active .switch-icon {
		opacity: 1;
	}

	.separator {
		width: 1rpx;
		height: 36rpx;
		background: rgba(255, 255, 255, 0.3);
		margin: 0 8rpx;
	}

  .close {
    width: 60rpx;
    height: 60rpx;
    margin-right: 16rpx;
  }

	.title {
		font-size: 18px;
		font-weight: 700
	}

	.power {
		font-size: 18px
	}

	.chips {
		white-space: nowrap;

		padding: 6px 10px;
	}

	.chip {
		display: inline-flex;
		align-items: center;
    width: 128rpx;
    height: 64rpx;
		justify-content: center;
		padding: 8px 14px;
		margin-right: 10px;
		background: #1a1a1a;
		border: 1px solid #333;
		border-radius: 10px
	}

	.chip.active {
		background: #2a2a2a
	}

	.seg {
		display: flex;
		background: #1a1a1a;
		border: 1px solid #333;
		border-radius: 12px;
		height: 68rpx;
		overflow: hidden;
		gap: 0;
	}

	.seg-btn {
		width: 263rpx;
		height: 68rpx;
		text-align: center;
		line-height: 68rpx;
		color: #cfcfcf;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.seg-btn.on {
		background: #ff5a24;
		color: #fff
	}

   .light-row {
     display: flex;
     align-items: center;
     justify-content: space-between;
     margin-top: 32rpx;
     margin-bottom: 36rpx;
     padding: 0 30rpx;
   }
   .light-icon {
     width: 40rpx;
     height: 42rpx;
   }
	.canvas {
		width: 100%;
		height: 260px;
    /* 背景渐变 */
    background:
        linear-gradient(to right, rgba(43, 0, 255, 1), rgba(0, 170, 255, 1), rgba(0, 255, 128, 1), rgba(255, 214, 0, 1), rgba(255, 149, 0, 1), rgba(255, 0, 0, 1)),
        linear-gradient(to bottom, rgba(255, 255, 255, 0), white);
    background-blend-mode: screen;border-radius: 0px;
		position: relative;
		cursor: pointer;
	}

	.color-indicator {
		position: absolute;
		width: 20px;
		height: 20px;
		border: 3px solid #ffffff;
		border-radius: 50%;
		transform: translate(-50%, -50%);
		box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
		pointer-events: none;
		z-index: 10;
	}

	.speed-panel {
		position: fixed;
		left: 32rpx;
		right: 32rpx;
		bottom: calc(144rpx + 24rpx + env(safe-area-inset-bottom));
    background: linear-gradient( 179deg, rgba(18,22,36,0) 0%, #121624 100%);;
		border: 1px solid #1f1f1f;
		border-radius: 100rpx;
		height: 104rpx;
		padding: 0 16px;
		display: flex;
		align-items: center;
		gap: 14px;
		z-index: 10;
	}

	.now {
		color: #cfcfcf
	}

	.val {
		flex: 1;
		text-align: center;
		margin: 0 8px;
	}

	.expand-btn {
		width: 60rpx;
		height: 60rpx;
		margin-right: 32rpx;
		opacity: 0.8;
	}
</style>