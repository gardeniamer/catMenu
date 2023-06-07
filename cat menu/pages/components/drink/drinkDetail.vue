<template>
	<view class="detail">
		<view class="detailLeft">
			<view class="leftContent" 
			:class="{leftContentActive: leftName == item.name}" 
			v-for = "(item,index) in list" 
			:key = "index" 
			@click="changeLeft(item.name,index)">
				<image :src="item.leftIcon" mode="" :class="{leftImage: index == 1 || index == 2 || index == 3}"></image>
				<view class=" leftMsg ">
					{{item.name}}
				</view> 
			</view>
		</view>
		<view class="detailRight">
			<view class="milkTeas" v-for = "(item,index) in list2" :key = "index" v-show = "exChange == 0">
				<view class="teaPhoto">
					<image :src = "item.teaPhoto" :class="{rightTea: item.teaName=='浓缩咖啡星冰乐'||item.teaName=='抹茶星冰乐'||item.teaName=='卡布奇诺'||item.teaName=='风味拿铁'}"></image>
				</view>
				<view class="teaContent" >
					<view class="teaName">
						{{item.teaName}}
					</view>
					<view class="price">
						{{item.price}} 
						<span class = "priceBefore">起{{item.priceBefore}}</span>
					</view>
					<view class="priceDecline">
						{{item.priceDecline}}
					</view>
				</view>
				<view class="teaChoose">
					<view class="chooseSize" @click = "choose(item)">
						选规格
					</view>
				</view>
			</view>
			<view class="milkTeas" v-for = "(item,index) in list3" :key = "item.teaName" v-show = "exChange == 1">
				<view class="teaPhoto">
					<image :src = "item.teaPhoto" :class="{rightTea: item.teaName=='浓缩咖啡星冰乐'||item.teaName=='抹茶星冰乐'||item.teaName=='卡布奇诺'||item.teaName=='风味拿铁'}"></image>
				</view>
				<view class="teaContent" >
					<view class="teaName">
						{{item.teaName}}
					</view>
					<view class="price">
						{{item.price}} 
						<span class = "priceBefore">起{{item.priceBefore}}</span>
					</view>
					<view class="priceDecline">
						{{item.priceDecline}}
					</view>
				</view>
				<view class="teaChoose">
					<view class="chooseSize" @click = "choose(item)">
						选规格
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
import data from "../../data.js"
export default {
	props:{
		change:{
			type: Number
		}
	},
	
	created() {
		this.list2 = data.list8
		this.list3 = data.list9
	},
	
	data() {
		return {
			leftName:'店长推荐',
			list:[
				{leftIcon:'../../static/drink/drink1.png',
				 name:'店长推荐'
				},
				{leftIcon:'../../static/drink/drink2.png',
				 name:'活动商品'
				},
				{leftIcon:'../../static/drink/drink3.png',
				 name:'限时惊喜'
				},
				{leftIcon:'../../static/drink/drink4.png',
				 name:'暖冬限定'
				},
				{leftIcon:'../../static/drink/drink5.png',
				 name:'超有料家族'
				},
				{leftIcon:'../../static/drink/drink6.png',
				 name:'超赞奶茶'
				},
				],
			list2:[],
			list3:[],
			exChange: this.change
		}
	},
	
	methods: {
		changeLeft(name,index) {
			this.leftName = name
			if(index == 0) {
				this.list2 = data.list8
				this.list3 = data.list9
			}
			else {
				this.list2 = data.listMore[index - 1]
				this.list3 = data.listMore[index - 1]
			}
		},
		
		choose(obj) {
			console.log(obj);
		}
		
	},
	
	watch: {
		change(newValue,oldValue){
			this.exChange = newValue
			this.leftName = '店长推荐'
			this.list2 = data.list8
			this.list3 = data.list9
		}
	}
	
}
</script>

<style>
.detail {
	width: 100%;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	align-items: center;
}

.detailLeft {
	width: 28%;
	display: flex;
	flex-direction: column;
}

.leftContent {
	width: 100%;
	height: 250rpx;
	/* height: 16%; */
}

.leftContent image {
	margin: 30rpx auto 10rpx auto;
	width: 35rpx;
	height: 40rpx;
	display: block;
	transform: translateY(60rpx);
}

.leftImage {
	width: 40rpx !important;
}

.leftMsg {
	display: inline-block;
	width: 100%;
	height: 30rpx;
	font-size: 12px;
	text-align: center; 	
	line-height: 30rpx;
	transform: translateY(60rpx);
}

.leftContentActive {
	color: #3fdcd2;
	background-color: #fff;
}

/* .detailMore {
	width: 3%;
	height: 968rpx;
	background-color: #fff;
} */

.detailRight {
	width: 72%;
	display: flex;
	flex-direction: column;
	border-left: 8px solid #fff;
}

.rightTea {
	height: 160rpx !important;
	transform: translateY(30rpx) !important;
}

.milkTeas {
	margin: 0 0 1px 0;
	width: 100%;
	height: 240rpx;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	align-items: center;
	background-color: #fff;
}

.teaPhoto,.teaContent,.teaChoose {
	height: 100%;
}

.teaPhoto,.teaChoose {
	flex: 1;
}

.teaContent {
	flex: 2;
	transform: translateX(5px);
	margin: 60rpx 0 0 0;
}

.teaPhoto image {
	width: 160rpx;
	height: 200rpx;
	transform: translateY(20rpx);
}

.teaName {
	font-size: 16px;
	margin: 0 0 0 10px;
}

.price {
	font-weight: bold;
	margin: 10px 0 4px 10px;
}

.priceBefore {
	font-weight: normal;
	font-size: 10px;
	text-decoration:line-through;
	color: #cccccc;
	padding: 5px 0 0 5px;
}

.priceDecline {
	display: inline;
	margin: 0 0 0 10px;
	font-size: 10px;
	border: 1px solid #fe3a39;
	border-radius: 6px;
	color: #fe3a39;
	font-weight: 600;
}

.chooseSize {
	width: 100%;
	height: 60rpx;
	text-align: center;
	line-height: 60rpx;
	border-radius: 50rpx;
	background-color: #95d6bf;
	transform: translate(-4rpx,120rpx);
	color: #f5faf8;
	font-size: 14px;
}
</style>