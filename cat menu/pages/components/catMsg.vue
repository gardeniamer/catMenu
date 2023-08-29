<template>
	<view class="community">
		<view class="push">
			
		</view>
		<navbar left-icon="back" right-icon="bars" backgroundColor = transparent :border = "false" @clickLeft="back" @clickRight="more">
			<template v-slot:default>
					<view class="navWord">扫描</view>					
			</template>
		</navbar>
		<view class="catImage">
			<image :src="catImg" mode=""></image>
		</view>
		<view class="catContent" v-for="(item,index) in list" :key="index">
			<view class="content">
				{{item}}
			</view>
			<span class="contentInput" v-for="(value,name,index2) in list2" :key="name" v-if="index2 == index">
				<image src="../../static/navigator/selectMan.png" mode="" v-if = "index2 == 1 && value == '公'"></image>
				<image src="../../static/navigator/selectWoman.png" mode="" v-if = "index2 == 1 && value == '母'"></image>
				<image src="../../static/navigator/selectYes.png" :class="{special: index2 == 4}" mode="" v-if = "index2 == 4 && value == '是'"></image>
				<image src="../../static/navigator/selectNo.png" mode="" v-if = "index2 == 4 && value == '否'"></image>
				{{value}}
			</span>
		</view>
		<view class="push2">
			
		</view>
	</view>
</template>

<script>
	import navbar from "../../uni_modules/uni-nav-bar/components/uni-nav-bar/uni-nav-bar.vue"
	import { pathToBase64, base64ToPath } from '../../js_sdk/mmmm-image-tools/index.js'
	export default {
		components: {
			navbar,
		},
		
		data() {
			return {
				catImg:"",
				catImgReal:"",
				list:[
					'姓名','性别','主人','出生日期','绝育','过往病例','疫苗'
					],
				list2:{
					nickName:'',
					gender:'',
					monster:'',
					dateOfBirth:'',
					birthControlStatus:'',
					disease:'',
					vaccine:''
				},
				token:"",
				petId:""
			}
		},
		
		onLoad(){
			uni.$on("transfer", (i)=>{
				this.catImg = i
				pathToBase64(i).then(i=>{
					this.catImgReal = i
				})
				.catch(err=>{
					console.log(err);
				})
				})
				setTimeout(()=>{
					this.pet()
				},200)
				
		},
		
		methods: {
			back() {
				uni.navigateBack()
			},
			
			pet() {
				uni.showLoading({
					title: '加载中'
				})
				setTimeout(()=>{
					(async function(){
						try {
							await catGet
						}catch(e){
							uni.hideLoading()
							uni.showToast({
								icon:"none",
								title: e
							})
							uni.navigateBack()
						}
					})()
				},1200)
				
				
				const catGet = new Promise((resolve, reject)=>{
					uni.request({
						method:"GET",
						url:'https://ai.ybinsure.com/s/api/getAccessToken',
						data:{
							accessKey: 'APPID_VRAuK415324F4G4r',
							accessSecret: '450e7b721fe9c4d149bafa087c490dc6'					
						},
						success: (res) => {
							if(res.data.status < 300) {
								this.token = res.data.data.access_token
								uni.request({
									method:"POST",
									url:'https://ai.ybinsure.com/s/api/uploadPetImageFindPeytId',
									header:{
										'content-type':'application/x-www-form-urlencoded'
										},
									data:{
										token: this.token,
										imageBase64:this.catImgReal,
										petType: 1,
										recogType: 1,
										},
									success: (res2) => {
										if (res2.data.status < 300) {
											this.petId = res2.data.data.petIds[0]
											uni.request({
												method:"POST",
												url:'https://ai.ybinsure.com/s/api/getPetArchivesList',
												header:{
													'content-type':'application/json'
													},
												data:{
													token:this.token,
													petId:this.petId
												},
												success: (res3) => {
													if(res3.data.status < 300) {
														uni.hideLoading()
														uni.showToast({
															title:"加载成功"
														})
														const data = res3.data.data.list[0]
														this.list2.nickName = data.nickname	
														if(data.gender == 1){
															this.list2.gender = '母'
															}
														else if(data.gender == 0){
															this.list2.gender = '公'
															}
														this.list2.dateOfBirth = data.dateOfBirth
														if(data.birthControlStatus == 1){
															this.list2.birthControlStatus = '是'
															}
														else if(data.birthControlStatus == 0){
															this.list2.birthControlStatus = '否'
															}									
														for(let vol of data.mark.split(",")) {
															if(vol.split(":")[0] == "monster"){
																this.list2.monster = vol.split(":")[1]
																}
															else if(vol.split(":")[0] == "disease"){
																this.list2.disease = vol.split(":")[1]
																}
															else if(vol.split(":")[0] == "vaccine"){
																this.list2.vaccine = vol.split(":")[1]
																}
														}
														resolve()
													}
													else {
														reject(res3.data.message)
													}
												}
											})
										}
										else {
											reject(res2.data.message)
										}
									}
								})
							}
							else {
								reject(res1.data.message)
							}
						}
					})
				})
				
			},
		},
		
	}
</script>

<style>
	* {
		margin: 0;
		padding: 0;
	}	
		
	.community {
		background-color: #f0f0f0;
		background-image: url("../../static/background/background.png");
		background-repeat: no-repeat;
		background-size: 70%;
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
	
	.catImage {
		margin: 60rpx auto 100rpx auto;
		width: 500rpx;
		height: 600rpx;
	}
	
	.catImage image {
		width: 100%;
		height: 100%;
	}
	
	.catContent {
		margin: 0 auto 40rpx auto;
		width: 600rpx;
		height: 100rpx;
		line-height: 100rpx;
	}
	
	.content {
		display: inline-block;
		width: 150rpx;
		height: 60rpx;
		line-height: 60rpx;
		background-color: #ffecd2;
		border-radius: 40rpx;
		text-align: center;
		font-size: 15px;
	}
	
	.contentInput {
		display: inline-block;
		width: 354rpx;
		height: 80rpx;
		border-bottom: 2px dashed #000000;
		transform: translateX(15rpx);
		text-align: center;
	}
	
	.contentInput image {
		width: 40rpx;
		height: 40rpx;
		transform: translate(-8rpx,8rpx)
	}
	
	.special {
		width: 50rpx !important;
	}
	
	.push2 {
		width: 100%;
		height: 20rpx;
	}
	
</style>