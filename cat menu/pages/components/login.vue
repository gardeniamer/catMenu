<template>
	<view class="loginDemo">
		<view class="demoIcon">
			<view class="iconAll">
				<view class="neiko">
					<image src="../../static/navigator/neiko.png" mode="" class = "cat"></image>
				</view>
					<image src="../../static/login/loginWords.png" mode="" class = "words"></image>
			</view>
		</view>
		<view class="entry">
			<view class="weChat">
				<image src="../../static/login/weChat.png" mode="" class = "loginChat"></image>
				<span>微信登录</span>
			</view>
			<view class="phone" @click="change()">
				<image src="../../static/login/loginPhone.png" mode="" class = "loginPhone"></image>
				<span class = "phoneWay">手机号登录</span>
			</view>
			<view class="final">
				<label class="radio">
					<radio value="" /><text class = "finalWord">我已阅读并同意猫谱<a href="#">《用户协议》</a>和<a href="#">《隐私政策》</a></text>
				</label>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		methods: {
			change() {
				uni.navigateTo({
					url:'/pages/components/login2'
				})
			}
		}
	}
</script>

<style>
	
	.radio a {
		text-decoration: none;
	}
	
	.loginChat {
		width: 25px;
		height: 25px;
		transform: translateX(-10px);
		vertical-align: middle;
	}
	
	.loginPhone {
		width: 20px;
		height: 30px;
		vertical-align: middle;
	}
	
	.loginDemo {
		width: 100%;
		height: 1620rpx;
		background: url("../../static/login/loginBJ.png");
		background-repeat: no-repeat;
	}
	
	.demoIcon {
		width: 100%;
		height: 60%;
	}
	
	.entry {
		width: 100%;
		height: 40%;
	}
	
	.neiko {
		margin: 0 auto;
		width: 250rpx;
		height:250rpx;
		background-color: #72a498;
		text-align: center;
		border-radius: 30rpx;
		box-shadow: 10px 5px 10px #72a498;
	}
	
	.iconAll {
		margin: 0 auto;
		width: 250rpx;
		height: 408rpx;
		text-align: center;
		transform: translateY(200rpx);
	}
	
	.cat {
		width: 80%;
		height: 80%;
		transform: translateY(24rpx);
	}
	
	.words {
		width: 80%;
		height: 120rpx;
		transform: translateY(16px);
	}
	
	.weChat,.phone {
		margin: 0 auto 30px auto;
		width: 80%;
		height: 100rpx;
		border-radius: 50rpx;
		text-align: center;
		line-height: 100rpx;
	}
	
	.weChat {
		background-color: #95d6be;
	}
	
	.phone {
		background-color: #fbe3b5;
	}
	
	.phoneWay {
		display: inline-block;
		transform: translateX(6px);
	}
	
	.final {
		margin: 0 auto;
		text-align: center;
	}
	
	.finalWord {
		font-size: 12px;
	}
	
</style>