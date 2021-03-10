<template>
	<view class="index">
		11222
	</view>
</template>

<script>
	export default {
		data() {
			return {
				uid: '',
				uniLogin:true,
			}
		},
		onLoad() {
			this.uid = getApp().globalData.uid
			this.uniLogin = getApp().globalData.uniLogin
			if(!this.uid) {
				uni.redirectTo({
					url:'../login/login'
				})
			}
		}
	}
</script>

<style scoped>

</style>