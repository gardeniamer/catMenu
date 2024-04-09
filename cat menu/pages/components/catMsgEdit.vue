<template>
	<view class="community">
		<view class="push">

		</view>
		<navbar left-icon="back" right-icon="bars" backgroundColor=transparent :border="false" @clickLeft="back"
			@clickRight="more">
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
				<view class="gender" v-if="index2 == 1">
					<span class="left" @click.stop="genderChange(0)">
						<image src="../../static/navigator/selectMan.png" mode="" v-show="gender == 0"></image>
						<image src="../../static/navigator/man.png" mode="" v-show="gender == 1"></image>
						公
					</span>
					<span class="right" @click.stop="genderChange(1)">
						<image src="../../static/navigator/selectWoman.png" mode="" v-show="gender == 1"></image>
						<image src="../../static/navigator/woman.png" mode="" v-show="gender == 0"></image>
						母
					</span>
				</view>
				<view class="reproduction" v-if="index2 == 4">
					<span class="left" @click.stop="controlChange(1)">
						<image src="../../static/navigator/selectYes.png" :class="{special: index2 == 4}" mode=""
							v-show="control == 1"></image>
						<image src="../../static/navigator/yes.png" :class="{special: index2 == 4}" mode=""
							v-show="control == 0"></image>
						是
					</span>
					<span class="right" @click.stop="controlChange(0)">
						<image src="../../static/navigator/selectNo.png" mode="" v-show="control == 0"></image>
						<image src="../../static/navigator/no.png" mode="" v-show="control == 1"></image>
						否
					</span>
				</view>
				<input type="text" name="" id="" v-if="index2 != 1 && index2 != 4 && index2 == 0" v-model="nickName">
				<input type="text" name="" id="" v-if="index2 != 1 && index2 != 4 && index2 == 2" v-model="monster">
				<input type="text" name="" id="" v-if="index2 != 1 && index2 != 4 && index2 == 3" v-model="dateOfBirth">
				<input type="text" name="" id="" v-if="index2 != 1 && index2 != 4 && index2 == 5" v-model="disease">
				<input type="text" name="" id="" v-if="index2 != 1 && index2 != 4 && index2 == 6" v-model="vaccine">
			</span>
		</view>
		<view class="finish" @click.stop="finished">
			确认存档
		</view>
		<view class="push2">

		</view>
	</view>
</template>

