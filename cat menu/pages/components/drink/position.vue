<template>
	<view class="positionAll">
		<view class="innerContent">
			<view class="">
				<image src="../../../static/drink/star.png" mode="" class = "star"></image>
				<span class = "positionDetail">晋中榆次店</span>
			</view>
			<view class="positionContent">
				<image src="../../../static/drink/position.png" mode="" class = "position"></image>
				<span class = "positionDetails">距离您2.0km</span>
			</view>
			<view class="choose">
				<view class="getSelf" :class = "{chooseMethod : name == 'getSelf'}" @click="chooseMethod('getSelf')">
					自取
				</view>
				<view class="getOther" :class = "{chooseMethod : name == 'getOther'}" @click="chooseMethod('getOther')">
					配送
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				name: 'getSelf',
			}
		},
		
		methods: {
			chooseMethod(name) {
				this.name = name
			}
		}
	}
</script>

<style>
	.positionAll {
		margin: 20rpx auto;
		width: 720rpx;
		height: 120rpx;
		position: relative;
	}
	
	.innerContent {
		width: 95%;
		height: 88%;
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%,-50%);
		background-color: #fff;
		border-radius: 25rpx;
	}
	
	.star {
		width: 20px;
		height: 19px;
		vertical-align: middle;
		transform: translateX(22rpx);
	}
	
	.positionDetail {
		display: inline-block;
		transform: translate(30rpx,4rpx);
		font-size: 15px;
	}
	
	.position {
		width: 12px;
		height: 16px;
		transform: translate(30rpx,12rpx);
	}
	
	.positionDetails {
		display: inline-block;
		font-size: 8px;
		transform: translate(40rpx,10rpx);
		color: #a9a9a9;
	}
	
	.choose {
		width: 200rpx;
		height: 50rpx;
		position: absolute;
		top: 50%;
		left: 68%;
		transform: translateY(-50%);
		border-radius: 60rpx;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		background-color: #f0f0f0;
	}
	
	.getSelf,.getOther {
		width: 100rpx;
		height: 50rpx;
		border-radius: 60rpx;
		text-align: center;
		line-height: 50rpx;
		font-size: 14px;
	}
	
	.chooseMethod {
		background-color: #95d6bf;
	}
</style>