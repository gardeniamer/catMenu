<template>
	<view class="chooseMenu">
		<view :class="{menu: menuName == 'typical'}" @click="changeMenu('typical',0)">
			经典菜单
		</view>
		<view :class="{menu: menuName == 'hot'}" @click="changeMenu('hot',1)">
			热销排行
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return {
				menuName: 'typical',
			}
		
		},
		
		methods: {
			changeMenu(name,index) {
				this.menuName = name
				this.$emit("exchange", index)
			}
		},
	}

</script>

<style>
	.chooseMenu {
		width: 100%;
		height: 100rpx;
		border-bottom: 1px solid #a9a9a9;
		background-color: #fff;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		text-align: center;
		line-height: 100rpx;
	}
	
	.menu {
		border-bottom: 4px solid #95d6bf;
		font-weight: bold;
	}
</style>