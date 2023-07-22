<template>

		<view class="community">
			<view class="push">
				
			</view>
			<navbar left-icon="back" right-icon="bars" backgroundColor = transparent :border = "false" @clickLeft="back" @clickRight="catList">
				<template v-slot:default>
						<view class="navWord">扫描</view>					
				</template>
			</navbar>
			<view class="scanPhoto">
				<image src="../../static/navigator/scanPhoto.png" mode=""></image>
			</view>
			<view class="exportImage">
				<view class="images" v-for = "(item,index) in list" :key="index">
					<image :src="item" mode="" 
					:class="{special2: index == 1,special3: index == 2}"
					@click = "superior(index)"></image>
				</view>
			</view>
			<view class="push2">
				
			</view>
		</view>

</template>

<script>
	import navbar from "../../uni_modules/uni-nav-bar/components/uni-nav-bar/uni-nav-bar.vue"
	export default {
		components:{
			navbar,
		},
		
		onLoad() {
			
			uni.showToast({
				icon:"none",
				title:'目前为' + this.format + '点中间切换模式'
			})

		},
		
		data() {
			return {
				list:['../../static/navigator/PhoneCamera.png',
				'../../static/navigator/mid.png',
				'../../static/navigator/PhonePhoto.png'],
				format:'存档模式',
				formatCount: 0,
				catImage:""
			}	
		},
		
		methods: {
			back() {
				uni.switchTab({
					url:'/pages/main'
				})
			},
			
			catList() {
				uni.showLoading({
					title:"加载中",
				})
				uni.request({
					method:"GET",
					url:'https://ai.ybinsure.com/s/api/getAccessToken',
					data:{
							accessKey: 'APPID_VRAuK415324F4G4r',
							accessSecret: '450e7b721fe9c4d149bafa087c490dc6'					
					},
					success: (res1) => {
						const token = res1.data.data.access_token
						uni.request({
							method:"POST",
							url:'https://ai.ybinsure.com/s/api/getPetArchivesList',
							header:{
								'content-type':'application/json'
							},
							data:{
								token:token,
							},
							success: (res2) => {
								uni.hideLoading()
								if(res2.data.status < 300) {
									if(uni.getStorageSync("catList") == '' ||
									uni.getStorageSync("catList") != res2.data.data.list) {
										uni.setStorageSync("catList",res2.data.data.list)
									}
									uni.navigateTo({
										url:"/pages/components/catList"
									})
								}
								else {
									uni.showToast({
										icon:"none",
										title: res2.data.message
									})
								}

							}
						})
					}
				})
			},
			
			superior(index) {
				if(index == 1) {
					this.format = this.format == '存档模式' ? '查询模式':'存档模式'
					uni.showToast({
						icon:"success",
						title:'目前为' + this.format
					})
				}
				
				if(index == 0) {
					if(this.format == '存档模式'){
						uni.chooseImage({
							count: 1,
							sourceType:['camera'],
							success:(res) => {
								uni.navigateTo({
									url:'/pages/components/catMsgEdit'
								})
								uni.$emit("transferEdit",res.tempFilePaths[0])
							}
						})
					}
					else if(this.format == '查询模式') {
						uni.chooseImage({
							count: 1,
							sourceType:['camera'],
							success:(res) => {
								uni.navigateTo({
									url:'/pages/components/catMsg'
								})
								uni.$emit("transfer",res.tempFilePaths[0])
							}
						})
					}
				}
				
				if(index == 2) {
					if(this.format == '存档模式'){
						uni.chooseImage({
							count: 1,
							sourceType: ['album'],
							success:(res) => {
								uni.navigateTo({
									url:'/pages/components/catMsgEdit'
								})
								uni.$emit("transferEdit",res.tempFilePaths[0])
							}
						})
					}
					
					else if(this.format == '查询模式'){
						uni.chooseImage({
							count: 1,
							sourceType: ['album'],
							success: (res) => {	
								uni.navigateTo({
									url:'/pages/components/catMsg'
								})
								uni.$emit("transfer",res.tempFilePaths[0])
							}
						})
						
					}
					
				}
				
			}
			
		}
		
	}
</script>

<style>
	* {
		margin: 0;
		padding: 0;
	}	
		
	.community {
		background-color: #f0f0f0;
		background-color: #f0f0f0;
		background-image: url("../../static/background/background.png");
		background-repeat: no-repeat;
		background-size: 100%;
		height: 1670rpx;
	}
	
	.push {
		width: 100%;
		height: 90rpx;
	}
	
	.navbar {
		width: 30px;
		height: 25px;
		transform: translate(65px,8px);
	}	
		
	.navWord {
		width: 100%;
		height: 100%;
		font-size: 20px;
		text-align: center;
		line-height: 44px;
	}
	
	.scanPhoto {
		margin: 60rpx auto 100rpx auto;
		width: 700rpx;
		height: 1000rpx;
	}
	
	.scanPhoto image {
		width: 100%;
		height: 100%;
		border-radius: 60rpx;
	}
	
	.exportImage {
		margin: 0 auto;
		width: 660rpx;
		height: 100rpx;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
		text-align: center;
		transform: translateY(-30rpx);
	}
	
	.images {
		width: 100rpx;
		height: 80%;
	}
	
	.special2 {
		width: 85rpx !important;
	}
	
	.special3 {
		width: 90rpx !important;
	}
	
	.images image {
		width: 100%;
		height: 100%;
	}
	
	.push2 {
		width: 100%;
		height: 40rpx;
	}
	
</style>