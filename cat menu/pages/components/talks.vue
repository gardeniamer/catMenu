<template>
	<view class="talksAll">
		<view class="talks">
			<view class="attention">
				<view class="attentionAll" @click="change('attention')">
					关注
					<image src="../../static/talks/attention.png" mode="" v-if = "changeAll != 'attention'"></image>
					<image src="../../static/talks/s_attention.png" mode="" v-if = "changeAll == 'attention'"></image>
				</view>
			</view>
			<view class="find">
				<view class="findAll" @click="change('find')">
					发现
					<image src="../../static/talks/find.png" mode="" v-if = "changeAll != 'find'"></image>
					<image src="../../static/talks/s_find.png" mode="" v-if = "changeAll == 'find'"></image>
				</view>
			</view>
			<view class="nearBy">
				<view class="nearByAll" @click="change('nearBy')">
					附近
					<image src="../../static/talks/nearby.png" mode="" v-if = "changeAll != 'nearBy'"></image>
					<image src="../../static/talks/s_nearby.png" mode="" v-if = "changeAll == 'nearBy'"></image>
				</view>
			</view>
		</view>
<!-- 		<keep-alive>
			<component :is = "changeAll"></component>
		</keep-alive> -->
		<attention v-show = "changeAll == 'attention'" :moreContent = "listMore"></attention>
		<find v-show = "changeAll == 'find'"></find>
		<near-by v-show = "changeAll == 'nearBy'"></near-by>

	</view>
</template>

<script>
	import attention from './talks/attention.vue'
	import find from './talks/find.vue'
	import nearBy from './talks/nearBy.vue'
	export default {
		props:{
			more:{
				type: Array
			}
		},
		
		components:{
			attention,
			find,
			nearBy
		},
		
		data(){
			return{	
				changeAll: 'attention',
				listMore:[]
			}
		},
		
		methods: {
			change(name) {
				this.changeAll = name
			}
		},
		
		watch:{
			more:{
				handler(newValue,oldValue){
				this.listMore = newValue
				},
				deep:true
			}
		
		}
		
	}
</script>

<style>
	
.talks image {
	width: 22px;
	height: 18px;
	transform: translate(8rpx,4rpx);
}
	
.talks {
	margin: 10px auto;
	width: 700rpx;
	height: 110rpx;
	background-color: black;
	border-radius: 50rpx;
	background-color: #ffffff;
	display: flex;
	flex-direction: row;
	justify-content: space-around;
	align-items: center;
}

.attention,.nearBy,.find {
	width: 160rpx;
	height: 88rpx;
	text-align: center;
	line-height: 88rpx;
	font-size: 20px;
}

.nearByAll image {
	width: 20px;
	height: 20px;
}

.findAll image {
	width: 22px;
	height: 16px;
	transform: translate(8rpx,3rpx);
}

</style>