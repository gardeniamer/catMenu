<template>
	<view class="loginDemo">
		<view class="phoneNumber">
			<span>手机号</span>
			<input type="text" name="" id="" placeholder="请输入您的手机号" ref="number">
		</view>
		<view class="password">
			<span v-show = "change == false">验证码</span>
			<span v-show = "change == true">密码</span>
			<input type="text" name="" id="" placeholder="请输入验证码" v-show = "change == false" ref="password01">
			<input type="text" name="" id="" placeholder="请输入密码" v-show = "change == true" ref="password02">
			<span class = "get" v-show = "change == false">获取验证码</span>
		</view>
		<view class="question">
			<span class = "change" v-show = "change == false" @click="exchange">用账号密码登录</span>
			<span class = "change" v-show = "change == true" @click="exchange">用验证码登录</span>
			<span class = "doubt" v-show = "change == false">获取不到验证码？</span>
		</view>
		<view class="login" @click.native="loginMain">
			免注册登录
		</view>
		<view class="final">
			<label class="radio">
				<radio value="" checked="true"/><text class = "finalWord">同意猫谱<a href="#">《用户协议》</a>和<a href="#">《隐私政策》</a></text>
			</label>
		</view>
		<view class="otherContent">
			----------其它登录方式----------
		</view>
		<view class="other">
			<view class="icons" v-for = "(item,index) in list" :key = "index">
				<image :src="item" mode=""></image>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:[
				'../../static/login/chat.png',
				'../../static/login/zhifubao.png',
				'../../static/login/QQ.png',
				'../../static/login/shouji.png',
				'../../static/login/apple.png'
				],
				change: false,
			}
		},
		
		methods: {
			exchange() {
				this.change = !this.change
			},
			
			loginMain() {
				const re=/\d{11}/
				if(re.test(this.$refs.number.$refs.input.value) 
				&& this.$refs.password01.$refs.input.value!="" 
				|| this.$refs.password02.$refs.input.value!=""){
						uni.switchTab({
							url:'/pages/main'
						})						
				}
				else{
					uni.showToast({
						icon:'none',
						title:"请输入正确的手机号或密码"
					})
				}
			}
			
		}
		
	}
</script>

<style>
	
	a {
		text-decoration: none;
	}
	
	.loginDemo {
		width: 100%;
		height: 1620rpx;
		background: url("../../static/login/loginBJ.png");
		background-repeat: no-repeat;
	}
	
	.phoneNumber,.password {
		width: 100%;
		height: 100rpx;
		border-bottom: 1px solid #a9a9a9;
		line-height: 120rpx;
	}
	
	.phoneNumber span, .password span, .question span {
		display: inline-block;
		transform: translate(30px);
		color: #8f8f8f;
	}
	
	.phoneNumber input, .password input {
		display: inline-block;
		transform: translate(60px,4px);
		font-size: 12px;
	}
	
	.get {
		width: 200rpx;
		height: 70rpx;
		color: #fff !important;
		font-size: 14px;
		text-align: center;
		line-height: 70rpx;
		background-color: #c7e9dd;
		border-radius: 70rpx;
		transform: translate(150rpx,-10rpx) !important;
	}
	
	.question {
		margin: 15px 0 0 0;
		height: 60rpx;
	}
	
	.change {
		float: left;
		transform: translate(60rpx);
		font-size: 14px;
	}
	.doubt {
		float: right;
		transform: translate(-10rpx) !important;
		font-size: 14px;
	}
	
	.login {
		margin: 15px auto 0 auto;
		width: 500rpx;
		height: 100rpx;
		background-color: #b2e1d9;
		border-radius: 40rpx;
		color: #fff;
		text-align: center;
		line-height: 100rpx;
	}
	
	.otherContent {
		position: absolute;
		top: 70%;
		left: 10%;
		width: 80%;
		height: 40rpx;
		text-align: center;
		font-size: 14px;
		color: #8f8f8f;
	}
	
	.other {
		position: absolute;
		top: 75%;
		left: 10%;
		width: 80%;
		height: 100rpx;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
	}
	
	.icons {
		width: 18%;
		height: 100%;
	}
	
	.icons image {
		width: 95%;
		height: 98%;
		transform: translate(4rpx,1rpx);
	}
	
	.final {
		text-align: center;
		margin: 10px 0 0 0;
	}
	
	.finalWord {
		font-size: 12px;
	}
	
</style>