<template>
	<view class="my-page">
		<!-- 顶部悬浮导航：返回 + 标题 + 设置（同一行） -->
		<view class="nav-float">
			<text class="nav-title">个人中心</text>
			<view class="settings-float" @click="goToSettings">
				<image class="menu-icon-svg" src="/static/icons/settings.svg" mode="widthFix"
					style="width:22pt;height:22pt"></image>
			</view>
		</view>


		<!-- 用户登录区域 -->
		<view class="user-section" :class="{'abs-profile': useAbsProfile}">
			<!-- 未登录状态 -->
			<view v-if="!isLoggedIn" class="login-area" @click="goToLogin">
				<image class="user-avatar" src="@/static/icons/my/avatar.png" mode="aspectFill"></image>
				<text class="login-text">点击登录/注册</text>
				<image class="login-arrow" src="@/static/icons/my/back2x.png" mode="aspectFill" alt="" srcset="" />
			</view>

			<!-- 已登录状态 -->
			<view v-else class="user-info-area flex-mode" @click="goToProfile">
				<image class="user-avatar" :src="userInfo.avatar" mode="aspectFill"></image>
				<view class="user-details">
					<text class="user-name">{{ userInfo.nickname }}</text>
				</view>

				<text class="profile-arrow">></text>
			</view>
		</view>

		<!-- 悬浮设置按钮（标题右侧） -->


		<!-- 菜单整体背景（暂不使用，避免与条目重叠） -->
		<view class="menu-card-bg"></view>

		<!-- 功能菜单卡片 -->
		<view class="menu-card" :class="{'abs-items': useAbsItems}">
			<view class="menu-item feedback-item" @click="goToFeedback">
				<view class="menu-icon-container feedback">
					<view class="menu-icon-slot">
						<image class="menu-icon-svg" src="/static/icons/feedback.svg" mode="widthFix"></image>
					</view>
				</view>
				<text class="menu-title">问题反馈</text>
				<image class="login-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" />
			</view>

			<view class="menu-item points-item" @click="goToPoints">
				<view class="menu-icon-container points">
					<view class="menu-icon-slot">
						<image class="menu-icon-svg" src="/static/icons/scoreShop.svg" mode="widthFix"></image>
					</view>
				</view>
				<text class="menu-title">积分商城</text>
				<image class="login-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" />
			</view>

			<view class="menu-item invite-item" @click="goToInvite">
				<view class="menu-icon-container invite">
					<view class="menu-icon-slot">
						<image class="menu-icon-svg" src="/static/icons/invite.svg" mode="widthFix"></image>
					</view>
				</view>
				<text class="menu-title">邀请好友</text>
				<image class="login-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" />
			</view>

			<view class="menu-item faq-item" @click="goToFAQ">
				<view class="menu-icon-container faq">
					<view class="menu-icon-slot">
						<image class="menu-icon-svg" src="/static/icons/question.svg" mode="widthFix"></image>
					</view>
				</view>
				<text class="menu-title">常见问题</text>
				<image class="login-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" />
			</view>

			<view class="menu-item about-item" @click="goToAbout">
				<view class="menu-icon-container about">
					<view class="menu-icon-slot">
						<image class="menu-icon-svg" src="/static/icons/about.svg" mode="widthFix"></image>
					</view>
				</view>
				<text class="menu-title">关于我们</text>
				<image class="login-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" />
			</view>

			<!-- 临时测试登录按钮 -->
<!--			<view class="menu-item" @click="testLogin">-->
<!--				<view class="menu-icon-container test">-->
<!--					<view class="menu-icon-slot">-->
<!--						<image class="menu-icon-svg" src="/static/icons/settings.svg" mode="widthFix"></image>-->
<!--					</view>-->
<!--				</view>-->
<!--				<text class="menu-title">{{ isLoggedIn ? '退出登录' : '测试登录' }}</text>-->
<!--				<image class="login-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" />-->
<!--			</view>-->
		</view>
	</view>
</template>

