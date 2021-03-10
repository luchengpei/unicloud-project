<template>
	<view>
		<view class="head comm-center">
			<image :src="userInfo.avatarUrl"></image>
			<view class="name">{{userInfo.username}}</view>
			<view class="remarks">{{userInfo.nickName}}</view>
		</view>
		<view class="list-menu">
			<view class="cell" v-for="(item,index) in list" :key="index">
				<view class="left-icon comm-center">
					<image :src="item.leftIcon"></image>
				</view>
				<view class="txt">{{item.title}}</view>
				<view class="right-icon comm-center">
					<image src="/static/other/youjiantou.png"></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				userInfo:{},
				url: 'http://www.javanx.cn/20190222/css3-radial-gradient/',
				list:[
					{
						title:'我的鼻血',
						leftIcon:'/static/other/2.png'
					},
					{
						title:'我的眼泪',
						leftIcon:'/static/other/7.png'
					},
					{
						title:'我的便便',
						leftIcon:'/static/other/10.png'
					},
					{
						title:'我的帅气',
						leftIcon:'/static/other/1.png'
					}
				]
			}
		},
		onLoad() {
			uniCloud.callFunction({
				name:'user-center',
				data:{
					action:'get',
					id:uni.getStorageSync('uid')
				},
				success: (res) => {
					if(res.result.data.length){
						this.userInfo = res.result.data[0]
					}
				}
			})
		},
		methods: {

		}
	}
</script>

<style lang="scss" scoped>
	page {
		background-color: #f8f8f8;
	}
	.comm-content {
		width: 100%;
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
	}
	
	.comm-center{
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.head {
		height: 400rpx;
		flex-direction: column;
		background-color: #f33e54;
		color: #fbf1ef;

		image {
			width: 120rpx;
			height: 120rpx;
			border: 5rpx solid #FFFFFF;
			border-radius: 100%;
		}

		.name {
			padding-top: 30rpx;
			font-size: 35rpx;
		}

		.remarks {
			padding-top: 10rpx;
			font-size: 24rpx;
		}
	}


	.list-menu {
		background-color: #FFFFFF;

		.cell {
			display: flex;
			justify-content: space-between;
			align-items: center;
			height: 100rpx;
			border-top: 5rpx solid #f8f8f8;
 
			.left-icon {
				width: 15%;

				image {
					width: 50rpx;
					height: 50rpx;
				}
			}

			.txt {
				width: 75%;
				font-size: 26rpx;
			}

			.right-icon {
				width: 10%;

				image {
					width: 30rpx;
					height: 30rpx;
				}
			}
		}
	}
</style>
