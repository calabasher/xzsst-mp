<template>
	<view>
		<van-cell-group>
		  <van-cell is-link title="个人简介" @click="navTo('/pages/setting/profile')" :value="userInfo.profile"></van-cell>
		  <view class="border-bottom">
			    <button open-type='contact' class="font-14 tleft white-bg pdt5 pdb5 flex-space-between">
					<text>联系客服</text><van-icon name="arrow" class="dy-font-color font-16" />
			    </button>
			</view>
		  <!-- <van-cell is-link title="用户须知" @click="navTo(url)" url="/pages/dashboard/index" /> -->
		</van-cell-group>
	</view>
</template>

<script>
	export default {
		components: {
		},
		data() {
			return {
				userInfo: {},	// 用户信息
			}
		},
		// 监听页面卸载， 监听页面的卸载， 当前处于A页面，点击返回按钮时，则将是A页面卸载、
		onUnload() {
		    this.imageList = []
		},
		onReady(){
		},
		onLoad(){
		},
		onShow(){
			let that = this;
			uni.getStorage({
			    key: 'userInfo',
			    success: function (res) {
					that.userInfo = res.data;
					that.userInfo.profile = that.userInfo.profile.length === 0 ? '未设置，设置一下吧' : that.userInfo.profile.length > 10 ? that.userInfo.profile.slice(0, 10) : that.userInfo.profile
			    }
			});
		},
		// 监听页面的隐藏,当从当前A页跳转到其他页面，那么A页面处于隐藏状态。
		onHide(){
		},
		methods: {
			navTo(url){
				uni.navigateTo({ url: url })
			},
			// 获取用户信息
			getUserInfo(){
				let that = this;
				const query = that.Bmob.Query('_User');
				query.get(that.myObjectId).then(res => {
					console.log('sd')
				  }).catch(err => {
					console.log(err)
				  })
			},
		},
		// watch: {
		// 	columnsNum(value) {
		// 	    this.set({
		// 	        displayColumns: this.data.columns.slice(0, +value)
		// 	    });
		// 	}
		// }
	}
</script>

<style>

</style>