<script>
	export default {
		name: 'MyPage',
		data() {
			return {
				useAbsProfile: true,
				useAbsItems: false,
				/* 恢复流式布局 */
				isLoggedIn: false, // 登录状态，可以通过点击测试登录切换
				userInfo: {
					avatar: 'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?w=400&h=400&fit=crop&crop=face',
					nickname: '智能车灯用户',
					phone: '188****8888',
					email: 'user@smartbeamx.com',
					points: 1580,
					level: 'VIP会员'
				},
				appVersion: '1.0.0'
			}
		},
		methods: {
			goHome() {
				uni.switchTab({
					url: '/pages/tabBar/home/home'
				})
			},
			openCamera() {
				uni.showToast({
					title: '相机功能开发中',
					icon: 'none'
				})
			},
			goToLogin() {
				uni.navigateTo({
					url: '/pages/login/login'
				})
			},
			goToProfile() {
				uni.navigateTo({
					url: '/pages/profile/profile'
				})
			},
			goToSettings() {
				uni.navigateTo({
					url: '/pages/settings/settings'
				})
			},
			goToFeedback() {
				uni.navigateTo({
					url: '/pages/feedback/feedback'
				})
			},
			goToPoints() {
				uni.navigateTo({
					url: '/pages/points/points'
				})
			},
			goToInvite() {
				uni.navigateTo({
					url: '/pages/invite/invite'
				})
			},
			goToFAQ() {
				uni.navigateTo({
					url: '/pages/faq/faq'
				})
			},
			goToAbout() {
				uni.navigateTo({
					url: '/pages/about/about'
				})
			},

			// 测试登录功能 - 用于演示登录后的状态
			testLogin() {
				this.isLoggedIn = !this.isLoggedIn
				if (this.isLoggedIn) {
					uni.showToast({
						title: '登录成功',
						icon: 'success'
					})
				} else {
					uni.showToast({
						title: '已退出登录',
						icon: 'none'
					})
				}
			}
		},
		onLoad() {
			console.log('我的页面加载')

			// 监听登录成功事件
			uni.$on('loginSuccess', (data) => {
				this.isLoggedIn = data.isLoggedIn
			})
		},
		onShow() {
			// 页面显示时检查是否从登录页面返回
			const pages = getCurrentPages()
			const currentPage = pages[pages.length - 1]

			// 检查是否有登录成功的参数（实际项目中可能通过全局状态管理）
			if (currentPage.options && currentPage.options.loginSuccess) {
				this.isLoggedIn = true
				uni.showToast({
					title: '登录成功',
					icon: 'success'
				})
			}
		},
		onNavigationBarButtonTap(e) {
			// 导航栏按钮点击事件
			if (e.index === 0) {
				// 点击设置按钮
				this.goToSettings()
			}
		},
		onUnload() {
			// 移除事件监听
			uni.$off('loginSuccess')
		}
	}
</script>

