<template>
	<view class="about-page">
		<view class="page-nav">
			<image class="nav-back" @click="goBack" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill" />

			<text class="page-title">关于我们</text>
		</view>
		<!-- 主要内容容器 -->
		<view class="main-container">
			<!-- 应用图标和信息 -->
			<view class="app-info">
				<view class="app-icon">
					<view class="icon-placeholder"></view>
				</view>
				<text class="app-name">XXX</text>
				<text class="app-version">Version {{ appVersion }}</text>
			</view>

			<!-- 关于平台描述 -->
			<view class="about-content">
				<text class="about-title">关于平台：</text>
				<text class="about-description">
					我们重新定义汽车灯光——不止于照明，更是情绪的表达与个性的延伸。车内256色智能氛围灯，随心情、音乐、驾驶模式自由变幻，打造专属移动光境；车外动态效果灯，以呼吸式迎宾光效与交互灯语，让每一次出行都充满仪式感。用科技点亮灵感，用光影讲述故事，让你的爱车成为独一无二的光影艺术品。
				</text>
			</view>

			<!-- 协议选项 -->
			<view class="agreements-container">
				<view class="agreement-section" @click="showServiceAgreement">
					<text class="agreement-text">服务协议</text>
				<image class="agreement-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill" />
				
				</view>

				<view class="agreement-section" @click="showPrivacyPolicy">
					<text class="agreement-text">隐私协议</text>
					<image class="agreement-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" />

				</view>
			</view>
		</view>

		<!-- 服务协议弹窗 -->
		<view v-if="showServiceModal" class="modal-overlay" @click="closeServiceModal">
			<view class="modal-content" @click.stop>
				<view class="modal-header">
					<text class="modal-title">服务协议</text>
					<text class="modal-close" @click="closeServiceModal">×</text>
				</view>
				<scroll-view class="modal-body" scroll-y>
					<text class="agreement-content">
						一、服务条款的确认和接纳

						本服务协议（以下简称"协议"）是您与SmartBeamX智能汽车灯光系统（以下简称"本平台"）之间就使用本平台服务所订立的协议。

						二、服务内容

						1. 智能汽车灯光控制：提供车内外灯光的智能化控制功能
						2. 个性化设置：支持256色氛围灯自定义调节
						3. 场景模式：提供多种预设灯光场景模式
						4. 音乐同步：灯光与音乐节拍同步变化功能
						5. 远程控制：通过手机APP远程控制车辆灯光

						三、用户权利和义务

						1. 用户有权享受本平台提供的各项服务
						2. 用户应合法使用本服务，不得用于违法用途
						3. 用户应保护好账户信息，避免账户被盗用
						4. 用户不得恶意破坏本平台的正常运行

						四、隐私保护

						本平台严格保护用户隐私信息，详见《隐私协议》。

						五、免责声明

						1. 因不可抗力导致的服务中断，本平台不承担责任
						2. 用户违法使用导致的后果，本平台不承担责任
						3. 第三方原因导致的损失，本平台不承担责任

						六、协议的修改和终止

						本平台有权根据需要修改本协议，修改后的协议将在平台上公布。

						七、法律适用

						本协议适用中华人民共和国法律法规。

						八、争议解决

						因本协议产生的争议，双方应友好协商解决；协商不成的，可向本平台所在地人民法院提起诉讼。

						本协议自用户点击同意之日起生效。
					</text>
				</scroll-view>
			</view>
		</view>

		<!-- 隐私协议弹窗 -->
		<view v-if="showPrivacyModal" class="modal-overlay" @click="closePrivacyModal">
			<view class="modal-content" @click.stop>
				<view class="modal-header">
					<text class="modal-title">隐私协议</text>
					<text class="modal-close" @click="closePrivacyModal">×</text>
				</view>
				<scroll-view class="modal-body" scroll-y>
					<text class="agreement-content">
						SmartBeamX隐私政策

						最后更新日期：2024年1月1日

						一、信息收集

						我们可能收集以下类型的信息：

						1. 个人识别信息
						- 姓名、电话号码、邮箱地址
						- 设备标识符、IP地址
						- 位置信息（在您授权的情况下）

						2. 使用数据
						- 应用使用情况和功能偏好
						- 灯光设置和场景配置
						- 设备连接状态和性能数据

						3. 车辆信息
						- 车型、年份等基本信息
						- 灯光系统状态和配置
						- 故障诊断数据

						二、信息使用

						我们使用收集的信息用于：

						1. 提供和改进服务功能
						2. 个性化用户体验
						3. 技术支持和客户服务
						4. 安全监控和欺诈防范
						5. 产品开发和功能优化

						三、信息共享

						除以下情况外，我们不会与第三方共享您的个人信息：

						1. 经您明确同意
						2. 法律法规要求
						3. 维护平台安全和其他用户权益
						4. 与可信的服务提供商合作（在严格保密协议下）

						四、信息安全

						我们采取以下措施保护您的信息：

						1. 数据加密传输和存储
						2. 访问权限控制
						3. 定期安全审计
						4. 员工保密培训

						五、您的权利

						您有权：

						1. 查看、更正或删除个人信息
						2. 撤回同意授权
						3. 投诉和举报隐私问题
						4. 数据可携带权

						六、Cookie和类似技术

						我们使用Cookie等技术来：
						- 记住您的偏好设置
						- 分析使用模式
						- 提供个性化内容

						七、儿童隐私

						我们不会故意收集13岁以下儿童的个人信息。

						八、隐私政策更新

						我们可能会不时更新本隐私政策，重大变更会通过应用内通知等方式告知您。

						九、联系我们

						如对本隐私政策有疑问，请联系：
						邮箱：privacy@smartbeamx.com
						电话：400-888-0000

						感谢您信任SmartBeamX！
					</text>
				</scroll-view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'AboutPage',
		data() {
			return {
				appVersion: '1.0.1',
				showServiceModal: false,
				showPrivacyModal: false
			}
		},
		methods: {
			goBack() {
				const pages = getCurrentPages && getCurrentPages()
				if (pages && pages.length > 1) {
					uni.navigateBack({
						delta: 1
					})
				} else {
					uni.switchTab({
						url: '/pages/tabBar/my/my'
					})
				}
			},
			showServiceAgreement() {
				this.showServiceModal = true
			},
			closeServiceModal() {
				this.showServiceModal = false
			},
			showPrivacyPolicy() {
				this.showPrivacyModal = true
			},
			closePrivacyModal() {
				this.showPrivacyModal = false
			}
		},
		onLoad() {
			console.log('关于页面加载')
		}
	}
