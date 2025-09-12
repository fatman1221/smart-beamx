<template>
	<view class="profile-page">
		<view class="profile-nav">
			<image class="nav-back" @click="goBack" src="@/static/icons/my/back2x.png" mode="aspectFill" alt="" srcset="" />
			<text class="nav-title">个人信息</text>
		</view>
		<!-- 个人信息主页面 -->
		<view class="profile-card">
			<!-- 头像区域 -->
			<view class="profile-item" @click="changeAvatar">
				<text class="profile-label">头像</text>
				<view class="profile-content">
					<image class="user-avatar" :src="userInfo.avatar" mode="aspectFill"></image>
					<image class="profile-arrow" src="@/static/icons/my/back2x.png" mode="aspectFill" alt="" srcset="" />
				</view>
			</view>

			<!-- 昵称 -->
			<view class="profile-item" @click="editNickname">
				<text class="profile-label">昵称</text>
				<view class="profile-content">
					<text class="profile-value">{{ userInfo.nickname }}</text>
			
					<image class="profile-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill" />
					
				</view>
			</view>

			<!-- 手机号 -->
			<view class="profile-item" @click="editPhone">
				<text class="profile-label">手机</text>
				<view class="profile-content">
					<text class="profile-value">{{ userInfo.phone }}</text>
					<image class="profile-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill" />
				</view>
			</view>

			<!-- 邮箱 -->
			<view class="profile-item" @click="editEmail">
				<text class="profile-label">邮箱</text>
				<view class="profile-content">
					<text class="profile-value">{{ userInfo.email }}</text>
				<image class="profile-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill" />
				
				</view>
			</view>

			<!-- 密码 -->
			<view class="profile-item" @click="setPassword">
				<text class="profile-label">密码</text>
				<view class="profile-content">
				<image class="profile-arrow" src="@/static/icons/my/back2x.png" alt="" srcset="" mode="aspectFill" />
				
				</view>
			</view>
		</view>


	</view>
</template>