<style scoped>
	.my-page {
		background: #000000;
		min-height: 100vh;
		color: #ffffff;
		position: relative;
		overflow: hidden;
	}

	/* 背景图（SVG）半透明覆盖层，可切换/删除 */
	.my-page::before {
		content: '';
		position: absolute;
		inset: 0;
		background: url('/static/icons/background.svg') center/cover no-repeat;
		opacity: 0.99;
		/* 可调：0 ~ 1 */
		pointer-events: none;
		z-index: 1;
	}

	/* 自定义悬浮标题（替代原生导航） */
	.custom-title {
		display: none;
	}

	.nav-float {
		position: absolute;
		top: 20pt;
		left: 0;
		right: 0;
		height: 32pt;
		display: flex;
		align-items: center;
		justify-content: center;
		z-index: 3;
	}

	.back-float {
		position: absolute;
		left: 16pt;
		width: 32pt;
		height: 32pt;
		display: flex;
		align-items: center;
		justify-content: center;
		color: #ffffff;
		opacity: 0.9;
	}

	.nav-title {
		font-family: PingFang SC, PingFang SC;
		font-weight: 600;
		font-size: 36rpx;
		color: #FFFFFF;
		line-height: 52rpx;
		text-align: center;
		font-style: normal;
		text-transform: none;
	}

	.settings-float {
		position: absolute;
		right: 16pt;
		width: 32pt;
		height: 32pt;
		display: flex;
		align-items: center;
		justify-content: center;
		z-index: 3;
	}

	.back-icon {
		font-size: 22pt;
		line-height: 1;
	}

	.camera-icon {
		font-size: 16pt;
		line-height: 1;
	}



	/* 用户登录区域 */
	.user-section {
		padding: 40px 20px 20px 20px;
		position: relative;
		z-index: 2;
	}

	.login-area {
		display: flex;
		align-items: center;
		background: rgba(255, 255, 255, 0.05);
		backdrop-filter: blur(20px);
		border-radius: 16px;
		position: relative;
		overflow: hidden;
	}

	.login-area::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background: linear-gradient(135deg, rgba(255, 255, 255, 0.1) 0%, rgba(255, 255, 255, 0.02) 100%);
		pointer-events: none;
	}

	.user-avatar {
		width: 128rpx;
		height: 128rpx;
		border-radius: 50%;
		margin-right: 24rpx;
		background-color: #333333;
		border: 1rpx solid rgba(255, 255, 255, 0.8);
	}

	.login-text {
		flex: 1;
		color: #ffffff;
		font-family: PingFang SC, PingFang SC;
		font-weight: 500;
		font-size: 40rpx;
		color: #FFFFFF;
		text-align: left;
		font-style: normal;
		text-transform: none;
	}

	.login-arrow {
		width: 36rpx;
		height: 36rpx;
		transform: rotateY(180deg);
		opacity: 0.5;
	}

	/* 已登录用户信息区域 */
	.user-info-area {
		display: flex;
		align-items: center;
		padding: 20px;
		background: rgba(255, 255, 255, 0.08);
		backdrop-filter: blur(20px);
		border-radius: 16px;
		border: 1px solid rgba(255, 255, 255, 0.15);
		position: relative;
		overflow: hidden;
		transition: all 0.3s ease;
	}

	.user-info-area.flex-mode {
		display: flex;
		align-items: center;
	}

	.user-info-area.flex-mode .user-avatar {
		position: static;
		width: 64pt;
		height: 64pt;
		margin-right: 12pt;
	}

	.user-info-area.flex-mode .user-details {
		position: static;
		display: flex;
		flex-direction: column;
	}

	.user-info-area.flex-mode .user-name {
		position: static;
		font-size: 20pt;
		line-height: 1.2;
	}

	.user-info-area.flex-mode .user-phone {
		position: static;
		margin-top: 6pt;
	}

	.user-info-area::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background: linear-gradient(135deg, rgba(0, 122, 255, 0.1) 0%, rgba(255, 255, 255, 0.05) 100%);
		pointer-events: none;
	}

	.user-info-area:active {
		transform: translateY(1px);
	}

	.user-details {
		flex: 1;

		position: relative;
		z-index: 1;
	}

	.user-name {
		font-size: 20px;
		color: #ffffff;
		font-weight: 600;
		margin-bottom: 4px;
		display: block;
	}

	.user-phone {
		font-size: 14px;
		color: rgba(255, 255, 255, 0.7);
		display: block;
	}

	.profile-arrow {
		font-size: 18px;
		color: rgba(255, 255, 255, 0.6);
		position: absolute;
		right: 12pt;
		top: 50%;
		transform: translateY(-50%);
		z-index: 1;
	}

	/* 功能菜单卡片 */
	.menu-card {
		margin: 20pt;
		background: rgba(255, 255, 255, 0.05);
		backdrop-filter: blur(20px);
		border-radius: 16px;
		border: 1px solid rgba(255, 255, 255, 0.1);
		overflow: hidden;
		position: relative;
		z-index: 2;
	}

	.menu-card::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background: linear-gradient(135deg, rgba(255, 255, 255, 0.08) 0%, rgba(255, 255, 255, 0.02) 100%);
		pointer-events: none;
	}

	.menu-item {
		display: flex;
		align-items: center;
		padding: 20px;
		border-bottom: none;
		/* 移除分割线 */
		position: relative;
		transition: background-color 0.3s ease;
	}

	.menu-item:last-child {
		border-bottom: none;
	}

	.menu-item:active {
		background-color: rgba(255, 255, 255, 0.05);
	}

	/* 绝对定位条目容器：以页面坐标安放每行（不参与卡片内的流式布局） */
	.menu-card.abs-items {
		height: 520pt;
		/* 预留可视高度，防止溢出；可按需要调整 */
		/* 移除底卡片视觉，改由每一行自身承载卡片效果 */
		background: transparent;
		border: none;
		backdrop-filter: none;
		overflow: visible;

		/* 可调的行卡片变量 */
		--item-bg: rgba(255, 255, 255, 0.05);
		--item-border: rgba(255, 255, 255, 0.10);
		--item-blur: 12px;
		--item-shadow: 0 8pt 20pt rgba(0, 0, 0, 0.35);
		--item-inset-shadow: 0 1pt 0 rgba(255, 255, 255, 0.04) inset;
	}

	.menu-card.abs-items .abs-item {
		position: absolute;
		left: var(--x);
		top: var(--y);
		width: var(--w);
		height: var(--h);
		border-radius: var(--radius, 12pt);
		background: var(--item-bg);
		border: 1px solid var(--item-border);
		backdrop-filter: blur(var(--item-blur));
		box-shadow: var(--item-shadow), var(--item-inset-shadow);
		overflow: hidden;
	}

	/* 箭头绝对定位（文本或SVG均可） */
	.menu-card.abs-items .abs-item .menu-arrow {
		position: absolute;
		left: var(--arrow-x, auto);
		top: var(--arrow-y, auto);
		width: var(--arrow-w, auto);
		height: var(--arrow-h, auto);
		color: var(--arrow-color, rgba(255, 255, 255, 0.3));
		font-size: var(--arrow-font, 16pt);
	}

	/* 绝对定位模式下，隐藏旧的图标容器背景，避免重复视觉元素 */
	.menu-card.abs-items .abs-item .menu-icon-container {
		display: none;
	}

	/* 单大卡片背景板：暂时隐藏，避免重叠 */
	.menu-card-bg {
		display: none;
	}

	/* 绝对定位版个人中心（蓝湖标注友好） */
	.user-section.abs-profile {
		/* 可在此处按蓝湖标注填写 */
		--profile-x: 40rpx;
		--profile-y: 200rpx;
		/* 再上移 */
		--profile-w: calc(100% - 80rpx);
		--profile-h: 192rpx;

		/* 子元素相对定位容器 */
		position: relative;
		padding: 0;
		/* 交由变量定位 */
		height: calc(var(--profile-y) + var(--profile-h));
	}

	.user-section.abs-profile .login-area,
	.user-section.abs-profile .user-info-area {
		position: absolute;
		left: var(--profile-x);
		top: var(--profile-y);
		width: var(--profile-w);
		height: var(--profile-h);
		display: flex;
		align-items: center;
		background: transparent;
		/* 浮层：去背景 */
		border: none;
		/* 去边框 */
		backdrop-filter: none;
		/* 去毛玻璃 */
	}

	/* 头像与文案绝对定位变量，可按需填写 */
	.user-section.abs-profile {
		--avatar-left: 20pt;
		--avatar-top: 8pt;
		--avatar-size: 64pt;
		/* 与蓝湖 64pt 一致 */
		--name-left: 100pt;
		--name-top: 24pt;
		--name-width: 220pt;
		--name-font: 20pt;
		--phone-left: 100pt;
		--phone-top: 44pt;
		--phone-width: 200pt;
		--phone-font: 12pt;
	}

	.user-section.abs-profile .user-info-area .user-avatar {
		position: absolute;
		left: var(--avatar-left);
		top: var(--avatar-top);
		width: var(--avatar-size);
		height: var(--avatar-size);
		border-radius: 50%;
		border: none;
	}

	.user-section.abs-profile .user-info-area .user-details {
		position: absolute;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
	}

	.user-section.abs-profile .user-info-area .user-name {
		position: absolute;
		left: var(--name-left);
		top: calc(var(--name-top) + 6pt);
		/* 下移，避开头像 */
		width: var(--name-width);
		font-size: var(--name-font);
	}

	.user-section.abs-profile .user-info-area .user-phone {
		position: absolute;
		left: var(--phone-left);
		top: var(--phone-top);
		width: var(--phone-width);
		font-size: var(--phone-font);
	}

	/* 关闭浮层下伪元素渐变，保持彻底透明 */
	.user-section.abs-profile .login-area::before,
	.user-section.abs-profile .user-info-area::before {
		display: none;
	}

	/* 避免与绝对定位的个人中心重叠，菜单卡片自动下移 */
	.user-section.abs-profile+.menu-card {
		margin-top: 8pt;
		/* 减小间距，避免与头像区产生视觉断层 */
	}

	/* 按你的标注对“问题反馈”这一行做定制 */
	.feedback-item {
		height: 50pt;
		/* 容器高度 */
		border-radius: 12pt;
		/* 四角 12pt */
		--icon-size: 24pt;
		/* 图标 24pt */
	}

	/* 移除“问题反馈”图标单独尺寸，统一由 --icon-size 控制 */

	.feedback-item .menu-title {
		width: auto;
		font-family: 'PingFang SC', 'PingFang SC-Medium', -apple-system, BlinkMacSystemFont, 'Helvetica Neue', Arial, 'Noto Sans CJK SC', sans-serif;
		font-weight: 500;
		text-align: left;
		background-color: transparent;
		font-size: 16px;
		/* 与下方保持一致 */
		letter-spacing: 0;
		line-height: normal;
		color: #FFFFFF;
	}

	.menu-icon-container {
		width: auto;
		height: auto;
		border-radius: 0;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-right: 12px;
		border: none;
		background: transparent;
	}

	.menu-icon-container.feedback,
	.menu-icon-container.points,
	.menu-icon-container.invite,
	.menu-icon-container.faq,
	.menu-icon-container.about,
	.menu-icon-container.test {
		background: transparent !important;
	}

	.menu-icon {
		font-size: 18px;
		color: #ffffff;
		font-weight: bold;
	}

	.menu-title {
		flex: 1;
		font-size: 16px;
		color: #ffffff;
		font-weight: 500;
	}

	.menu-arrow {
		font-size: 16px;
		color: rgba(255, 255, 255, 0.6);
	}

	/* 响应式适配 */
	@media (max-width: 750px) {
		.user-section {
			padding: 32px 16px 16px 16px;
		}

		.menu-card {
			margin: 16px;
		}

		.menu-item {
			padding: 16px;
		}

		.user-avatar {
			width: 50px;
			height: 50px;
			border-radius: 25px;
		}


	}