</script>

<style scoped>
	.about-page {
		position: relative;
		background-color: #000000;
		min-height: 100vh;
		color: #ffffff;
		padding: 20px;
	}

	.about-page::before {
		content: '';
		position: absolute;
		inset: 0;
		background: url('/static/icons/background.svg') center/cover no-repeat;
		opacity: 0.99;
		pointer-events: none;
		z-index: 0;
	}

	.page-nav {
		position: sticky;
		top: 0;
		text-align: center;
		padding: 16rpx 0;
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
	}

	.back-icon {
		font-size: 22pt;
		line-height: 1;
	}

	/* 主要内容容器 */
	.main-container {
		background-color: #1a1a1a;
		border-radius: 12px;
		margin-bottom: 12px;
		overflow: hidden;
		position: relative;
		z-index: 1;
	}

	/* 应用图标和信息 */
	.app-info {
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 40px 20px 32px 20px;
	}

	.app-icon {
		margin-bottom: 20px;
	}

	.icon-placeholder {
		width: 120px;
		height: 120px;
		background: #666666;
		border-radius: 60px;
	}

	.app-name {
		font-size: 24px;
		font-weight: 600;
		color: #ffffff;
		margin-bottom: 8px;
	}

	.app-version {
		font-size: 14px;
		color: #999999;
	}

	/* 关于平台描述 */
	.about-content {
		padding: 20px;
	}

	.about-title {
		font-size: 16px;
		color: #ffffff;
		margin-bottom: 16px;
		display: block;
		font-weight: 500;
	}

	.about-description {
		font-size: 14px;
		color: #cccccc;
		line-height: 1.6;
		display: block;
	}

	/* 协议选项 */
	.agreements-container {
		padding: 0;
	}

	.agreement-section {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 20px;
		cursor: pointer;
		transition: all 0.3s ease;
	}

	.agreement-section:last-child {
		border-bottom: none;
	}

	.agreement-section:active {
		background: rgba(255, 255, 255, 0.05);
	}

	.agreement-text {
		font-size: 16px;
		color: #ffffff;
		line-height: 1.5;
		flex: 1;
		margin-right: 16px;
	}

	.agreement-arrow {
		font-size: 20px;
		width: 36rpx;
		height: 36rpx;
		transform: rotateY(180deg);
		opacity: 0.5; 
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
	}

	.modal-content {
		background-color: #1a1a1a;
		border: 1px solid #333333;
		border-radius: 12px;
		width: 100%;
		max-width: 500px;
		max-height: 80vh;
		overflow: hidden;
	}

	.modal-header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 20px;
		border-bottom: 1px solid #333333;
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
		max-height: 60vh;
		padding: 20px;
	}

	.agreement-content {
		font-size: 14px;
		color: #cccccc;
		line-height: 1.6;
		white-space: pre-line;
		display: block;
	}
</style>