<template>
	<view class="brand">
		<view class="top">
			<span class = "word">品牌</span>
			<span class = "brandAll">查看所有品牌</span>
			<span class = "pointer"></span>
		</view>
		<view class="example">
			<view class="brands" v-for = "(item,index) in list" :key = "index">
				<view class="brandPhoto">
					<image :src="item.brand" mode=""></image>
					<view class="brandName">
						{{item.brandName}}
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			list:[{
				brandName:'爱肯拿',
				brand:'../../static/shop/brand1.png'
			},
			{
				brandName:'渴望',
				brand:'../../static/shop/brand2.png'
			},
			{
				brandName:'皇家',
				brand:'../../static/shop/brand3.png'
			},
			{
				brandName:'冠能',
				brand:'../../static/shop/brand4.png'
			}]
		}
	}
}
</script>

<style>
.brand {
	margin: 0 auto;
	width: 700rpx;
	height: 300rpx;
}

.top {
	width: 100%;
	height: 60rpx;
}

.word {
	display: inline-block;
	transform: translate(12px,5px);
}

.brandAll {
	display: inline-block;
	float: right;
	font-size: 10px;
	transform: translate(-16px,8px);
	color: #eea396;
}

.pointer {
	float: right;
	width: 5px;
	height: 5px;
	transform: translate(65px,13px) rotate(45deg);
	border-top: 1px solid #a7a7a7 ;
	border-right: 1px solid #a7a7a7;
}

.example {
	margin: 6px 0 0 0;
	width: 700rpx;
	height: 240rpx;
	display: flex;
	flex-direction: row;
	justify-content: space-around;
	align-items: center;
}

.brands {
	width: 180rpx;
	height: 100%;
	text-align: center;
}

.brandPhoto image {
	width: 70%;
	height: 50%;
}

.brandPhoto{
	margin: 0 auto;
	width: 175rpx;
	height: 240rpx;
}

</style>