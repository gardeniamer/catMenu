<template>
	<view class="allContent">
		<view class="vipAll">
		<view class="comboDetail" 
		v-for = "(item,index) in list" :key = "index"
		:class="{active: index == choice}"
		@click="choose(index)">
			{{item}}
		<view class = "moreChoice"></view>
		</view>
		</view>
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
						<span class = "special">会员价</span>
						<span class = "priceBefore">{{item.priceBefore}}</span>
					</view>
				</view>
			</view>
		</view>
		<view class="finalWord">
			-----没有更多了-----
		</view>
		<view class="push2">
			
		</view>
	</view>

</template>

<script>
	import data from "../../data.js"
	export default {
		created() {
			this.list2 = data.list10
		},
		
		data() {
			return {
				list:['品种','会员福利','品牌'],
				choice: 1,
				list2:[]
			}
		},
		
		methods: {
			choose(index) {
				this.choice = index
				if(index == 1) {
					this.list2 = data.list10
				}
				else if(index == 0) {
					this.list2 = data.listMore2[0]
				}
				else {
					this.list2 = data.listMore2[1]
				}
			}
		}
		
	}
</script>

<style>
	
	.allContent {
		background-color: #fff;
	}
	
	.showPhoto image {
		width: 100%;
		height: 100%;
	}
	
/* 	.specialImage {
		height: 90% !important;
		transform: translateY(15rpx);
	} */
	
	.vipAll {
		margin: 0 auto 10px auto;
		width: 700rpx;
		height: 120rpx;
		border-radius: 40rpx;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
	}
	
	.comboDetail {
		width: 25%;
		height: 100%;
		text-align: center;
		line-height: 120rpx;
	}
	
	.moreChoice {
		display: inline-block;
		width: 10px;
		height: 10px;
		border-right: 1.5px solid #c7c7c7;
		border-bottom: 1.5px solid #c7c7c7;
		transform:translate(8px,-2px) rotate(45deg);
	}
	
	.active {
		color: #9cd6c4;
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
	}
	
	.show {
		margin: 0 0 10px 0;
		width: 48%;
		height: 500rpx;
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
		margin: 0 4px 0 0;
		font-size: 10px;
		background-color: #ff0000;
		border-radius: 8rpx;
		color: #fff;
	}
	
	.price span {
		font-size: 10px;
	}
	
	.priceBefore {
		float: right;
		color: #c7c7c7;
		text-decoration: line-through;
	}
	
	.priceNow {
		margin: 0 6px 0 0;
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