<template>
	<view class="community">
		<view class="push">
			
		</view>
		<navbar left-icon = "back" right-icon="cart" backgroundColor = transparent :border = "false"  @clickLeft="back">
			<template v-slot:default>
					<image src="../../../static/navigator/neiko.png" mode="" class="navbar"></image>
					<view  class="navWord">商城</view>					
			</template>
		</navbar>
		<view class="stage">
			<span v-for = "(item,index) in list" 
			:key="index"
			:class="{staging: stage == index}"> 
			{{item}} 
			</span>
		</view>
		<view class="opposite">
			<span class = "serve">服务方：猫谱</span>
			<span class = "doctor">医生详情 ></span>
		</view>
		<consultContent></consultContent>
	</view>
</template>

<script>
import navbar from "../../../uni_modules/uni-nav-bar/components/uni-nav-bar/uni-nav-bar.vue"
import consultContent from "./consultContent.vue"
export default {
	components: {
		navbar,
		consultContent,
	},
	
	data() {
		return{
			list:['描述问题','>','购买服务','>','等待回复','>','进入咨询'],
			stage: 0,
		}
	},
	
	methods: {
		back() {
			uni.switchTab({
				url:'/pages/components/shop'
			})
		}
	}
	
}
</script>

<style>
.community {
	background-color: #fcfdff;
	background-image: url("../../../static/background/background.png");
	background-repeat: no-repeat;
	background-size: 100%;
}	
	
.push {
	width: 100%;
	height: 90rpx;
} 
	
.navbar {
	width: 30px;
	height: 25px;
	transform: translate(65px,8px);
}	
	
.navWord {
	width: 100%;
	height: 100%;
	font-size: 20px;
	text-align: center;
	line-height: 44px;
}

.stage {
	margin: 0 auto;
	width: 700rpx;
	height: 60rpx;
	text-align: center;
	font-size: 15px;
}

.stage span {
	margin: 0 3px 0 3px;
	color: #b3b4b6;
}

.staging {
	color: #9dbfb4;
}

.opposite {
	margin: 0 auto 10px auto;
	width: 650rpx;
	height: 60rpx;
	line-height: 60rpx;
	border-top: 2px solid #f6f6f6;
}

.serve {
	float: left;
	font-size: 12px;
}

.doctor {
	float: right;
	font-size: 12px;
}

</style>