<template>

	<view class="community">
		<view class="push">
			
		</view>
		<navbar right-icon="cart" backgroundColor = transparent :border = "false">
			<template v-slot:default>
					<image src="../../static/navigator/paw.png" mode="" class="navbar"></image>
					<view  class="navWord">饮品</view>					
			</template>
		</navbar>
		<view class="drinkSearch">
			<input type="text" class = "searchInput" placeholder = "搜索奶茶" v-model="inputMilk"/>
			<image src="../../static/drink/drinkSearch.png" mode="" class = "search" @click="search"></image>
		</view>
		<position></position>
		<choose-menu @exchange = "change"></choose-menu>
		<drink-detail :change = "changeIndex"></drink-detail>
	</view>

</template>

<script>
	import navbar from "../../uni_modules/uni-nav-bar/components/uni-nav-bar/uni-nav-bar.vue"
	import position from "./drink/position.vue"
	import chooseMenu from "./drink/chooseMenu.vue"
	import drinkDetail from "./drink/drinkDetail.vue"
	export default {
		components: {
			navbar,
			position,
			chooseMenu,
			drinkDetail,
		},
		
		data() {
			return {
				changeIndex: 0,
				inputMilk:''
			}
		},
		
		methods:{
			change(index) {
				this.changeIndex = index
			},
			
			search() {
				console.log(this.inputMilk);
			}
			
		},
		
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
	background-size: 70%;
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

.drinkSearch {
	width: 700rpx;
	height: 80rpx;
	margin: 10px auto 5px auto;
	background-color: #fff;
	border-radius: 50rpx;
}

.search {
	float: right;
	width: 80rpx;
	height: 80rpx;
	transform: translate(-3rpx,0rpx);
}

.searchInput {
	display: inline-block;
	width: 500rpx;
	height: 80rpx;
	transform: translateX(20px);
	font-size: 16px;
}

</style>
