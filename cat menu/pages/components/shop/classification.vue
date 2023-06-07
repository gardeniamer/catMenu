<template>
	<view class="all">
		<view class="classification">
			<view class="various" v-for = "(item,index) in list" :key = "index">
				<image :src="item.icon" mode=""></image>
				<view class="iconText">
					{{item.text}}
				</view>
			</view>
		</view>
		<view class="refer">
			<image src="../../../static/shop/refer.png" class="referPhoto" @click="consult"></image>
		</view>
	</view>
</template>

<script>
export default {	
	data() {
		return {
			list:[{
				icon:'../../static/shop/shopGift.png',
				text:'新手礼'
			},
			{
				icon:'../../static/shop/shopFood.png',
				text:'主粮'
			},
			{
				icon:'../../static/shop/shopSale.png',
				text:'零售'
			},
			{
				icon:'../../static/shop/shopLife.png',
				text:'用品'
			},
			{
				icon:'../../static/shop/shopTrain.png',
				text:'保健'
			}]			
		}

	},
	
	methods: {
		consult() {
			uni.navigateTo({
				url:'/pages/components/shop/consult'
			})
		}
	}
	
}
</script>

<style>
.all {
	margin: 10px auto 10px auto;
	width: 700rpx;
	height: 500rpx;
}

.classification {
	width: 100%;
	height: 30%;
	display: flex;
	flex-direction: row;
	justify-content: space-around;
	align-items: center;
}

.refer {
	margin: 10px 0 10px 0;
	width: 100%;
	height: 66%;
}

.various {
	width: 120rpx;
	height: 100%;
}

.various image {
	width: 45px;
	height: 45px;
	transform: translateX(8px);
}

.iconText {
	margin: 5px 0 0 0;
	text-align: center;
	font-size: 14px;
	font-weight: 500;
}

.referPhoto {
	margin: 0 auto;
	width: 700rpx;
	height: 350rpx;
	transform: translateX(0px);
}

</style>