<script>
	export default {
		name: 'ProfilePage',
		data() {
			return {
				// 已移除单页切换逻辑，改为独立路由页面
				userInfo: {
					avatar: 'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?w=400&h=400&fit=crop&crop=face',
					nickname: '小米洋',
					phone: '188****8888',
					email: '188****5678@gmail.com'
				},
				editForm: {
					avatar: '',
					nickname: '',
					phone: '',
					newEmail: '',
					email: '',
					password: '',
					confirmPassword: ''
				},
				verifyCode: ['', '', '', '', '', ''],
				emailVerifyCode: ['', '', '', '', '', '']
			}
		},
		methods: {
			goBack() {
				console.log('个人信息页面返回按钮点击')
				uni.switchTab({
					url: '/pages/tabBar/my/my',
					success: () => {
						console.log('成功跳转到我的页面')
					},
					fail: (err) => {
						console.log('跳转失败:', err)
						// 备用方案：直接返回
						uni.navigateBack({
							delta: 1
						})
					}
				})
			},
			// 编辑昵称
			editNickname() {
				uni.navigateTo({
					url: `/pages/profile/nickname?current=${encodeURIComponent(this.userInfo.nickname)}`
				})
			},

			// 编辑手机号
			editPhone() {
				uni.navigateTo({
					url: `/pages/profile/phone?current=${encodeURIComponent(this.userInfo.phone)}`
				})
			},

			// 手机号下一步
			nextStepPhone() {
				if (!this.editForm.phone || this.editForm.phone.length !== 11) {
					uni.showToast({
						title: '请输入正确的手机号',
						icon: 'none'
					})
					return
				}
				this.currentPage = 'phoneVerify'
				this.verifyCode = ['1', '8', '7', '7', '7', '9']
			},
			onPhoneInput(e) {
				const onlyDigits = (e.detail.value || '').replace(/\D+/g, '')
				this.editForm.phone = onlyDigits
			},

			// 输入验证码
			inputCode(e, index) {
				this.verifyCode[index] = e.detail.value
				// 自动跳转到下一个输入框
				if (e.detail.value && index < 5) {
					// 这里可以添加自动聚焦下一个输入框的逻辑
				}
			},

			// 提交手机号变更
			submitPhoneChange() {
				const code = this.verifyCode.join('')
				if (code.length !== 6) {
					uni.showToast({
						title: '请输入完整验证码',
						icon: 'none'
					})
					return
				}

				this.userInfo.phone = this.editForm.phone.replace(/(\d{3})(\d{4})(\d{4})/, '$1****$3')
				this.currentPage = 'main'
				uni.showToast({
					title: '手机号修改成功',
					icon: 'success'
				})
			},

			// 更换头像
			changeAvatar() {
				uni.navigateTo({
					url: `/pages/profile/avatar?current=${encodeURIComponent(this.userInfo.avatar)}`
				})
			},

			// 选择头像
			selectAvatar() {
				uni.chooseImage({
					count: 1,
					sizeType: ['compressed'],
					sourceType: ['album', 'camera'],
					success: (res) => {
						this.editForm.avatar = res.tempFilePaths[0]
						this.userInfo.avatar = res.tempFilePaths[0]
						this.currentPage = 'main'
						uni.showToast({
							title: '头像更新成功',
							icon: 'success'
						})
					}
				})
			},

			// 编辑邮箱
			editEmail() {
				uni.navigateTo({
					url: `/pages/profile/email?current=${encodeURIComponent(this.userInfo.email)}`
				})
			},

			// 手机号验证
			verifyByPhone() {
				this.currentPage = 'emailEdit'
				this.editForm.email = this.userInfo.email
			},

			// 邮箱验证
			verifyByEmail() {
				this.currentPage = 'emailEdit'
				this.editForm.email = this.userInfo.email
			},

			// 完成邮箱设置
			completeEmailChange() {
				if (!this.editForm.newEmail) {
					uni.showToast({
						title: '请输入邮箱地址',
						icon: 'none'
					})
					return
				}
				this.currentPage = 'emailVerify'
				this.emailVerifyCode = ['1', '8', '7', '7', '7', '9']
			},

			// 输入邮箱验证码
			inputEmailCode(e, index) {
				this.emailVerifyCode[index] = e.detail.value
			},

			// 提交邮箱变更
			submitEmailChange() {
				const code = this.emailVerifyCode.join('')
				if (code.length !== 6) {
					uni.showToast({
						title: '请输入完整验证码',
						icon: 'none'
					})
					return
				}

				this.userInfo.email = this.editForm.newEmail.replace(/(.{3}).+(@.+)/, '$1****$2')
				this.currentPage = 'main'
				uni.showToast({
					title: '邮箱修改成功',
					icon: 'success'
				})
			},

			// 设置密码
			setPassword() {
				uni.navigateTo({
					url: '/pages/profile/password'
				})
			},

			// 提交密码变更
			submitPasswordChange() {
				if (!this.editForm.password || !this.editForm.confirmPassword) {
					uni.showToast({
						title: '请输入密码',
						icon: 'none'
					})
					return
				}

				if (this.editForm.password !== this.editForm.confirmPassword) {
					uni.showToast({
						title: '两次密码不一致',
						icon: 'none'
					})
					return
				}

				this.currentPage = 'main'
				uni.showToast({
					title: '密码设置成功',
					icon: 'success'
				})
			},

			// 提交昵称变更
			submitNicknameChange() {
				const nickname = (this.editForm.nickname || '').trim()
				if (!nickname) {
					uni.showToast({
						title: '请输入昵称',
						icon: 'none'
					})
					return
				}
				this.userInfo.nickname = nickname
				this.currentPage = 'main'
				uni.showToast({
					title: '昵称修改成功',
					icon: 'success'
				})
			}
		},
		onLoad() {
			console.log('个人信息页面加载')
			// 监听子页面的数据更新
			uni.$on('updateNickname', (data) => {
				this.userInfo.nickname = data.nickname
			})
			uni.$on('updatePhone', (data) => {
				this.userInfo.phone = data.phone
			})
			uni.$on('updateEmail', (data) => {
				this.userInfo.email = data.email
			})
			uni.$on('updateAvatar', (data) => {
				this.userInfo.avatar = data.avatar
			})
		},
		onUnload() {
			// 移除事件监听
			uni.$off('updateNickname')
			uni.$off('updatePhone')
			uni.$off('updateEmail')
			uni.$off('updateAvatar')
		}
	}
</script>