<script>
	import navbar from "../../uni_modules/uni-nav-bar/components/uni-nav-bar/uni-nav-bar.vue"
	import {
		pathToBase64,
		base64ToPath
	} from '../../js_sdk/mmmm-image-tools/index.js'
	export default {

		components: {
			navbar,
		},

		data() {
			return {
				catImg: "",
				catImgReal: "",
				list: [
					'姓名', '性别', '主人', '出生日期', '绝育', '过往病例', '疫苗'
				],
				list2: {
					nickName: "",
					gender: "",
					monster: "",
					dateOfBirth: "",
					birthControlStatus: "",
					disease: "",
					vaccine: ""
				},
				gender: 0,
				control: 1,
				count: 0,
				nickName: "",
				monster: "",
				dateOfBirth: "",
				disease: "",
				vaccine: "",
				token: ""
			}
		},

		onLoad() {
			uni.showLoading({
				title: "加载中",
				icon: "none"
			})

			uni.$on("transferEdit", (i) => {
				this.catImg = i
				pathToBase64(i).then(i => {
					this.catImgReal = i
					if (this.catImgReal != "") {
						uni.hideLoading()
					}
				}).catch(err => {
					console.log(err);
				})
			})

		},

		methods: {
			back() {
				uni.navigateBack()
			},

			genderChange(index) {
				this.gender = index
			},

			controlChange(index) {
				this.control = index
			},

			finished() {
				this.list2.nickName = this.nickName
				this.list2.monster = this.monster
				this.list2.dateOfBirth = this.dateOfBirth
				this.list2.disease = this.disease
				this.list2.vaccine = this.vaccine
				for (let value in this.list2) {
					console.log(this.list2[value]);
					if (this.list2[value] == "" && value != "gender" && value != "birthControlStatus") {
						uni.showToast({
							icon: 'error',
							title: '请填写完整信息'
						})
						this.count++
						break
					}
				}
				if (this.count == 0) {
					uni.showLoading({
						title: "加载中",
						icon: "none"
					})
					if (uni.getStorageSync("petKind") == 1) {
						const petStore = new Promise((resolve, reject) => {
							uni.request({
								method: "POST",
								url: 'https://api.shuzike.com/lifeservice/check2/102',
								header: {
									'Content-Type': 'application/json',
									'UserAuthKey': '7840de5c-7220-470e-be5e-836198da6f231209'
								},
								data: {
									imageBase64: this.catImgReal.split(",")[1],
									nickname: this.list2.nickName,
									petId: "",
									groupId: "",
									petDbId: "",
									isVerification: "",
									gender: String(this.gender),
									dateOfBirth: this.list2.dateOfBirth,
									birthControlStatus: String(this.control),
									mark: 'monster' + ":" + this.list2.monster + "," +
										"disease" + ":" + this.list2.disease + "," +
										"vaccine" + ":" + this.list2.vaccine
								},
								success: (res) => {
									uni.hideLoading()
									if (res.data.msg == "成功") {
										let obj = uni.getStorageSync("petMsg")
										obj[res.data.data.result.petId] = {
											images:[{
												url: this.catImg
											}],
											nickname: this.list2.nickName,
											gender: this.gender,
											dateOfBirth: this.list2.dateOfBirth,
											birthControlStatus: this.control,
											mark: 'monster' + ":" + this.list2.monster + "," +
												"disease" + ":" + this.list2.disease + "," +
												"vaccine" + ":" + this.list2.vaccine
										}
										uni.setStorageSync("petMsg", obj)
										resolve()
									} else {
										reject(res.data.msg)
									}
								}
							})
						})
						petStore.then((value) => {
								uni.showToast({
									icon: 'success',
									title: '存储成功'
								})
								setTimeout(() => {
									uni.navigateBack()
								}, 1600)
							})
							.catch((rea) => {
								uni.showToast({
									icon: "none",
									title: rea
								})
								setTimeout(() => {
									uni.navigateBack()
								}, 1600)
							})

					}
					if (uni.getStorageSync("petKind") == 0) {
						const petStore = new Promise((resolve, reject) => {
							uni.request({
								method: "POST",
								url: 'https://api.shuzike.com/lifeservice/check2/115',
								header: {
									'content-type': 'application/json',
									'UserAuthKey': '7840de5c-7220-470e-be5e-836198da6f231209'
								},
								data: {
									imageBase64: this.catImgReal.split(",")[1],
									nickname: this.list2.nickName,
									petId: "",
									groupId: "",
									petDbId: "",
									isVerification: "",
									gender: String(this.gender),
									dateOfBirth: this.list2.dateOfBirth,
									birthControlStatus: String(this.control),
									mark: 'monster' + ":" + this.list2.monster + "," +
										"disease" + ":" + this.list2.disease + "," +
										"vaccine" + ":" + this.list2.vaccine
								},
								success: (res) => {
									uni.hideLoading()
									if (res.data.msg == "成功") {
										let obj = uni.getStorageSync("petMsg")
										obj[res.data.data.result.petId] = {
											images:[{
												url: this.catImg
											}],
											nickname: this.list2.nickName,
											gender: this.gender,
											dateOfBirth: this.list2.dateOfBirth,
											birthControlStatus: this.control,
											mark: 'monster' + ":" + this.list2.monster + "," +
												"disease" + ":" + this.list2.disease + "," +
												"vaccine" + ":" + this.list2.vaccine
										}
										uni.setStorageSync("petMsg", obj)
										resolve()
									} else {
										reject(res.data.msg)
									}
								}
							})
						})
						petStore.then((value) => {
								uni.showToast({
									icon: 'success',
									title: '存储成功'
								})
								setTimeout(() => {
									uni.navigateBack()
								}, 1600)
							})
							.catch((rea) => {
								uni.showToast({
									icon: "none",
									title: rea
								})
								setTimeout(() => {
									uni.navigateBack()
								}, 1600)
							})
					}
				} else {
					this.count = 0
				}
			}

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
		transform: translate(65px, 8px);
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
		transform: translate(-8rpx, 8rpx)
	}

	.contentInput input {
		height: 70rpx;
		transform: translateY(14rpx);
	}

	.left {
		width: 100rpx;
		height: 80rpx;
		display: inline-block;
		transform: translateX(-60rpx);
	}

	.right {
		width: 100rpx;
		height: 80rpx;
		display: inline-block;
		transform: translateX(60rpx);
	}

	.special {
		width: 50rpx !important;
	}

	.finish {
		margin: 0 auto;
		width: 600rpx;
		height: 100rpx;
		background-color: #ffecd2;
		text-align: center;
		line-height: 100rpx;
		border-radius: 100rpx;
	}

	.push2 {
		width: 100%;
		height: 60rpx;
	}
</style>