<template>
	<view class="community">
		<view class="push">
			
		</view>
		<navbar right-icon="gear" backgroundColor = transparent :border = "false" >
			<template v-slot:default>
					<image src="../../static/navigator/neiko.png" mode="" class="navBarInfo"></image>
					<view  class="navWord">我的</view>					
			</template>
		</navbar>
		<info-user></info-user>
		<user-power></user-power>
		<info-more>
			<template #top>
				<view class = "left">我的订单</view>
				<view class = "right" @click="allMsg">查看全部</view>
			</template>
			<template #bottom>
				<view class = "obj" v-for = "(item,index) in list" :key = "index">
					<image :src = "item.imgPath" mode="" class = "moreImg" @click="singleMsg1(index)"></image>
					<view class="imgContent">
						{{item.imgContent}}
					</view>
				</view>
			</template>
		</info-more>
		<info-more>
			<template #top>
				<view class = "left">常用信息</view>
			</template>
			<template #bottom>
				<view class = "obj" v-for = "(item,index) in list2" :key = "index">
					<image :src = "item.imgPath" mode="" class = "moreImg" @click="singleMsg2(index)"></image>
					<view class="imgContent">
						{{item.imgContent}}
					</view>
				</view>
			</template>
		</info-more>
		<info-more>
			<template #top>
				<view class = "left">领养必读</view>
			</template>
			<template #bottom>
				<view class = "obj" v-for = "(item,index) in list3" :key = "index">
					<image :src = "item.imgPath" mode="" class = "moreImg" @click="singleMsg3(index)"></image>
					<view class="imgContent">
						{{item.imgContent}}
					</view>
				</view>
			</template>
		</info-more>
		<info-more>
			<template #top>
				<view class = "left">我的服务</view>
			</template>
			<template #bottom>
				<view class = "obj" v-for = "(item,index) in list4" :key = "index">
					<image :src = "item.imgPath" mode="" class = "moreImg" @click="singleMsg4(index)"></image>
					<view class="imgContent">
						{{item.imgContent}}
					</view>
				</view>
			</template>
		</info-more>
		<view class="push2">
			
		</view>
	</view>
</template>

<script>
import navbar from "../../uni_modules/uni-nav-bar/components/uni-nav-bar/uni-nav-bar.vue"
import infoUser from "./info/infoUser.vue"
import userPower from "./info/userPower.vue"
import infoMore from "./info/infoMore.vue"
import data from "../data.js"
export default {
	components: {
		navbar,
		infoUser,
		userPower,
		infoMore
	},
	
	created() {
		this.list = data.list
		this.list2 = data.list2
		this.list3 = data.list3
		this.list4 = data.list4
	},
	
	data() {
		return {
			list: [],
			list2: [],
			list3: [],
			list4: [],		
		}

	},
	
	methods: {
		allMsg() {
			console.log("ok")
		},
		
		singleMsg1(index){
			console.log(index);
		},
		
		singleMsg2(index){
			console.log(index);
		},
		
		singleMsg3(index){
			console.log(index);
		},
	
		singleMsg4(index){
			console.log(index);
		}
		
	}
	
}
</script>

<style>
* {
	margin: 0;
	padding: 0;
}	
	
.community {
	background-color: #f0f0f0;
	background-image: url("../../static/background/background.png");
	background-repeat: no-repeat;
	background-size: 90%;
}

.push {
	width: 100%;
	height: 90rpx;
}

.navBarInfo {
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

.left {
	display: inline-block;
	transform: translate(6px,5px);
}

.right {
	display: inline-block;
	font-size: 12px;
	float: right;
	color: #a2a2a2;
	transform: translate(-6px,7px);
}

.obj {
	width: 20%;
	height: 100%;
	text-align: center;
	transform: translateY(10px);
}

.moreImg {
	width: 28px;
	height: 25px;
}

.imgContent {
	transform: translateY(6px);
	font-size: 12px;
}

.push2 {
	width: 100%;
	height: 10rpx;
}

</style>