</style>
<style scoped>
	/* SVG 图标占位样式与参数（用于替换现有文字图标） */

	/* 默认变量，可在 .my-page 或具体元素上覆写 */
	.my-page {
		--icon-size: 22pt;
		/* 统一菜单图标尺寸 */
		--icon-color: #ffffff;
		--icon-stroke: transparent;
		--icon-stroke-width: 0;
		--icon-opacity: 1;
	}

	/* 图标容器中的通用插槽（可包裹 svg 或 image） */
	.menu-icon-slot {
		display: flex;
		align-items: center;
		justify-content: center;
		width: var(--icon-size);
		height: var(--icon-size);
		margin-right: 12px;
	}

	/* 直接给 <svg> 或 <image> 添加该类即可 */
	.menu-icon-svg {
		width: var(--icon-size);
		height: var(--icon-size);
		display: block;
		color: var(--icon-color);
		opacity: var(--icon-opacity);
	}

	/* 兼容在 scoped 下嵌套的 svg（无需额外类名） */
	.menu-icon-container :deep(svg) {
		width: var(--icon-size);
		height: var(--icon-size);
		display: block;
		color: var(--icon-color);
		opacity: var(--icon-opacity);
	}

	/* 使大多数内联 path 继承 currentColor（需 svg 未硬编码 fill） */
	.menu-icon-container :deep(path) {
		fill: currentColor;
		stroke: var(--icon-stroke);
		stroke-width: var(--icon-stroke-width);
	}

	/* 快捷尺寸工具类 */
	.icon-size-sm {
		--icon-size: 18px;
	}

	.icon-size-md {
		--icon-size: 22px;
	}

	.icon-size-lg {
		--icon-size: 26px;
	}

	/* 快捷颜色工具类（可按需改为你的主色） */
	.icon-color-primary {
		--icon-color: #ffffff;
	}

	.icon-color-info {
		--icon-color: #4facfe;
	}

	.icon-color-success {
		--icon-color: #43e97b;
	}

	.icon-color-warning {
		--icon-color: #F7931E;
	}

	.icon-color-danger {
		--icon-color: #f5576c;
	}

	.icon-dim {
		--icon-opacity: 0.7;
	}

	/* 描边辅助（你的 svg 需要 path 未硬编码 stroke） */
	.icon-stroke {
		--icon-stroke: rgba(255, 255, 255, 0.9);
		--icon-stroke-width: 1.5;
	}

	/* 玻璃态图标背景（用于需要更轻的图标底） */
	.menu-icon-container.is-glass {
		background: rgba(255, 255, 255, 0.06);
		border: 1px solid rgba(255, 255, 255, 0.14);
		backdrop-filter: blur(12px);
	}

	/* 点击反馈 */
	.menu-item:active .menu-icon-container {
		transform: scale(0.98);
	}
</style>