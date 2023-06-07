<template>
	<view class="allUser">
		<view class="leftPhoto" @click="login()"></view>
		<view class="rightMsg">
			<view class="topMsg" @click="login()">
				点击头像登录
			</view>
			<view class="bottomMsg">
				<view class="badge" v-for = "(item,index) in list" :key = "index">
					{{item}}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			list:['优惠券','积分','社交达人']
		}
	},
	methods: {
		login() {
			uni.navigateTo({
				url:'/pages/components/login'
			})
		}
	}
}
</script>

<style>
.allUser {
	margin: 10px auto 10px auto;
	width: 700rpx;
	height: 210rpx;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	align-items: center;
}

.leftPhoto {
	width: 30%;
	height: 95%;
	border-radius: 60rpx;
	background: url("../../../static/info/userPhoto.png");
	background-repeat: no-repeat;
	background-size: 100%;
	background-position: center center;
	box-shadow: 5px 5px 20px #039cd6;
}

.rightMsg {
	width: 60%;
	height: 100%;
	display: flex;
	flex-direction: column;
	justify-content: space-around;
	align-items: center;
}

.topMsg,.bottomMsg {
	width: 100%;
	height: 50%;
}

.topMsg {
	text-align: left;
	line-height: 104rpx;
	font-size: 20px;
	color: #5e6376;
}

.bottomMsg {
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	align-items: center;
	flex-wrap: wrap;
	overflow: hidden;
}

.badge {
	margin: 0 0 1px 0;
	width: 30%;
	height: 50%;
	border-radius: 40rpx;
	background-color: #ffecd2;
	font-size: 12px;
	text-align: center;
	line-height: 52rpx;
}

</style>