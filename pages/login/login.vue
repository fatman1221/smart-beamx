<template>
	<view class="login-page">
		<!-- 顶部悬浮：返回 + 标题（个人中心） -->
		<view class="login-nav">
			<text class="login-title">个人中心</text>
			<view class="login-settings" @click="goSettings">
				<image class="menu-icon-svg" src="/static/icons/settings.svg" mode="widthFix"
					style="width:22pt;height:22pt"></image>
			</view>
		</view>
		<!-- 头部logo和欢迎信息 -->
		<view class="header-section">
			<view class="logo-container">
				<view class="logo">logo</view>
				<text class="welcome-text">欢迎登录</text>
			</view>
		</view>

		<!-- 登录表单 -->
		<view class="form-container">
			<!-- 手机号验证登录 -->
			<view class="login-section">
				<text class="provider-text">中国移动提供认证服务</text>
				<view class="phone-display">
					<text class="phone-number">188****8888</text>
				</view>

				<!-- 协议条款 -->
				<view class="agreement-section">
					<view class="checkbox-container" @click="toggleAgreement">
						<view class="checkbox" :class="{ checked: agreedToTerms }">
							<text v-if="agreedToTerms" class="checkmark">✓</text>
						</view>
						<text class="agreement-text">
							我已阅读并同意《服务条款》和《隐私条款》
						</text>
					</view>
				</view>

				<!-- 验证登录按钮 -->
				<button class="login-btn" :class="{ disabled: !agreedToTerms }" :disabled="!agreedToTerms"
					@click="handlePhoneLogin">
					验证并登录
				</button>

				<!-- 其他登录方式 -->
				<view class="other-login">
					<text class="other-login-text" @click="showOtherMethods">其他号码登录</text>
				</view>
			</view>
		</view>

		<!-- 其他登录方式弹窗 -->
		<view v-if="showOtherModal" class="modal-overlay" @click="closeOtherModal">
			<view class="modal-content" @click.stop>
				<view class="modal-header">
					<text class="modal-title">其他登录方式</text>
					<text class="modal-close" @click="closeOtherModal">×</text>
				</view>
				<view class="modal-body">
					<view class="login-method" @click="handleManualLogin">
						<text class="method-icon">📱</text>
						<text class="method-text">手机号密码登录</text>
					</view>
					<view class="login-method" @click="handleWechatLogin">
						<text class="method-icon">💬</text>
						<text class="method-text">微信登录</text>
					</view>
					<view class="login-method" @click="handleEmailLogin">
						<text class="method-icon">📧</text>
						<text class="method-text">邮箱登录</text>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'LoginPage',
		data() {
			return {
				agreedToTerms: false,
				showOtherModal: false,
				phoneNumber: '188****8888'
			}
		},
		methods: {
			goSettings() {
				uni.navigateTo({
					url: '/pages/settings/settings'
				})
			},
			// 切换协议同意状态
			toggleAgreement() {
				this.agreedToTerms = !this.agreedToTerms
			},

			// 手机验证登录
			handlePhoneLogin() {
				if (!this.agreedToTerms) {
					uni.showToast({
						title: '请先同意服务条款',
						icon: 'none'
					})
					return
				}

				uni.showLoading({
					title: '验证中...'
				})

				// 模拟登录过程
				setTimeout(() => {
					uni.hideLoading()
					uni.showToast({
						title: '登录成功',
						icon: 'success'
					})

					// 登录成功后直接切换到"我的"页面，并通知登录状态
					setTimeout(() => {
						uni.redirectTo({
							url: '/pages/tabBar/my/my'
						})
						setTimeout(() => {
							uni.$emit('loginSuccess', {
								isLoggedIn: true
							})
						}, 200)
					}, 500)
				}, 2000)
			},

			// 显示其他登录方式
			showOtherMethods() {
				this.showOtherModal = true
			},

			// 关闭其他登录方式弹窗
			closeOtherModal() {
				this.showOtherModal = false
			},

			// 手动输入手机号登录
			handleManualLogin() {
				this.closeOtherModal()
				uni.showToast({
					title: '功能开发中',
					icon: 'none'
				})
			},

			// 微信登录
			handleWechatLogin() {
				this.closeOtherModal()
				uni.showToast({
					title: '功能开发中',
					icon: 'none'
				})
			},

			// 邮箱登录
			handleEmailLogin() {
				this.closeOtherModal()
				uni.showToast({
					title: '功能开发中',
					icon: 'none'
				})
			}
		},
		onLoad() {
			console.log('登录页面加载')
		}
	}
