<template>
	<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" circular class = "banner">
		<swiper-item v-for = "(item,index) in list" :key = "index">
			<image :src="item" mode="" class = "shopImg"></image>
		</swiper-item>
	</swiper>
</template>

<script>
export default {	
	data() {
		return {
			list:['../../static/shop/banner1.png',
			'../../static/shop/banner2.png',
			'../../static/shop/banner3.png',
			]
		}
	},
}
</script>

<style>
	.shopImg {
		width: 100%;
		height: 100%;
	}
	
	.banner {
		margin: 0 auto;
		width: 700rpx;
		height: 280rpx;
		border-radius: 20rpx;
		background-color: #fff;
	}
	
	.banner image {
		border-radius: 10rpx;
		margin: 0 2rpx 0 2rpx;
	}
	
</style>