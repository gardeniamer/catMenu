<template>
	<view class="allContent">
		<view class="combo" v-for = "(item,index) in list" 
		:key = "index" @click="entryDetail(index)">
			<span class = "comboContent">{{item.comboContent}}</span>
			<span class = "trait">{{item.trait}}</span>
			<view class="comboIntro">
				{{item.comboIntro}}
			</view>
			<view class="comboPhoto">
				<view class="photo" v-for="(item2,index2) in item.vip" :key="index2">
					<image :src="item2" mode=""></image>
					<view class = "price" v-for="(item3,index3) in item.price" :key="index3" v-if="index2 == index3">
						{{item3}}
						 <span class = "priceBefore" v-for="(item4,index4) in item.priceBefore" :key="index4" v-if="index2 == index4">{{item4}}</span>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	emit:["vipChange"],
	
	data() {
		return {
			list:[{
				comboContent:'养宠套餐',
				trait:'高性价比',
				comboIntro:'养宠顾问私人定制',
				vip:['../../static/shop/animalCombo.png','../../static/shop/animalCombo.png'],
				price:['￥72','￥99'],
				priceBefore:['￥180','￥236'],
			},
			{
				comboContent:'会员福利',
				trait:'会员专享',
				comboIntro:'网易严选高性价比',
				vip:['../../static/shop/show2.png','../../static/shop/show.png'],
				price:['￥22','￥39'],
				priceBefore:['￥32','￥40']
			}]
		}
	},
	
	methods: {
		entryDetail(index) {
			this.$emit("vipChange", index)
		}
	}
	
}
</script>

<style>
.allContent {
	margin: 0 auto;
	width: 700rpx;
	height: 300rpx;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	align-items: center;
}

.combo,.vip {
	width: 48%;
	height: 100%;
}

.trait {
	display: inline-block;
	padding: 1px;
	font-size: 12px;
	transform: translateX(8px);
	background-color: #fa6306;
	color: #fff;
	border-radius: 3px;
}

.comboIntro {
	font-size: 12px;
	color: #b63028;
	transform: translateY(5px);
}

.comboPhoto {
	width: 100%;
	height: 75%;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	align-items: center;
	position: relative;
}

.photo {
	width: 50%;
	height: 70%;
	text-align: center;
}

.photo image {
	width: 60px;
	height: 60px;
}

.price {
	color: #b63028;
	font-size: 12px;
}

.priceBefore {
	display: inline-block;
	float: right;
	color: #a9a9a9;
	font-size: 10px;
	text-decoration: line-through;
	transform: translateX(-5rpx);
}

</style>