</script>

<style scoped>
	.login-page {
		position: relative;
		min-height: 100vh;
	}

	.login-nav {
		position: absolute;
		top: 20pt;
		left: 0;
		right: 0;
		height: 32pt;
		display: flex;
		align-items: center;
		justify-content: center;
		z-index: 2;
	}


	.login-settings {
		position: absolute;
		right: 16pt;
		width: 32pt;
		height: 32pt;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.login-title {
		font-family: PingFang SC, PingFang SC;
		font-weight: 600;
		font-size: 36rpx;
		color: #FFFFFF;
		line-height: 52rpx;
		text-align: center;
		font-style: normal;
		text-transform: none;
	}

	.login-page::before {
		content: '';
		position: absolute;
		inset: 0;
		background: url('/static/icons/background.svg') center/cover no-repeat;
		opacity: 0.99;
		/* 可调：0 ~ 1 */
		pointer-events: none;
		/* 不拦截点击 */
		z-index: 0;
	}

	/* 头部区域 */
	.header-section {
		display: flex;
		flex-direction: column;
		align-items: center;
		/* 默认居中 */
		padding: 228px 40px 60px 40px;
		/* 1.5 倍放大（从152px到228px） */
		position: relative;
		z-index: 1;
		/* 盖住背景 */
	}

	.logo-container {
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: flex-start;
		gap: 24rpx;
		align-self: flex-start;

		/* 控制距离屏幕左边的距离 */
		margin-top: 48rpx;
		/* 1.5 倍放大 */
	}



	.logo {
		width: 128rpx;
		height: 128rpx;
		background: #666666;
		border-radius: 50%;
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 16px;
		color: #ffffff;
		font-weight: 500;

	}

	.header-section .welcome-text {


		font-family: PingFang SC, PingFang SC;
		font-weight: 600;
		font-size: 56rpx;
		color: rgba(255, 255, 255, 0.9);

		text-align: left;
		font-style: normal;
		text-transform: none;

	}

	/* 表单容器 */
	.form-container {
		padding: 0 40px;
		flex: 1;
		position: relative;
		z-index: 1;
	}

	.login-section {
		background: rgba(255, 255, 255, 0.05);
		backdrop-filter: blur(20px);
		border-radius: 20px;
		border: 1px solid rgba(255, 255, 255, 0.1);
		padding: 40px 32px;
		position: relative;
		overflow: hidden;
	}

	.login-section::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background: linear-gradient(135deg, rgba(255, 255, 255, 0.08) 0%, rgba(255, 255, 255, 0.02) 100%);
		pointer-events: none;
	}

	.provider-text {
		font-size: 12pt;
		color: #999999;
		text-align: center;
		margin-bottom: 24px;
		display: block;
		position: relative;
		z-index: 1;
	}

	.phone-display {
		text-align: center;
		margin-bottom: 32px;
		position: relative;
		z-index: 1;
	}

	.phone-number {
		font-size: 28px;
		font-weight: 600;
		color: #ffffff;
		letter-spacing: 2px;
	}

	/* 协议条款 */
	.agreement-section {
		margin-bottom: 32rpx;
		position: relative;
		z-index: 1;
	}

	.checkbox-container {
		display: flex;
		align-items: center;
		cursor: pointer;
	}

	.checkbox {
		width: 28rpx;
		height: 28rpx;
		border-radius: 50%;
		border: 2px solid rgba(255, 255, 255, 0.3);
		margin-right: 8rpx;
		display: flex;
		align-items: center;
		justify-content: center;
		transition: all 0.3s ease;
	}

	.checkbox.checked {
		background-color: #007AFF;
		border-color: #007AFF;
	}

	.checkmark {
		font-size: 12px;
		color: #ffffff;
		font-weight: bold;
	}

	.agreement-text {
		font-size: 14px;
		color: #cccccc;
		line-height: 1.5;
		flex: 1;
	}

	/* 登录按钮 */
	.login-btn {
		box-sizing: border-box;
		width: 100%;
		height: 96rpx;
		line-height: 96rpx;
		background: linear-gradient(135deg, #ff6b35 0%, #f7931e 100%);
		color: #ffffff;
		border: none;
		border-radius: 20rpx;
		font-size: 32rpx;
		font-weight: 600;
		transition: all 0.3s ease;
		cursor: pointer;
		position: relative;
		z-index: 1;
		box-shadow: 0 4px 20px rgba(255, 107, 53, 0.3);
		color: rgba(255, 255, 255, 1);
		font-family: PingFang SC, PingFang SC;
	}

	.login-btn:hover {
		transform: translateY(-1px);
		box-shadow: 0 6px 25px rgba(255, 107, 53, 0.4);
	}

	.login-btn:active {
		transform: translateY(0);
	}

	.login-btn.disabled {
		color: rgba(255, 255, 255, 0.4);
		cursor: not-allowed;
		transform: none;
		box-shadow: none;
		opacity: 0.6;

	}

	/* 其他登录方式 */
	.other-login {
		text-align: center;
		margin-top: 24px;
		position: relative;
		z-index: 1;
	}

	.other-login-text {
		font-size: 14px;
		color: #999999;
		cursor: pointer;
		transition: color 0.3s ease;
	}

	.other-login-text:hover {
		color: #ffffff;
	}

	/* 弹窗样式 */
	.modal-overlay {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background-color: rgba(0, 0, 0, 0.8);
		display: flex;
		align-items: center;
		justify-content: center;
		z-index: 1000;
		padding: 20px;
		backdrop-filter: blur(10px);
	}

	.modal-content {
		background: rgba(255, 255, 255, 0.05);
		backdrop-filter: blur(30px);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 20px;
		width: 90%;
		max-width: 400px;
	}

	.modal-header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 20px 24px;
		border-bottom: 1px solid rgba(255, 255, 255, 0.1);
	}

	.modal-title {
		font-size: 18px;
		font-weight: 600;
		color: #ffffff;
	}

	.modal-close {
		font-size: 24px;
		color: #666666;
		cursor: pointer;
		width: 30px;
		height: 30px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 15px;
		transition: all 0.3s ease;
	}

	.modal-close:hover {
		background: rgba(255, 255, 255, 0.1);
		color: #ffffff;
	}

	.modal-body {
		padding: 24px;
	}

	.login-method {
		display: flex;
		align-items: center;
		padding: 16px 0;
		cursor: pointer;
		transition: all 0.3s ease;
		border-radius: 8px;
	}

	.login-method:hover {
		background: rgba(255, 255, 255, 0.05);
	}

	.method-icon {
		font-size: 20px;
		margin-right: 16px;
		width: 24px;
		text-align: center;
	}

	.method-text {
		font-size: 16px;
		color: #ffffff;
	}

	/* 响应式设计 */
	@media (max-width: 750px) {
		.header-section {
			padding: 60px 20px 40px 20px;
		}

		.form-container {
			padding: 0 20px;
		}

		.login-section {
			padding: 32px 24px;
		}

		.phone-number {
			font-size: 24px;
		}
	}
</style>