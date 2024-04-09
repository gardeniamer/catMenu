<template>
	<view class="community">
		<view class="push">
			
		</view>
		<navbar left-icon="back" right-icon="" backgroundColor = transparent :border = "false" @clickLeft="back">
			<template v-slot:default>
				<image src="../../static/navigator/neiko.png" mode="" class="navbar"></image>
					<view class="navWord">宠物列表</view>					
			</template>
		</navbar>
		<view class="showMsg">
			<view class="show" v-for = "(item,index) in list" :key = "index">
				<view class="showPhoto">
					<image :src= 'item.images[0].url' mode=""></image>
				</view>
				<view class="showContent">
					<view class="catMsg">
						姓名：{{item.nickname}}
					</view>
					<view class="catMsg">
						性别：{{item.gender == 1?'母':'公'}}
					</view>
					<view class="catMsg" v-if="(item.mark.split(',')[0].split(':')[1].length <= 6)">
						所属对象：{{item.mark.split(",")[0].split(":")[1]}}
					</view>
					<view class="catMsg" v-if="(item.mark.split(',')[0].split(':')[1].length > 6)">
						所属对象：{{item.mark.split(",")[0].split(":")[1].slice(0,5)}}...
					</view>
				</view>
			</view>
		
		</view>
	</view>
</template>

<script>
	import navbar from "../../uni_modules/uni-nav-bar/components/uni-nav-bar/uni-nav-bar.vue"
	export default {
		components: {
			navbar
		},
		
		created() {
			this.list = uni.getStorageSync("catList")
			this.list = [...this.list,...this.list2]
		},
		
		data() {
			return {
				list:[],
				list2:[
				{
					nickname:"吉吉",
					gender: 0,
					mark:"monster:晋中学院,disease:无,vaccine:未打疫苗",
					images:[{
						url:"https://ts1.cn.mm.bing.net/th/id/R-C.847aa902d6d8232f64304cc97bf26b79?rik=ZQJd5lE%2fBQlOPg&riu=http%3a%2f%2fpic.zsucai.com%2ffiles%2f2013%2f0910%2fggxm6.jpg&ehk=p9rXNok%2f8LIKSFZsRZdzeBYaP5cpFzNqr4hXIAuTPg8%3d&risl=&pid=ImgRaw&r=0"
					},]
				},
				{
					nickname:"毛毛",
					gender: 1,
					mark:"monster:太原师范大学,disease:无,vaccine:未打疫苗",
					images:[{
						url:"https://desk-fd.zol-img.com.cn/t_s960x600c5/g5/M00/06/08/ChMkJlZXu1SIYdyGAAMg2QRtIk8AAFZagH3kcEAAyDx571.jpg"
					},]
				},
				{
					nickname:"小雪",
					gender: 1,
					mark:"monster:山西中医药大学,disease:无,vaccine:未打疫苗",
					images:[{
						url:"https://img.zcool.cn/community/01c57f5d391760a8012187f4e52b95.jpg@1280w_1l_2o_100sh.jpg"
					},]
				},
				{
					nickname:"小白",
					gender: 0,
					mark:"monster:山西传媒学院,disease:无,vaccine:未打疫苗",
					images:[{
						url:"https://ts1.cn.mm.bing.net/th/id/R-C.df3a265f0f7478438b29d723f7c7eb43?rik=1zIQHOZvgq6zdQ&riu=http%3a%2f%2fimg.crcz.com%2fallimg%2f201910%2f26%2f1572070977102312.jpg&ehk=9xFcb4W0%2bUDVk5Gk2z2K5TwPC4AIEYeSbHqEpreO8P8%3d&risl=&pid=ImgRaw&r=0&sres=1&sresct=1"
					},]
				},
				{
					nickname:"小乐",
					gender: 0,
					mark:"monster:山西能源学院,disease:无,vaccine:未打疫苗",
					images:[{
						url:"https://img.zcool.cn/community/01570a5d390482a8012187f478c722.jpg@1280w_1l_2o_100sh.jpg"
					},]
				},
				{
					nickname:"小橘子",
					gender: 1,
					mark:"monster:山西卫生健康职业学院,disease:无,vaccine:未打疫苗",
					images:[{
						url:"https://ts1.cn.mm.bing.net/th/id/R-C.cf9cd3022164820cca8c99fcad1f60d7?rik=8q8%2fUjHt0%2foViA&riu=http%3a%2f%2fwww.quazero.com%2fuploads%2fallimg%2f140228%2f1-14022QA428.jpg&ehk=rsN5YCMWLKzBg4lvBhtz7iqlFC30TLnBNKG3F1ilN2c%3d&risl=&pid=ImgRaw&r=0"
					},]
				},
				{
					nickname:"小灰灰",
					gender: 0,
					mark:"monster:山西财经大学,disease:无,vaccine:未打疫苗",
					images:[{
						url:"https://tse1-mm.cn.bing.net/th/id/OIP-C.VG-v3VEdHT2iquPU5F6RgwHaEo?pid=ImgDet&rs=1"
					},]
				},
				{
					nickname:"花纹哥",
					gender: 0,
					mark:"monster:晋中学院,disease:无,vaccine:未打疫苗",
					images:[{
						url:"https://ts1.cn.mm.bing.net/th/id/R-C.d8d3fb8173451c8e6fb38f62e4a6b881?rik=yRDHM5uTlLMA0w&riu=http%3a%2f%2fup.kukudesk.com%2fpic%2f8f%2ffe%2ff8%2f8ffef805271a29149918120b822b0bb6.jpg&ehk=i%2f6U1EUAqIE80DzgC9tyMdTcYlWBSbmBHYXKzYclS3g%3d&risl=&pid=ImgRaw&r=0"
					},]
				}
				]
			}
		},
		
		methods: {
			back() {
				uni.navigateBack()
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
	}
	
	.push {
		width: 100%;
		height: 90rpx;
	}
	
	.navbar {
		width: 30px;
		height: 25px;
		transform: translate(100rpx,16rpx);
	}	
		
	.navWord {
		width: 100%;
		height: 100%;
		font-size: 20px;
		text-align: center;
		line-height: 44px;
	}
	
	.showMsg {
		margin: 0 auto;
		width: 700rpx;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		flex-wrap: wrap;
		background-color: #fff;
		background-color: #f0f0f0;
	}
	
	.showPhoto image {
		width: 100%;
		height: 100%;
		border-top-left-radius: 10rpx;
		border-top-right-radius: 10rpx;
	}
	
	.show {
		margin: 20rpx 0 20rpx 0;
		width: 48%;
		height: 500rpx;
		background-color: #fff;
		border-radius: 10rpx;
	}
	
	.showPhoto {
		width: 100%;
		height: 60%;
	}
	
	.showContent {
		width: 100%;
		height: 40%;
	}
	
	.catMsg {
		margin: 20rpx 0 20rpx 0;
		font-weight: bold;
		transform: translateX(20rpx);
		font-size: 14px;
	}
	
</style>