<template>
	<view class="">
		<view class="title">
			精选:
		</view>
		<view class="contentChoose">
			<view class="allchoices" v-for="(item,index) in list" :key="index">
				<image :src="item.choosePhoto" mode="" :class="{special: item.chooseWord == '交流天地'}"></image>
				<view class="chooseWord">
					{{item.chooseWord}}
				</view>
			</view>
		</view>
		<view class="moreContent">
			<view class="userMsg" v-for="(item,index) in list2" :key="index">
				<image :src="item.findPhoto" mode="" class = "usersPhoto"></image>
				<view class="introduce">
					<span class = "summary">{{item.findContentOne}}</span>
					<span class = "replenish">{{item.findContentTwo}}</span>	
					<span class="findSpecial">
						+ 关注
					</span>					
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import data from "../../data.js"
	export default {
		created() {
			this.list2 = data.list7
		},
		
		data() {
			return {
				list:[{
					choosePhoto:'../../../static/talks/daily.png',
					chooseWord:'日常分享'
				},
				{
					choosePhoto:'../../../static/talks/konwledge.png',
					chooseWord:'知识普及'
				},
				{
					choosePhoto:'../../../static/talks/findTalk.png',
					chooseWord:'交流天地'
				}],
				
				list2:[]
				
			}
		}
	}
</script>

<style>
	.title {
		width: 150rpx;
		height: 60rpx;
		text-align: center;
		line-height: 60rpx;
		background-color: #ffecd2;
		border-radius: 60rpx;
		transform: translateX(15px);
	}
	
	.contentChoose {
		margin: 6px auto 6px auto;
		width: 700rpx;
		height: 180rpx;
		background-color: #ffffff;
		border-radius: 40rpx;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
	}
	
	.allchoices {
		width: 180rpx;
		height: 100%;
	}
	
	.allchoices image {
		width: 100rpx;
		height: 100rpx;
		transform: translate(38rpx,10rpx);
	}
	
	.knowIcon {
		transform: translate(22px,5px);
	}
	
	.talkIcon {
		width: 60px;
		transform: translate(16px,7px);
	}
	
	.chooseWord {
		text-align: center;
		transform: translateY(10px);
		font-family: STCaiyun;
		color: #fbd48f;
	}
	
	.moreContent {
		width: 700rpx;
		margin: 0 auto;
		border-top: 0.1px solid transparent;
		background-color: #fff;
	}
	
	.userMsg {
		margin: 10px auto 0 auto;
		width: 660rpx;
		height: 180rpx;
		border-bottom: 1px solid #A9A9A9;
	}
	
	.usersPhoto {
		width: 50px;
		height: 50px;
		transform: translate(16px,16px);
		border-radius: 10px;
		vertical-align: middle;
	}
	
	.introduce {
		width: 500rpx;
		transform: translate(75px,-30px);
	}
	
	.summary {
		font-weight: bold;
	}
	
	.replenish {
		display: block;
		font-size: 12px;
		color: #A9A9A9;
		margin: 5px 0 0 0;
	}
	
	.findSpecial {
		float: right;
		width: 140rpx;
		height: 50rpx;
		text-align: center;
		line-height: 50rpx;
		background-color: #fec374;
		border-radius: 60rpx;
		transform: translateY(-70rpx);
		font-weight: 600;
	}
	
	.special {
		width: 120rpx !important;
		transform: translate(30rpx,10rpx) !important;
	}
	
</style>