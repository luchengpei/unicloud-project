<template>
	<view>
		<u-toast ref="uToast" />
		<!--logo-->
		<view class="logo-box">
			<image
				src="https://6e69-niew6-1302638010.tcb.qcloud.la/%E8%83%8C%E6%99%AF/logo.png?sign=5d11ed914e4c29acd6ef9ddd7671a5c7&t=1615006414"
				mode="widthFix"></image>
		</view>
		<view class="login-form">
			<!--提示信息-->
			<view class="tip-box">
				<view class="upper">
					<image src="/static/other/2.png"></image>
					<text>欢迎加入!</text>
				</view>
				<view class="lower">请输入您的账号/密码登录!</view>
			</view>
			<view class="row">
				<view class="left os-center">
					<!-- <view style="font-size: 40rpx;padding-bottom: 5rpx;color: #041B3D;">+</view> -->
					<view >账号</view>
				</view>
				<input type="text" v-model="account" placeholder="请输入账号" maxlength="11"
					placeholder-class="input-placeholder" />
				<view class="right os-center">
					<image src="/static/other/1.png" mode="widthFix"></image>
				</view>
			</view>
			<view class="row">
				<view class="left os-center">
					<view>密码</view>
				</view>
				<input :type="showPassword?'text':'password'" v-model="password" placeholder="请输入密码" @input="passwordInput" maxlength="20"
					placeholder-class="input-placeholder" />
				<view class="right os-center" @click="showPassword=!showPassword">
					<image v-if="passwordShow" src="/static/other/4.png" mode="widthFix"></image>
				</view>
			</view>
			<view class="login-btn" @click="submit">
				<text>注册</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				account: '',
				password: '',
				passwordShow: false,
				showPassword:false
			}
		},
		methods: {
			//密码框输入事件
			passwordInput(e) {
				this.passwordShow = e.detail.value=='' ? false : true
			},
			submit(){
				uni.getUserInfo({
					success: (user) => {
						const {userInfo} = user
						uniCloud.callFunction({
							name:'user-center',
							data:{
								action:'register',
								params:{
									username:this.account,
									password:this.password,
									...userInfo
								}
							},
							success: (res) => {
								if(res.result.code==0){
									uni.setStorageSync('uniIdToken',res.result.token)
									getApp().globalData.uid = res.result.uid
									getApp().globalData.uniLogin = false
								}
								uni.navigateTo({
									url:'../login/login'
								})
							}
						})
					}
				})		
			}
		}
	}
</script>

<style lang="scss">
	page {
		position: relative;
		width: 100vw;
		height: 100vh;
		background-color: #F6F7FB;
	}

	.logo-box {
		width: 100%;
		height: 420rpx;
		display: flex;
		justify-content: center;
		align-items: flex-end;
		box-sizing: 100%;

		image {
			width: 500rpx;
			height: 250rpx;
		}
	}

	.login-form {
		margin: 0 60rpx;

		.tip-box {
			margin-top: 90rpx;
			height: 200rpx;
			flex-direction: column;

			.upper {
				height: 100rpx;
				font-size: 48rpx;
				font-family: Source Han Sans SC;
				font-weight: 400;
				color: #041B3D;

				image {
					padding-top: 10rpx;
					width: 50rpx;
					height: 50rpx;
				}

				text {
					padding-left: 30rpx;
				}
			}

			.lower {
				font-size: 28rpx;
				font-family: Source Han Sans SC;
				font-weight: 400;
				color: #7F8B9E;
			}
		}

		.row {
			margin-bottom: 30rpx;
			display: flex;
			justify-content: flex-start;
			align-items: center;
			height: 128rpx;
			border-radius: 30rpx;
			background-color: #FFFFFF;

			.left {
				width: 152rpx;
				height: 100%;
				font-size: 28rpx;
				font-family: Source Han Sans SC;
				font-weight: 400;
				color: #7F8B9E;
			}

			.account {
				font-size: 42rpx;
				font-family: Source Han Sans SC;
				font-weight: 400;
				color: #041B3D;
			}


			input {
				color: #223653;
				font-family: Source Han Sans SC;
				font-weight: 400;
				width: 470rpx;
				font-size: 28rpx;
			}

			.right {
				width: 138rpx;

				image {
					width: 36rpx;
					height: 36rpx;
				}
			}
		}
		
		.os-center{
			display: flex;
			justify-content: center;
			align-items: center;
		}

		.login-btn {
			margin-top: 20rpx;
			display: flex;
			align-items: center;
			justify-content: center;
			font-size: 35rpx;
			font-family: Source Han Sans SC;
			height: 110rpx;
			color: #FFFFFF;
			border-radius: 25rpx;
			background-color: #407bff;
		}

	}

	.input-placeholder {
		line-height: 100rpx;
		font-size: 28rpx;
		font-family: Source Han Sans SC;
		font-weight: 400;
		color: #ACAFB9;
	}
</style>
