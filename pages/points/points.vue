<template>
	<view class="points-page">
		<view class="hero">
			<view class="score-card">
				<view class="left">
					<text class="score">{{ points }}</text>
					<text class="score-unit">积分</text>
				</view>
				<view class="right column">
					<button class="link" @click="goRules">积分奖励规则 ></button>
					<button class="plain" @click="goDetail">积分明细</button>
				</view>
			</view>
			<view class="checkin">
				<view class="days">
					<view class="day" v-for="d in 7" :class="{done: d<=checkedDays}">
						<text style="font-size: 24rpx;">{{d}}天</text>
						<image src="@/static/icons/my/points-icon.png" class="point-icon" alt="" srcset="" mode="aspectFill" :key="d" />
					</view>
				</view>
				<button class="checkin-btn" :disabled="checkedToday"
					@click="doCheckin">{{ checkedToday ? '已打卡' : '今日打卡' }}</button>
			</view>
		</view>

		<view class="task-card">
			<text class="section-title">做任务得积分</text>
			<view class="task-row" v-for="t in tasks" :key="t.id">
				<text class="task-name">{{ t.name }}</text>
				<image src="@/static/icons/my/points-icon.png" class="point-img" mode="aspectFill" alt="" srcset="" :key="d" />
				<text class="task-add">+{{ t.add }}</text>
				<view class="task-btn" @click="takeTask(t)" :class="{claim:t.action==='做任务'}">
					{{ t.taken ? '已领取' : (t.action || '领积分') }}
				</view>
			</view>
		</view>

		<view class="tabs">
			<view class="tab" v-for="(c,i) in tabs" :key="i" :class="{active: curTab===i}" @click="curTab=i">{{ c }}
			</view>
		</view>

		<scroll-view scroll-y class="goods-grid">
			<view class="card" v-for="g in goods" :key="g.id">
				<image class="cover" :src="g.img" mode="aspectFill" />
				<view class="info">
					<text class="title">{{ g.title }}</text>
					<view class="price-row">
						<text class="price">$ {{ g.price }}</text>
						<text class="cart">🛒</text>
					</view>
					<text class="asin">ASIN: {{ g.asin }}</text>
				</view>
			</view>
		</scroll-view>

		<!-- 		<view class="search-bar-fixed">
			<view class="search" @click="goSearch">🔍 请输入关键字</view>
		</view> -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				points: 2488,
				checkedDays: 1,
				checkedToday: false,
				tabs: ['精选', '优惠', '好物'],
				curTab: 0,
				tasks: [{
						id: 1,
						name: '新增模式',
						add: 100,
						taken: false
					},
					{
						id: 2,
						name: '设置灯光',
						add: 100,
						taken: false
					},
					{
						id: 3,
						name: '购买商品',
						add: 1000,
						taken: false,
						action: '做任务'
					}
				],
				goods: []
			}
		},
		onLoad() {
			this.goods = this.mockGoods()
		},
		methods: {
			goRules() {
				uni.navigateTo({
					url: '/pages/points/rulesText'
				})
			},
			goDetail() {
				uni.navigateTo({
					url: '/pages/points/rules'
				})
			},
			doCheckin() {
				this.checkedToday = true;
				this.checkedDays = Math.min(7, this.checkedDays + 1);
				this.points += 20
			},
			takeTask(t) {
				if (t.taken) return;
				t.taken = true;
				this.points += t.add;
				uni.showToast({
					title: '已领取 +' + t.add,
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
					asin: 'BOCXNW7X2'
				}))
			}
		}
	}
</script>