<style scoped>
	.profile-page {
		position: relative;
		background: #000;
		min-height: 100vh;
		color: #fff;
		padding: 0;
	}

	.profile-page::before {
		content: '';
		position: absolute;
		inset: 0;
		background: url('/static/icons/background.svg') center/cover no-repeat;
		opacity: .99;
		pointer-events: none;
		z-index: 0;
	}

	.profile-nav {
		position: sticky;
		top: 22rpx;
    margin-bottom: 46rpx;
		height: 44pt;
		z-index: 2;
	}

	.nav-back {
		position: absolute;
		left: 20rpx;
		top: 54rpx;
		width: 40rpx;
		height: 40rpx;
		display: flex;
		align-items: center;
		justify-content: center;
		color: #fff;
		cursor: pointer;
		z-index: 10;
	}

	.back-icon {
		font-size: 22pt;
		line-height: 1;
	}

	.nav-title {
		position: absolute;
		left: 0;
		right: 0;
		top: 20pt;
		text-align: center;
		color: #ffffff;
	
		font-weight: 600;
		
		font-family: PingFang SC, PingFang SC;
	
		font-size: 36rpx;
		color: #FFFFFF;
		line-height: 52rpx;
		text-align: center;
		font-style: normal;
		text-transform: none;
	}

	/* 个人信息卡片 */
	.profile-card {
		margin: 20px;
		background: #1A1A1A;
		backdrop-filter: blur(20px);
		border-radius: 32rpx;

		overflow: hidden;
	}

	.profile-item {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 26rpx 32rpx;
	
		cursor: pointer;
		transition: all 0.3s ease;
	}

	.profile-item:last-child {
		border-bottom: none;
	}

	.profile-item:active {
		background: rgba(255, 255, 255, 0.05);
	}

	.profile-label {
		font-size: 16px;
		color: #ffffff;
		font-weight: 500;
	}

	.profile-content {
		display: flex;
		align-items: center;
		gap: 12px;
	}

	.profile-value {
		font-size: 16px;
		color: #cccccc;
	}

	.profile-arrow {
		width: 36rpx;
		height: 36rpx;
		transform: rotateY(180deg);
		opacity: 0.5; 
	}

	.user-avatar {
		width: 50px;
		height: 50px;
		border-radius: 25px;
		border: 2px solid rgba(255, 255, 255, 0.2);
	}

	/* 编辑页面 */
	.edit-page {
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		padding: 40px 20px;
		position: relative;
		z-index: 1;
	}

	.edit-header {
		margin-bottom: 60px;
	}

	.edit-title {
		font-size: 24px;
		font-weight: 600;
		color: #ffffff;
		margin-bottom: 12px;
		display: block;
	}

	.edit-subtitle {
		font-size: 16px;
		color: #999999;
		display: block;
	}

	.edit-content {
		flex: 1;
		display: flex;
		flex-direction: column;
		gap: 40px;
	}

	.edit-input {
		width: 100%;
		padding: 20px 24px;
		background: rgba(255, 255, 255, 0.05);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 16px;
		color: #ffffff;
		font-size: 16px;
		text-align: center;
		outline: none;
		transition: all 0.3s ease;
	}

	.phone-input {
		ime-mode: disabled;
	}

	.edit-input:focus {
		border-color: rgba(255, 255, 255, 0.2);
		background: rgba(255, 255, 255, 0.08);
	}

	.edit-input::placeholder {
		color: rgba(255, 255, 255, 0.4);
	}

	.password-input {
		text-align: left;
		margin-bottom: 24px;
		padding: 24px;
		font-size: 18px;
		min-height: 60px;
	}

	.edit-btn {
		width: 100%;
		padding: 16px;
		background: rgba(255, 255, 255, 0.1);
		color: #ffffff;
		border: none;
		border-radius: 16px;
		font-size: 16px;
		font-weight: 500;
		cursor: pointer;
		transition: all 0.3s ease;
	}

	.edit-btn:active {
		background: rgba(255, 255, 255, 0.15);
	}

	/* 验证码输入 */
	.code-input-container {
		display: grid;
		grid-template-columns: repeat(6, 1fr);
		gap: 12px;
		margin-bottom: 40px;
	}

	.code-input {
		aspect-ratio: 1;
		background: rgba(255, 255, 255, 0.05);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 12px;
		color: #ffffff;
		font-size: 24px;
		font-weight: 600;
		text-align: center;
		outline: none;
		transition: all 0.3s ease;
	}

	.code-input:focus {
		border-color: rgba(255, 255, 255, 0.2);
		background: rgba(255, 255, 255, 0.08);
	}

	/* 头像编辑 */
	.avatar-edit {
		align-items: center;
		justify-content: center;
		text-align: center;
	}

	.avatar-preview {
		margin-bottom: 40px;
	}

	.preview-avatar {
		width: 120px;
		height: 120px;
		border-radius: 60px;
		border: 3px solid rgba(255, 255, 255, 0.2);
	}

	/* 验证选择 */
	.verify-option {
		width: 100%;
		padding: 20px;
		background: rgba(255, 255, 255, 0.05);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 16px;
		color: #ffffff;
		font-size: 16px;
		font-weight: 500;
		cursor: pointer;
		transition: all 0.3s ease;
		margin-bottom: 20px;
	}

	.verify-option:active {
		background: rgba(255, 255, 255, 0.1);
	}

	/* 响应式设计 */
	@media (max-width: 750px) {
		.profile-card {
			margin: 16px;
		}

		.profile-item {
			padding: 16px;
		}

		.edit-page {
			padding: 32px 16px;
		}

		.user-avatar {
			width: 40px;
			height: 40px;
			border-radius: 20px;
		}
	}
</style>