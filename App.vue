<script>
	export default {
		onLaunch: function() {
			uniCloud.callFunction({
				name:'user-center',
				data:{
					action:'checkToken'
				},
				success: (res) => {
					console.log(res,'res')
					if(!res.result.uid){
						return false
					}
					setTimeout(()=>{
						getApp().globalData.uid = res.result.uid
						getApp().globalData.uniLogin = false
					},30)	
				}
			})
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		},
		globalData:{
			uid:'',//用户id
			uniLogin:true,//用户是否登陆 true 需要登陆
		}
	}
</script>

<style>
	/*每个页面公共css */
</style>
