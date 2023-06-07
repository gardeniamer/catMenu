<template>
	<view class="">
		<view class = "attentionFriend">
			<span class="friendnomi">推荐猫友:</span>   <span class="friendRefresh" @click="refresh">换一换</span>
			<scroll-view scroll-x="true" class="attentionContent" >
				<view class = "attentionItem" v-for="(item,index) in list2" :key="index">
					<view class="attentionItemIn">
						<view class="itemInUser">
							<image :src="item.photo" mode="" class="inUserPhoto"></image>
							<view class="inUserName">
									<view class = "intro">{{item.userName}}</view>
									<view class = "more">多人关注</view>	
							</view>
						</view>
						<view class="itemInCat">
							<image :src="item.photo" mode="" class="inCatPhoto"></image>
							<view class="inCatName">
								{{item.catName}}
							</view>
						</view>
						<view class="special">
							+ 关注
						</view>
					</view>
				</view>
			</scroll-view>
		</view>
		<view class="attentionDetail" v-for="(item,index) in list1" :key="index">
			<view class="detailUser">
				<view class="userInfo">
					<image :src="item.userPhoto" mode="" class="userPhoto"></image>
					<view class="userName">
						{{item.userName}}
					</view>					
				</view>

				<view class="specialMore">
					+  关注
				</view>
			</view>
			<view class="detailCat">
				<view class="catInfo">
					<image :src="item.userPhoto" mode="" class="catPhoto"></image>
					<view class="catName">
						{{item.catName}}
					</view>					
				</view>
			</view>
			<view class="catPhoto">
				<image :src="item.catPhoto" class="catImg"></image>
			</view>
		</view>
	</view>

</template>

<script>
import data from "../../data.js"
	export default {
		props:{
			moreContent:{
				type: Array
			}
		},
		
		created() {
			this.list1 = data.list5
			this.list2 = data.list6
		},
		
		data() {
			return {
				list1:[],
				list2:[],
				list3:[],
				listMore: []
			}
		},
		
		methods: {
			refresh() {
				this.list2.reverse()
			}
		},
		
		watch:{
			moreContent:{
				handler(newValue,oldValue){
				this.listMore = newValue
				this.list1 = [...this.list1, ...this.listMore]
				},
				deep:true
			}

		}
		
	}
</script>

<style>
	
	.inUserName {
		margin: 0 0 0 20rpx;
	}
	
	.more {
		text-align: left;
		color: #a9a9a9;
		font-size: 9px;
	}
	
	.intro {
		display: inline-block;
		width: 180rpx;
		text-align: left;
		font-size: 14px;
	}
	
	.friendnomi {
		display: inline-block;
		font-size: 14px;
		background-color: #ffecd2;
		padding: 5px;
		border-radius: 22px;
		transform: translate(8px,6px);
	}
	
	.friendRefresh {
		display: inline-block;
		float: right;
		font-size: 12px;
		transform: translate(-8px,10px);
		color: #a6a6a6;
	}
	
	.attentionFriend {
		width: 700rpx;
		height: 300rpx;
		margin: 30px auto 0 auto;
		background-color: #f9f9f9;
	}
	
	.attentionContent {
		width: 700rpx;
		height: 210rpx;
		display: inline-block;
		line-height: 210rpx;
		text-align: center;
		font-size: 36rpx;
		white-space: nowrap;
		transform: translateY(12px);
	}
	
	.attentionItem {
		display: inline-block;
		position: relative;
		width: 50%;
		height: 210rpx;
		line-height: 210rpx;
		text-align: center;
		font-size: 36rpx;
		border-radius: 20rpx;
		margin: 0 10px 0 10px;
		background-color: #fff;
	}
	
	.attentionItemIn {
		position: absolute;
		top: 50%;
		transform: translateY(-65%);
		width: 100%;
		height: 180rpx;
	}
	
	.itemInUser {
		width: 100%;
		height: 80rpx;
		line-height: 32rpx;
	}
	
	.inUserPhoto {
		width: 60rpx;
		height: 60rpx;
		vertical-align: middle;
		border-radius: 30px;
	}
	
	.inUserName {
		display: inline-block;
		width: 90px;
		height: 60rpx;
		font-size: 16px;
		transform: translateY(10px);
	}
	
	.itemInCat {
		margin: 0 auto;
		width: 80%;
		height: 48rpx;
		background-color: #f9f9f9;
		line-height: 40rpx;
		transform: translateY(5px);
	}
	
	.inCatPhoto {
		width: 38rpx;
		height: 38rpx;
		border-radius: 18rpx;
		vertical-align: middle;
	}
	
	.inCatName {
		display: inline-block;
		font-size: 10px;
		color: #a4a4a4;
		margin: 0 0 0 3px;
	}
	
	.special {
		margin: 0 auto;
		font-size: 14px;
		line-height: 40rpx;
		text-align: center;
		font-weight: bold;
		width: 150rpx;
		height: 40rpx;
		background-color: greenyellow;
		border-radius: 20px;
		background-color: #fec374;
		transform: translateY(30rpx);
	}
	
	.attentionDetail {
		margin:10px auto 0 auto;
		width: 700rpx;
		height: 700rpx;
		display: flex;
		flex-direction: column;
		background-color: #fff;
	}
	
	.detailUser,.detailCat {
		width: 100%;
		height: 80rpx;
	}
	
	.detailCat {
		margin: 5px auto 5px auto;
		width: 80%;
		height: 45rpx;
		background-color: #f9f9f9;
	}
	
	.catPhoto {
		flex: 1;
	}
	
	.userPhoto,.catPhoto {
		width: 60rpx;
		height: 60rpx;
		vertical-align: middle;
		border-radius: 30px;
	}
	
	.userName,.catName {
		margin: 0 0 0 10px;
		display: inline-block;
		transform: translateY(2px);
	}
	
	.specialMore {
		float: right;
		width: 160rpx;
		height: 60%;
		display: inline-block;
		text-align: center;
		line-height: 48rpx;
		border-radius: 664rpx;
		background-color: brown;
		transform: translate(-8px,16rpx);
		background-color: #fec374;
		font-weight: bold;
	}
	
	.userInfo,.catInfo {
		display: inline-block;
		width: 480rpx;
		height: 100%;
		transform: translate(10px,4px);
	}
	
	
	.catPhoto {
		width: 38rpx;
		height: 38rpx;
		transform: translateY(3rpx);
	}
	
	.catName {
		font-size: 10px;
		color: #a4a4a4;
	}
	
	.catInfo {
		width: 240rpx;
		transform: translate(10px,-2px);
	}
	
	.catImg {
		width: 700rpx;
		height: 100%;
	}
	
</style>