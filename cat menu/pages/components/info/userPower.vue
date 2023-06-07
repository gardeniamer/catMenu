<template>
	<view class="powerAll">
		<view class="powers" v-for = "(item,index) in list" :key = "index" @click="other(index)">
			<image :src="item.powerPath" mode="" 
			:class="{special: item.powerName == '个人动态' 
			,special2: item.powerName == '我的宠物'}">
			</image>
			<view class="powerName">
				{{item.powerName}}
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			list:[{
				powerPath:'../../static/navigator/phone.png',
				powerName:'个人动态'
			},
			{
				powerPath:'../../static/navigator/paw.png',
				powerName:'猫命名历'
			},
			{
				powerPath:'../../static/navigator/cat.png',
				powerName:'我的宠物'
			},
			{
				powerPath:'../../static/navigator/calendar.png',
				powerName:'喂猫打卡'
			},]
		}
	},
	
	methods: {
		other(index) {
			if(index == 3) {
				uni.navigateTo({
					url:'/pages/components/info/attendance'
				})
			}
			if(index == 2) {
				uni.navigateTo({
					url:'/pages/components/info/pet'
				})
			}
		}
	}
	
}
</script>

<style>
.powerAll {
	margin: 10px auto 10px auto;
	width: 700rpx;
	height: 210rpx;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	align-items: center;
	background-color: #fff;
	border-radius: 10px;
}

.powers {
	width: 22%;
	height: 100%;
	text-align: center;
	transform: translateY(40rpx);
}

.powers image {
	width: 100rpx;
	height: 80rpx;
}

.special {
	width: 54rpx !important;
}

.special2 {
	width: 130rpx !important;
	transform: translateX(-10rpx);
}

.powerName {
	font-family: STCaiyun;
	color: #c1b28c;
}

</style>