<style scoped>
	.points-page {
		background: #000;
		min-height: 100vh;
		color: #fff
	}

	.hero {
		padding: 16px
	}

	.score-card {
		display: flex;
		justify-content: space-between;
		align-items: center;
		background: #191919;

		border-radius: 24rpx;
		padding: 32rpx 24rpx
	}

	.left {
		display: flex;
		align-items: center;
	}

	.score {
		font-family: PingFang SC, PingFang SC;
		font-weight: 600;
		font-size: 64rpx;
		color: #FFFFFF;
		text-align: left;
		font-style: normal;
		text-transform: none;
	}

	.score-unit {
		margin-top: 20rpx;
		margin-left: 6px;
		opacity: .4;
		width: 48rpx;
		height: 40rpx;
		font-family: PingFang SC, PingFang SC;
		font-weight: 400;
		font-size: 24rpx;
		color: #FFFFFF;
		line-height: 40rpx;
		text-align: left;
		font-style: normal;
		text-transform: none;
	}

	.right.column {
		display: flex;
		flex-direction: column;
		gap: 8px
	}

	.plain {
		width: 160rpx;
		height: 60rpx;
		line-height: 60rpx;
		border-radius: 12rpx;
		border: 2rpx solid rgba(255, 255, 255, 0.46);
		background: #191919;
		font-family: PingFang SC, PingFang SC;
		font-weight: 400;
		font-size: 24rpx;
		color: #FFFFFF;
		text-align: center;
		font-style: normal;
		text-transform: none;
	}

	.link {

		height: 40rpx;
		font-family: PingFang SC, PingFang SC;
		font-weight: 400;
		font-size: 24rpx;
		color: rgba(255, 255, 255, 0.4);
		line-height: 40rpx;
		text-align: left;
		font-style: normal;
		text-transform: none;
		background: #191919;

	}

	.checkin {
		margin-top: 12px;
		background: #191919;
		border-radius: 14px;
		padding: 14px
	}

	.days {
		display: flex;
		justify-content: space-between;
		margin-bottom: 24rpx
	}

	.day {
		width: 48rpx;
		opacity: .3
	}

	.point-icon {
		width: 48rpx;
		height: 48rpx;
		margin-top: 8rpx;
	}

	.done {
		opacity: 1;
	}

	.checkin-btn {
		width: 100%;
		height: 72rpx;
		font-family: PingFang SC, PingFang SC;
		font-weight: 400;
		font-size: 24rpx;
		color: #FFFFFF;
		line-height: 72rpx;
		text-align: center;
		font-style: normal;
		text-transform: none;
		background: #3F3F3F;
	}

	.task-card {
		margin: 8px 16px;
		background: #191919;
		border-radius: 14px;
		padding: 16px
	}

	.section-title {
		height: 44rpx;
		font-family: PingFang SC, PingFang SC;
		font-weight: 600;
		font-size: 28rpx;
		color: #FFFFFF;
		line-height: 44rpx;
		text-align: left;
		font-style: normal;
		text-transform: none;
		margin-bottom: 24rpx
	}

	.task-row {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-top: 24rpx;
	}

	.task-row:first-of-type {
		border-top: none
	}

	.task-name {
		font-family: PingFang SC, PingFang SC;
		font-weight: 400;
		font-size: 24rpx;
		color: #FFFFFF;
		text-align: left;
		font-style: normal;
		text-transform: none;
		opacity: 0.4;
	}

	.claim {
		background: none !important;
		border: 1rpx solid #fff;
	}

	.point-img {
		width: 36rpx;
		height: 36rpx;
		margin-left: 24rpx;
	}

	.task-right {
		display: flex;
		align-items: center;
		gap: 10px
	}

	.task-add {
		opacity: .9;
		margin-left: 4rpx;
	}

	.task-btn {
		color: #fff;
		width: 148rpx;
		height: 64rpx;
		line-height: 64rpx;
		background: #414141;
		border-radius: 78rpx;
		font-family: PingFang SC, PingFang SC;
		font-weight: 400;
		font-size: 28rpx;
		color: #FFFFFF;
		text-align: center;
		font-style: normal;
		text-transform: none;
		margin-left: auto;
	}

	.tabs {
		display: flex;
		gap: 10px;
		padding: 12px 16px
	}

	.tab {
		background: #1E1F21;
		border-radius: 12rpx;
		color: #cfcfcf;
		padding: 8rpx 40rpx;

		font-family: PingFang SC, PingFang SC;
		font-weight: 400;
		font-size: 32rpx;
		color: #FFFFFF;

		text-align: center;
		font-style: normal;
		text-transform: none;
	}

	.tab.active {
		background: #38393B;

		font-weight: 600;
	}

	.goods-grid {
		padding: 0 12px 20px
	}

	.card {
		background: #121212;
		border: 1px solid #2f2f2f;
		border-radius: 18px;
		overflow: hidden;
		margin: 0 4px 12px 4px;
		width: calc(50% - 8px);
		display: inline-block;
		vertical-align: top
	}

	.cover {
		width: 100%;
		height: 180px
	}

	.info {
		padding: 12px
	}

	.title {
		display: block;
		line-height: 1.4
	}

	.price-row {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin: 6px 0
	}

	.price {
		color: #ff4d4f;
		font-weight: 800
	}

	.asin {
		opacity: .7
	}

	.search-bar-fixed {
		position: fixed;
		left: 0;
		right: 0;
		top: 10px;
		display: flex;
		justify-content: center;
		pointer-events: none
	}

	.search {
		pointer-events: auto;
		width: 84%;
		background: #2a2a2a;
		border: 1px solid #444;
		border-radius: 24px;
		color: #cfcfcf;
		padding: 10px 14px
	}
</style>