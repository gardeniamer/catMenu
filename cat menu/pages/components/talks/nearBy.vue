<template>
	<view class="">
		<view class="title">
			推荐:
		</view>
		<view class="catMsg">
			<view class="msgDetail" v-for="(item,index) in list" :key="index">
				<image :src="item.catPhoto" mode="" class="detailPhoto"></image>
				<view class="detailContent">
					{{item.photoContent}}
				</view>
				<view class="monsterMsg">
					<image :src="item.userPhoto" mode="" class = "monsterPhoto"></image>
					<span class = "monsterName">{{item.userName}}</span>
					<image src="../../../static/talks/heart.png" mode="" class = "heart">
						<span class = "heartCount">{{item.heart}}</span>
					</image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [{
					catPhoto:'../../../static/talks/near1.png',
					photoContent:'铲屎官如何照顾好一只猫',
					userPhoto:'../../../static/talks/find1.png',
					userName:'凤梨不是梨',
					heart:'137'
				},
				{
					catPhoto:'../../../static/talks/near2.png',
					photoContent:'猫咪老打喷嚏,不只是患了感冒',
					userPhoto:'../../../static/talks/find2.png',
					userName:'w_FangTon',
					heart:'185'
				},
				{
					catPhoto:'../../../static/talks/near5.png',
					photoContent:'挑战猫藓(药浴分享)',
					userPhoto:'../../../static/talks/find3.png',
					userName:'熙熙攘攘',
					heart:'175'
				},
				{
					catPhoto:'../../../static/talks/near4.png',
					photoContent:'品种猫VS土猫哪个更值',
					userPhoto:'../../../static/talks/userPhoto2.png',
					userName:'深度',
					heart:'118'
				},
				{
					catPhoto:'../../../static/talks/near7.png',
					photoContent:'猫猫与其他动物的关系',
					userPhoto:'../../../static/talks/userPhoto4.png',
					userName:'百科全书',
					heart:'309'
				},
				{
					catPhoto:'../../../static/talks/near8.png',
					photoContent:'猫猫课堂开课了！！',
					userPhoto:'../../../static/talks/userPhoto6.png',
					userName:'懂猫人',
					heart:'227'
				}]
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
		transform: translateX(30rpx);
	}
	
	.catMsg {
		margin: 0 auto;
		width: 700rpx;
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: space-around;
		align-items: center;
	}
	
	.msgDetail {
		margin: 5px 0 10px 0;
		width: 310rpx;
		height: 420rpx;
		background-color: #fff;
		border-radius: 12rpx;
	}
	
	.detailPhoto {
		width: 100%;
		height: 70%;
		border-top-left-radius: 10rpx;
		border-top-right-radius: 12rpx;
	}
	
	.detailContent {
		width: 90%;
		margin: 0 auto;
		font-size: 10px;
	}
	
	.monsterMsg {
		margin: 0 auto;
		width: 95%;
		height: 40rpx;
		transform: translateY(9rpx);
	}
	
	.monsterPhoto {
		width: 18px;
		height: 18px;
		border-radius: 18px;
		vertical-align: middle;
	}
	
	.monsterName {
		display: inline-block;
		width: 155rpx;
		font-size: 8px;
		transform: translateX(12rpx);
	}
	
	.heart {
		float: right;
		width: 13px;
		height: 12px;
		transform: translate(-60rpx,14rpx);
	}
	
	.heartCount {		
		float: right;
		font-size: 12px;
		transform: translate(16rpx,10rpx);
	}
	
</style>