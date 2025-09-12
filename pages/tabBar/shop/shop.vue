<template>
	<view class="shop-page">
<!--		<custom-tab-bar />-->
		<!-- 顶部横幅 + 城市 + 搜索条 -->
		<view class="banner">
			<image class="banner-img" :src="bannerUrl" mode="aspectFill" />
			<view class="top-bar">
				<view class="loc">
					<image class="loc-icon" src="@/static/icons/shop/location.png" mode="aspectFit" />
					<text class="loc-text">{{ city }}</text>
				</view>

				<view class="search" @click="goSearch">
					<!-- <input type="text" placeholder="请输入关键字" /> -->
					<image class="search-icon" src="@/static/icons/shop/search2x.png" alt="" srcset="" /> 请输入关键词
				</view>
			</view>
		</view>
    <!-- 广告图片 -->
    <view class="ad-banner">
      <image class="ad-image" src="https://images.unsplash.com/photo-1545665277-5937489579f2?q=80&w=1600" mode="aspectFill" />
    </view>

		<!-- 分类chips -->
		<scroll-view class="chip-row" scroll-x>
			<view v-for="(c,i) in cats" :key="i" class="chip" :class="{active: curCat===i}" @click="curCat=i">{{ c }}
			</view>
		</scroll-view>



		<!-- 商品栅格 两列 -->
		<scroll-view scroll-y class="goods-area">
			<view class="card-item" v-for="g in goods" :key="g.id" @click="viewProduct(g)">
				<image class="cover" :src="g.img" mode="aspectFill" />
				<view class="info">
					<text class="title">{{ g.title }}</text>
					<view class="price-row">
						<text class="price">$ {{ g.price }}</text>
						<image src="@/static/icons/shop/shopping-cart.png" class="shopping-cart" alt="" srcset="" />

					</view>
					<text class="asin">ASIN: {{ g.asin }}</text>
				</view>
			</view>
		</scroll-view>
		<CustomTabBar />
	</view>
</template>

<script>

import CustomTabBar   from "../../../custom-tab-bar/index.vue";

	export default {
		name: 'ShopPage',
		components: { CustomTabBar},
		data() {
			return {
				city: '深圳市',
				bannerUrl: 'https://images.unsplash.com/photo-1612010167108-3e6bff0e3c70?q=80&w=1600',
				cats: ['小车', '卡车', '吉普', '摩托车', '越野', '其他'],
				curCat: 0,
				goods: []
			}
		},
		methods: {
			viewProduct(product) {
				uni.showToast({
					title: `查看${product.name}`,
					icon: 'none'
				})
			},
			goSearch() {
				uni.navigateTo({
					url: '/pages/points/search'
				})
			},
			mockGoods() {
				const imgs = [
					'https://images.unsplash.com/photo-1545665277-5937489579f2?q=80&w=800',
					'https://images.unsplash.com/photo-1612010167108-3e6bff0e3c70?q=80&w=800',
					'https://images.unsplash.com/photo-1584624274612-9b3e2e5c12e2?q=80&w=800',
					'https://images.unsplash.com/photo-1592194996308-7b43878e84a6?q=80&w=800'
				]
				return imgs.map((img, i) => ({
					id: i + 1,
					img,
					title: 'LED 轮环灯RGB 带 APP 和遥控霓虹灯 带转向信号和制动功',
					price: '68.00',
					asin: 'BOCXNW7X2',
					name: 'LED 灯'
				}))
			}
		},
		onLoad() {
			this.goods = this.mockGoods()
		}
	}
</script>

<style scoped>
	.shop-page {
		background: #000;
		background-image: url('/static/icons/background.svg');
		background-size: cover;
		background-position: center;
		background-repeat: no-repeat;
		min-height: 100vh;
		color: #fff;
		position: relative;
	}

	.shop-page::before {
		content: '';
		position: absolute;
		inset: 0;
		background: url('/static/icons/background.svg') center/cover no-repeat;
		opacity: 0.4;
		pointer-events: none;
		z-index: 0;
	}

	.banner {
		position: relative;
		height: 120rpx;
		top: 66rpx;
		z-index: 1;
		margin-bottom: 20rpx;
	}

	.banner-img {
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%
	}

	.shopping-cart {
		width: 48rpx;
		height: 48rpx;
	}

	.top-bar {
		position: absolute;
		left: 12px;
		right: 12px;
		top: 12px;
		display: flex;
		align-items: center;
		gap: 10px
	}

	.loc {
		background: rgba(0, 0, 0, .5);
		border: none !important;
		outline: none;
		border-radius: 16px;
		padding: 6px 10px;
		display: flex;
		align-items: center;
		gap: 4px;
	}

	.loc-icon {
		width: 24rpx;
		height: 24rpx;
		display: block;
		border: none !important;
		outline: none;
		box-shadow: none;
		background: transparent;
		border-radius: 0;
	}

	.loc-text {
		color: #ffffff;
		font-size: 24rpx;
	}

	.search {
		flex: 1;
		color: #cfcfcf;
		height: 64rpx;
    width: 508rpx;
		line-height: 64rpx;
		background: #363636;
		border-radius: 999rpx;
		display: flex;
		align-items: center;
	}

	.search-icon {
		width: 30rpx;
		height: 30rpx;
		margin-left: 32rpx;
    margin-right: 8rpx;
	}

	.chip-row {
		white-space: nowrap;
		padding: 12px 12px 8px;
		position: relative;
		z-index: 1;
	}

	.chip {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		padding: 8px 16px;
		height: 64rpx;
		background: #38393B;
		border-radius: 12rpx;
		font-family: PingFang SC, PingFang SC;
		font-weight: 600;
		font-size: 32rpx;
		color: #FFFFFF;
		text-align: center;
		font-style: normal;
		text-transform: none;
		margin-right: 16rpx;
		border: none !important;
	}

	.chip.active {
		background: #3a3a3a;
		color: #fff
	}

	/* 广告图片样式 */
	.ad-banner {
		width: 100%;
		height: 352rpx;
		margin: 44rpx 0 24rpx 0;
		overflow: hidden;
		position: relative;
		z-index: 1;
		border-radius: 12rpx;
	}

	.ad-image {
		width: 100%;
		height: 100%;
		position: relative;
		z-index: 1;
	}

	.goods-area {
		padding: 6px 10px 90px;
		position: relative;
		z-index: 1;
	}

	.card-item {
		background: rgba(26, 26, 26, 1);
		border-radius: 18rpx;
		overflow: hidden;
		margin: 0 6px 12px 6px;
		width: calc(50% - 12px);
		display: inline-block;
		vertical-align: top
	}

	.cover {
		width: 100%;
		height: 180px
	}

	.info {
		padding: 10px
	}

	.title {
		display: block;
		line-height: 1.4;
    font-size: 24rpx;
    height: 80rpx;
    width: 324rpx;
	}

	.price-row {
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin: 6px 0
	}

	.price {
		color: #ff4d4f;
		font-weight: 800
	}

	.asin {
		opacity: .7;
    font-size:20rpx;
	}
</style>