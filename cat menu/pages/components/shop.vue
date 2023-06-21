<template>
	<view class="community">
		<view class="push">
			
		</view>
		<navbar :left-icon="icon" right-icon="cart" backgroundColor = transparent :border = "false" @clickLeft="back">
			<template v-slot:default>
					<image src="../../static/navigator/neiko.png" mode="" class="navbar"></image>
					<view  class="navWord">商城</view>					
			</template>
		</navbar>
			<view class="shopSearch">
			<input type="text" class = "searchInput" placeholder = "搜索商品"/>
			<image src="../../static/drink/drinkSearch.png" mode="" class = "search"></image>
			</view>
			<view v-show = "vipCombo == false">
				<shop-banner></shop-banner>
				<classification></classification>
				<combo-vip @vipChange="combo"></combo-vip>
				<shop-brand></shop-brand>
				<more-content :listMore = "listMore"></more-content>
			</view>
			<view v-show = "vipCombo == true">
				<vip-combo></vip-combo>
			</view>

	</view>
</template>

<script>
import navbar from "../../uni_modules/uni-nav-bar/components/uni-nav-bar/uni-nav-bar.vue"
import shopBanner from "./shop/shopBanner.vue"
import classification from "./shop/classification.vue"
import comboVip from "./shop/comboVip.vue"
import shopBrand from "./shop/shopBrand.vue"
import vipCombo from "./shop/vipCombo.vue"
import moreContent from "./shop/moreContent.vue"
import data from "../data.js"
export default {
	components: {
		navbar,
		shopBanner,
		classification,
		comboVip,
		shopBrand,
		vipCombo,
		moreContent
	},
	
	data() {
		return {
			list:
				[
				'../../static/drink/milkTea.png',
				'../../static/drink/milkTea2.png',
				'../../static/drink/milkTea3.png',
				'../../static/drink/milkTea4.png'
				],
			vipCombo:false,
			icon:'',
			listMore: []
		}
	},
	
	methods: {
		combo(index) {
			if(index == 1) {
				this.vipCombo = true
				this.icon = "back"
			}
		},
		
		back() {
			this.vipCombo = false
			this.icon = ""
		}
		
	},
	onHide() {
		this.vipCombo = false
		this.icon = ""
	},
	
	onReachBottom() {
		if(this.listMore == "") {
			this.listMore = data.list11More1
		}
		else if(this.listMore == data.list11More1) {
			this.listMore = data.list11More2
		}
		else if(this.listMore == data.list11More2) {
			this.listMore = data.list11More3
		}
		else if(this.listMore == data.list11More3) {
			this.listMore = data.list11More4
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
	background-size: 80%;
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

.shopSearch {
	width: 700rpx;
	height: 100rpx;
	margin: 10px auto 10px auto;
	background-color: #fff;
	border-radius: 50rpx;
}

.search {
	float: right;
	width: 96rpx;
	height: 96rpx;
	transform: translate(-3rpx,2rpx);
}

.searchInput {
	display: inline-block;
	width: 500rpx;
	height: 100rpx;
	transform: translateX(20px);
	font-size: 20px;
}

</style>