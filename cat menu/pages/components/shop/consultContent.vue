<template>
	<view class="">
		<view class="frame">
			<view class="doctorWord">
				<image src="../../../static/shop/consultPhoto.png" mode=""></image>
				<view class="wordContent">
					您好，我是您的医生助手，需要了解您宠物的情况辅助医生更好的诊断.
				</view>
			</view>
			<view class="doctorWord">
				<image src="../../../static/shop/consultPhoto.png" mode=""></image>
				<view class="wordContent">
					请尽可能详细描述您宠物的问题
					(具体症状、患病时长、用药情况
					等，10-200字)
				</view>
			</view>
			<view class="warn">
				您宠物的信息仅接诊医生可见，《猫谱》 为您提供
				隐私保护
			</view>
			<view class="customerWord" v-for = "(item,index) in list2" :key="index">
				<view class="customerWordContent">
					{{item}}
				</view>
				<image src="../../../static/shop/consultPhoto.png" mode=""></image>
			</view>
		</view>
		<view class="inputPlace">
			<view class="inputFrame">
				<input type="text" placeholder="请尽量相信描述,充分利用机会" v-model="inputContent">
				<view class="key" @click.stop="send">发送</view>
			</view>
			<view class="otherWay">
				<view class="ways" v-for="(item,index) in list" :key="index">
					<image :src="item.icon" mode="" :class="{once: index == 0, submit: index == 1}"></image>
					<span>{{item.content}}</span>
				</view>
			</view>
		</view>
	</view>

</template>

<script>
export default {
	data() {
		return {
			list:[
				{icon:'../../../static/shop/consult1.png',
				 content:'曾经问过'},
				{icon:'../../../static/shop/consult2.png',
				 content:'上传图片'},
				{icon:'../../../static/shop/consult3.png',
				 content:'语音输入'}
				],
			list2:['你好医生，我有很严重的问题。'],
			inputContent:''
		}
	},
	
	methods: {
		send() {
			// if(this.$refs.question.$refs.input.value!=" ") {
			// 	this.list2.push(this.$refs.question.$refs.input.value)
			// 	this.$refs.question.$refs.input.value=" "
			// }
			
			if(this.inputContent != ""){
				this.list2.push(this.inputContent)
				this.inputContent=''
			}
			
			else {
				uni.showToast({
					icon:'error',
					title:'请先输入内容'
				})
			}

		}
	}
	
}
</script>

<style>
	.frame {
		margin: 0 auto;
		width: 700rpx;
		height: 780rpx;
		overflow: scroll;
	}
	
	.doctorWord,.customerWord {
		margin: 0 0 20px 0;
	}
	
	.customerWord {
		width: 100%;
	}
	
	.customerWord image {
		width: 50px;
		height: 50px;
		border-radius: 50rpx;
		vertical-align: text-bottom;
		transform: translateX(42px);
	}
	
	.doctorWord image {
		width: 50px;
		height: 50px;
		border-radius: 50rpx;
		vertical-align: text-bottom;
	}
	
	.customerWordContent {
		display: inline-block;
		width: 70%;
		background-color: #f2f8f8;
		border-radius: 12rpx;
		transform: translateX(40px);
		font-size: 15px;
	}
	
	.wordContent {
		display: inline-block;
		margin: 0 0 0 20px;
		width: 70%;
		background-color: #f2f8f8;
		border-radius: 12rpx;
		font-size: 15px;
	}
	
	.warn {
		margin: 20px auto 20px auto;
		width: 610rpx;
		height: 70rpx;
		background-color: #efefef;
		color: #7f7f7f;
		border-radius: 16rpx;
		font-size: 12px;
	}
	
	.inputPlace {
		margin: 0 auto;
		position: absolute;
		top: 84%;
		left: 3.25%;
		width: 700rpx;
		height: 210rpx;
		z-index: 1;
	}
	
	.inputFrame {
		width: 100%;
		height: 50%;
	}
	
	.inputFrame input {
		width: 75%;
		height: 100%;
		border-radius: 30rpx;
		background-color: #f9f9f9;
		font-size: 18px;
		display: inline-block;
		transform: translateX(5px);
	}
	
	.otherWay {
		width: 100%;
		height: 50%;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
	}
	
	.key {
		display: inline-block;
		width: 20%;
		height: 70rpx;
		background-color: #93d7be;
		border-radius: 60rpx;
		line-height: 70rpx;
		text-align: center;
		color: #fff;
		transform: translate(15px,-20px);
	}
	
	.ways image {
		width: 40rpx;
		height: 44rpx;
		vertical-align: text-top;
	}
	
	.once {
		width: 50rpx !important;
		height: 48rpx !important;
	}
	
	.submit {
		width: 54rpx !important;
	}
	
	.ways span {
		margin: 0 0 0 4px;
		font-size: 12px;
	}
	
</style>