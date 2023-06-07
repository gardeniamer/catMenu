<template>
	<view class="function">
		<view class="functionTop">
			<slot name = "top"></slot>
		</view>
		<view class="functionBottom">
			<slot name = "bottom"></slot>
		</view>
	</view>
</template>

<script>
</script>

<style>
.function {
	margin: 10px auto 10px auto;
	width: 700rpx;
	height: 210rpx;
	background-color: #fff;
	border-radius: 10px;
}

.functionTop {
	width: 100%;
	height: 60rpx;
}

.functionBottom {
	width: 100%;
	height: 150rpx;
	display: flex;
	flex-direction: row;
	justify-content: space-around;
	align-items: center;
}

</style>