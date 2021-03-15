<template>
	<view class="index">
		<view className="article">
			<view className="wrap">
				<view className="title">
					<text className="title">快快快</text>
				</view>
				<view className="content">

					<view className="time">
						<text>发布时间:</text>
						<text style="margin-left:20rpx">20202</text>
					</view>

					<view className="info">
						<view className="preview">
							<!-- <AtIcon value='eye' size='20'></AtIcon> -->
							<text className="number">3</text>
						</view>
						<view className="collection" >
							<!-- <AtIcon value='heart' size='20'></AtIcon> -->
							<text className="number">55</text>
						</view>
					</view>

					<view className="img">
						<image
							src="https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2977303835,4064798147&fm=11&gp=0.jpg">
						</image>
					</view>

					<view className="type">
						<!-- <AtIcon value='image' size='20'></AtIcon> -->
						<text className="title1">xxqeq</text>
					</view>

				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				uid: '',
				uniLogin: true,
			}
		},
		onLoad() {
			this.uid = getApp().globalData.uid
			this.uniLogin = getApp().globalData.uniLogin
			// if (!this.uid) {
			// 	uni.redirectTo({
			// 		url: '../login/login'
			// 	})
			// }
		}
	}
</script>

<style scoped lang="scss">
	.article {
		width: 100vw;
		padding: 30rpx;
		box-sizing: border-box;

		.wrap {
			color: #ccc;
			margin-bottom: 20rpx;

			.img {
				width: 100%;

				>image {
					width: 100%;
				}
			}

			.title {
				font-weight: 600;
				margin-bottom: 20rpx;
				color: #444;
			}

			.info {
				display: flex;
				align-items: center;
				margin: 20rpx 0;
				.preview {
					margin-right: 30rpx;
				}

				.number {
					margin-left: 10rpx;
				}
			}

			.type {
				margin-top: 20rpx;

				>.title1 {
					margin-left: 20rpx;
					color: #ccc;
				}
			}
		}
	}
</style>
