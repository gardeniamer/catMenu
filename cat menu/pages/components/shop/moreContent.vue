<template>
	<view class="">
		<view class="showMsg">
			<view class="show" v-for = "(item,index) in list2" :key = "index">
				<view class="showPhoto">
					<image :src= 'item.showPhoto' mode=""></image>
				</view>
				<view class="showContent">
					<view class="msg">
						{{item.msg}}
					</view>
					<view class="advantage">
						<span v-for = "(item2,index) in item.advantage" :key="index">
						{{item2}}
						</span>	
					</view>
					<view class="price">
						<span class = "priceNow">{{item.priceNow}}</span>
						<span class = "nowPeople">{{item.nowPeople}}</span>
					</view>
				</view>
			</view>

		</view>
		<view class="finalWord" v-if="show == 0">
			-----下拉生成更多-----
		</view>
		<view class="finalWord" v-if="show == 1">
			-----没有更多了-----
		</view>
		<view class="push2">
			
		</view>
	</view>

</template>

<script>
	import data from "../../data.js"
	export default {
		
		props:{
			listMore:{
				type:Array
			}
		},
		
		created() {
			this.list2 = data.list11
		},
		
		data() {
			return {
				list2:[],
				special: 0,
				show: 0
			}
		},
		
		watch:{
			listMore:{
				handler(newValue,oldValue) {
					this.list2 = [...this.list2,...newValue]
					this.special += 1
					if(this.special == 5) {
						this.show = 1
					}
				},
				deep: true,
				immediate: true
			}
		}
		
	}
</script>

<style>
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
		margin: 0 0 10px 0;
		width: 48%;
		height: 500rpx;
		background-color: #fff;
		border-radius: 10rpx;
	}
	
	.showPhoto {
		width: 100%;
		height: 70%;
	}
	
	.showContent {
		width: 100%;
		height: 30%;
	}
	
	.msg {
		width: 100%;
		height: 50%;
		font-size: 13px;
	}
	
	.advantage {
		width: 100%;
		height: 25%;
		line-height: 35rpx;
	}
	
	.price {
		width: 100%;
		height: 25%;
		line-height: 30rpx; 
	}
	
	.advantage span {
		margin: 0 8rpx 0 8rpx;
		font-size: 10px;
		background-color: #ff0000;
		border-radius: 8rpx;
		color: #fff;
	}
	
	.price span {
		font-size: 10px;
	}
	
	.nowPeople {
		margin: 0 8rpx 0 0;
		float: right;
		color: #c7c7c7;
	}
	
	.priceNow {
		margin: 0 12rpx 0 8rpx;
		color: #f07032;
	}
	
	.special {
		border-radius: 10rpx;
		color: #f0944b;
		border: 1px solid #f0944b;
	}
	
	.finalWord {
		text-align: center;
		font-size: 12px;
		color: #b9b9b9;
	}
	
	.push2 {
		width: 100%;
		height: 40rpx;
	}
	
</style>