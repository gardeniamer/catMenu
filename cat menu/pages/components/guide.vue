<template>
	<view class="">
	<!-- <before-login v-if = "change == false"></before-login> -->
	<swiper :indicator-dots="true" :autoplay="false" @change="loginDemo($event)" v-if = "change == true">
		<swiper-item v-for="(item,index) in list" :key="index">
			<view class="swiper-item">
				<view class="swiper-item">
					<image :src="item" mode=""></image>
					<view class="entry" v-show = "special && index == 2" @click="entry">
						进入
					</view>
				</view>
			</view>
		</swiper-item>
	</swiper>	
	</view>

</template>

<script>
	import beforeLogin from "./beforeLogin.vue"
	export default {
		
		components: {
			beforeLogin,
		},
		
		data() {
			return {
				list:[
				'../../static/login/guide1.png',
				'../../static/login/guide2.png',
				'../../static/login/guide3.png'
				],
				special: false,
				change: false
			}
		},
		
		methods: {
			loginDemo(event) {
				if(event.detail.current == 2) {
					setTimeout(()=>{
						this.special = true
						uni.setStorage({
							key:"initial",
							data: true
						})
					}, 10);
				}
			},
			
			entry(){
				uni.switchTab({
					url:'/pages/main'
				})
			}
			
		},
		
		mounted() {
			setTimeout(()=>{
				uni.getStorage({
					key:"initial",
					success(res) {
						if(res.data == true) {
							uni.switchTab({
								url:'/pages/main'
							})
						}
					}
				})
				this.change = true
			}, 100);	
			
		},
		
	}
</script>

<style>
	
	uni-swiper {
		display: block;
		height: 1320rpx;
	}
	
	swiper-item {
		overflow: auto;
	}
	
	.swiper-item {
		margin: 0 auto;
		width: 700rpx;
		height: 1247rpx;
	}
	
	.swiper-item image {
		width: 100%;
		height: 100%;
	}
	
	.entry {
		margin: 0 auto;
		width: 200rpx;
		height: 60rpx;
		font-size: 18px;
		text-align: center;
		line-height: 60rpx;
		background-color: #c7e9dd;
		transform: translateY(-30px);
		border-radius: 40rpx;
		color: #fff;
	}
	
</style>