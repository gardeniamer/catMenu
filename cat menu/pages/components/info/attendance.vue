	<template>
		<view class="community">
			<view class="push">
				
			</view>
			<view class="">
			<navbar left-icon = "back" backgroundColor = transparent :border = "false" @clickLeft="back">
				<template v-slot:default>
						<image src="../../../static/navigator/calendar.png" mode="" class="infoNav"></image>
						<view  class="navWord">喂猫打卡</view>					
				</template>
			</navbar>
			<uni-calendar :lunar= "true" 
			:showMonth="false"
			:selected="selected"
			:startDate="'1999-3-20'"
			@change="change">
			</uni-calendar>
		</view>
			<view class="clock">
				<view class="decoration"></view>
				<view class="real">
					<view class="decoration"></view>
					<view class="content">
						<view class="fill">
							<view class="inputContent" v-for="(item,index) in list" :key="index">
								<image :src="item" mode=""></image>
								<input type="text" name="" id="" placeholder="请填写" v-model="list2.inputCon" v-if="index == 0">
								<input type="text" name="" id="" placeholder="请填写" v-if="index != 0">
							</view>
						</view>
						<view class="icon">
							<view class="iconContent" v-if = "judge == false">
								待完成
							</view>
							<view class="iconContent" v-else>
								已完成
							</view>
							<view class="iconContent2" @click.stop="clock">
								打卡
							</view>
							<view class="iconContent3" @click.stop="record">
								标记
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>


	</template>

	<script>
	import navbar from "../../../uni_modules/uni-nav-bar/components/uni-nav-bar/uni-nav-bar.vue"
	import calendar from "../../../uni_modules/uni-calendar/components/uni-calendar/uni-calendar.vue"

	function getDate(date, AddDayCount = 0) {
		if (!date) {
			date = new Date();
		}
		if (typeof date !== 'object') {
			date = date.replace(/-/g, '/');
		}
		const dd = new Date(date);

		dd.setDate(dd.getDate() + AddDayCount); // 获取AddDayCount天后的日期

		const y = dd.getFullYear();
		const m = dd.getMonth() + 1 < 10 ? '0' + (dd.getMonth() + 1) : dd.getMonth() + 1; // 获取当前月份的日期，不足10补0
		const d = dd.getDate() < 10 ? '0' + dd.getDate() : dd.getDate(); // 获取当前几号，不足10补0
		return {
			fullDate: y + '-' + m + '-' + d,
			year: y,
			month: m,
			date: d,
			day: dd.getDay()
		};
	}
	export default {
		components: {
			navbar
		},
		
		data() {
			return {
				selected:[
					{date:"2023.6.13",info:'签到'},
				],
				data:'',
				list:[
					'../../../static/info/attendance1.png',
					'../../../static/info/attendance2.png',
					'../../../static/info/attendance3.png'
				],
				judge: false,
				list2:{
					inputCon:"",
					inputLo:"",
					inputCat:""
				}
			}
		},
		
		onLoad() {
			let year
			let month
			let day
			year = new Date().getFullYear()
			if( (new Date().getMonth() + 1 ) <= 9) {
				month = '0' + (new Date().getMonth() + 1)
			}
			else {
				month = new Date().getMonth() + 1
			}
			day = new Date().getDate()
			let all
			all = year + '-' + month + '-' + day
			this.data = all
		},
		
		methods: {
			back() {
				uni.switchTab({
					url:'/pages/components/info'
				})
			},
			
			change(e) {
				this.data = e.fulldate
			},
			
			
			clock() {
				if(this.list2.inputCon != "") {
				if(this.list2.inputCon == new Date().getFullYear()+'.'+ (new Date().getMonth() + 1)+'.'+ new Date().getDate()){
					if(this.selected[this.selected.length-1].date == new Date().getFullYear()+'.'+ (new Date().getMonth() + 1)+'.'+ new Date().getDate()){
						this.selected.pop()
					}
					
						this.selected.push({date:this.list2.inputCon,info:'签到'})
						this.list2.inputCon = ""
						this.judge=true
					}
					else {
						uni.showToast({
							icon:"none",
							title:"打卡仅允许今天(以格式2019.1.1输入)"
						})
					}				
				}
				
				else {
					if(this.data.split("-")[2] != new Date().getDate()){
						uni.showToast({
							icon:"none",
							title:"打卡仅允许今天"
						})
					}
					else {
						if(this.selected[this.selected.length-1].info == "标记"){
							this.selected.pop()
						}
						if(this.judge != true) {
							this.selected.push({date:this.data,info:"签到"})
							uni.showToast({
								icon:"none",
								title:"打卡成功"
							})
							this.judge=true
						}
					}
				}
						
			},
			
			record() {
				if(this.list2.inputCon != "") {
					if(this.list2.inputCon.split(".").length==3){
						this.selected.push({date:this.list2.inputCon,info:"标记"})
						this.list2.inputCon = ""
						uni.showToast({
							icon:"none",
							title:"标记成功"
						})
					}
					else {
						uni.showToast({
							icon:"none",
							title:"(请以格式2019.1.1输入)"
						})
					}
				}
				else {
					if(this.selected[this.selected.length-1].date != this.data){
						this.selected.push({date:this.data,info:"标记"})
						uni.showToast({
							icon:"none",
							title:"标记成功"
						})
					}

				}
			}
			
		}
		
	}
	</script>

	<style>
	.community {
		background-color: #f0f0f0;
		background-image: url("../../../static/background/background.png");
		background-repeat: no-repeat;
		background-size: 60%;
	}

	.push {
		width: 100%;
		height: 90rpx;
	}	

	.infoNav {
			width: 30px;
			height: 25px;
			transform: translate(35px,8px);
		}

	.navWord {
		width: 100%;
		height: 100%;
		font-size: 20px;
		text-align: center;
		line-height: 44px;
	}

	.clock {
		margin: 10px auto 0 auto;
		width: 700rpx;
		height: 800rpx;
		background-color: #93d4be;
		border-top-left-radius: 100rpx;
		border-top-right-radius: 100rpx;
		border-top: 1px solid transparent;
	}

	.decoration {
		margin: 15px auto 0 auto;
		width: 200rpx;
		height: 20rpx;
		background-color: #fff;
		border-radius: 20rpx;
	}

	.real {
		margin: 25px auto 0 auto;
		width: 700rpx;
		height: 700rpx;
		background-color: #fff5e9;
		border-top-left-radius: 100rpx;
		border-top-right-radius: 100rpx;
		border-top: 1px solid transparent;
	}

	.real .decoration {
		background-color: #94d7be;
	}

	.content {
		margin: 20px auto 0 auto;
		width: 90%;
		height: 600rpx;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
	}

	.fill {
		height: 100%;
		width: 75%;
		display: flex;
		flex-direction: column;
		justify-content: space-around;
		align-items: center;
	}

	.inputContent {
		width: 90%;
		height: 20%;
		line-height: 150rpx;
	}

	.inputContent image {
		width: 35px;
		height: 35px;
		vertical-align: text-bottom;	
	}

	.inputContent input {
		display: inline-block;
		width: 320rpx;
		height: 50rpx;
		transform: translateX(10px);
		border-bottom: 2px dashed #000000;
	}

	.icon {
		height: 100%;
		width: 25%;
	}

	.iconContent,.iconContent2,.iconContent3 {
		width: 100%;
		height: 10%;
		line-height: 60rpx;
		text-align: center;
		border-radius: 30rpx;
		background-color: #f9d48e;
		font-weight: bold;
	}

	/* .iconContent {
		margin: 80rpx 0 0 0;
	} */

	.iconContent2 {
		margin: 60rpx 0 0 0;
	}

	.iconContent3 {
		margin: 60rpx 0 0 0;
	}

	</style>