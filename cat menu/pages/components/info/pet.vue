<template>
	<view class="allContent">
		<view class="push">
			
		</view>
		<navbar left-icon = "back" backgroundColor = transparent :border = "false" @clickLeft="back">
			<template v-slot:default>
					<image src="../../../static/navigator/cat.png" mode="" class = "infoNav"></image>
					<view  class="navWord">我的宠物</view>					
			</template>
		</navbar>
		<view class="msg">
			<view class="top">
				<view class="topWord1">
					宠物管家服务
				</view>
				<view class="topWord2">
					免费帮您个性订制养宠方案
				</view>
			</view>
			<view class="moreMsg" v-for="(item,index) in list" :key="index">
				{{item.name}}
				<view class="choose" v-if="index != 5 && index != 6 && index != 2">
					{{item.format}}
				</view>
				
				<view class="photo" v-else-if="index == 2">
					<image :src="item.format" mode="" class="photoUser"></image>
				</view>
				
				<view class="choices" v-else>
					<span v-for="(item2,index1) in item.format" 
					:key="index1"
					:class="{activeOne: activeOne == index1 && index == 5, 
					activeTwo: activeTwo == index1 && index == 6}"
					@click="changeMsg(index,index1)"
					>{{item2}}</span>
				</view>
				<view class="pointer" v-if = "index != 5 && index != 6 && index != 1"></view>
			</view>
		</view>
		<view class="backGround">
			<view class="final">
				完成
			</view>
		</view>
		<view class="push2">
			
		</view>
	</view>
</template>

<script>
import navbar from "../../../uni_modules/uni-nav-bar/components/uni-nav-bar/uni-nav-bar.vue"
export default {
	components: {
		navbar,
	},
	
	data() {
		return {
		list:[
			{
				name:'宠物品种',
				format: '请选择'
			},
			{
				name:'宠物昵称',
				format: '请填写'
			},
			{
				name:'头像',
				format: '../../../static/info/myPetPhoto.png'
			},
			{
				name:'出生日期',
				format: '请选择'
			},
			{
				name:'相伴日期',
				format: '请选择'
			},
			{
				name:'宠物性别',
				format: ['公','母']
			},
			{
				name:'是否绝育',
				format: ['是','否']
			},
			{
				name:'疫苗',
				format: '请选择'
			},
			],
			activeOne: 0,
			activeTwo: 0
		}

	},
	
	methods: {
		changeMsg(index,index1) {
			if(index == 5) {
				this.activeOne = index1
			}
			if(index == 6) {
				this.activeTwo = index1
			}
		},
		
		back() {
			uni.switchTab({
				url:'/pages/components/info'
			})
		},
		
	}
	
	
}
</script>

<style>
	
	.allContent {
			background-color: #f0f0f0;
			background-image: url("../../../static/background/background.png");
			background-repeat: no-repeat;
			background-size: 60%;
	}
	
	.push {
		width: 100%;
		height: 90rpx;
	}
	
	.infoNav {
		width: 60px;
		height: 25px;
		transform: translate(25px,8px);
	}
	
	.navWord {
		width: 100%;
		height: 100%;
		font-size: 20px;
		text-align: center;
		line-height: 44px;
	}
	
	.msg {
		margin: 0 auto;
		width: 90%;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: center;
	}
	
	.top {
		width: 100%;
		height: 120rpx;
	}
	
	.topWord1 {
		font-size: 20px;
		font-weight: bold;
	}
	
	.topWord2 {
		margin: 10px 0 0 0;
		font-size: 12px;
	}
	
	.moreMsg {
		width: 100%;
		height: 150rpx;
		line-height: 150rpx;
		position: relative;
	}
	
	.choose {
		display: inline-block; 
		float: right; 
		transform: translateX(-20px);
		font-size: 14px;
		color: #9c9c9c;
	}
	
	.pointer {
		position: absolute;
		top: 50%;
		left: 95%;
		display: inline-block;
		width: 8px;
		height: 8px;
		border-top: 1px solid #9c9c9c;
		border-left: 1px solid #9c9c9c;
		transform: translateY(-50%) rotate(135deg);
	}
	
	.choices {
		float: right;
		display: inline-block;
	}
	
	.choices span {
		display: inline-block;
		margin: 4px;
		width: 60rpx;
		height: 60rpx;
		font-size: 15px;
		line-height: 60rpx;
		text-align: center;
		border: 1px solid #9c9c9c;
	}
	
	.activeOne {
		background-color: #f4faf6;
		color: #67a891;
	}
	
	.activeTwo {
		background-color: #f4faf6;
		color: #67a891;
	}
	
	.photo {
		float: right;
		display: inline-block;
		width: 60rpx;
		height: 60rpx;
		transform: translate(-30px,8px);
	}
	
	.photoUser {
		width: 100%;
		height: 100%;
	}
	
	.backGround {
		width: 100%;
		height: 120rpx;
		background-color: #f1f1f1;
	}
	
	.final {
		margin: 0 auto;
		width: 600rpx;
		height: 100rpx;
		background-color: #aeddcd;
		text-align: center;
		line-height: 100rpx;
		border-radius: 60rpx;
		color: #fff;
		font-size: 20px;
		transform: translateY(5px);
	}
	
	.push2 {
		width: 100%;
		height: 40rpx;
	}
	
</style>