<template>
	<view class="community">
		<view class="push">
		
		</view>
		<navbar right-icon="search" backgroundColor = transparent :border = "false"  name = "talks" >			
			<template v-slot:default>
					<image src="../static/navigator/paw.png" mode="" class="mainNav"></image>
					<view  class="navWord">社区</view>					
			</template>
		</navbar>
		<talks :more = "list"></talks>
	</view>

</template>

<script>
import navbar from "../uni_modules/uni-nav-bar/components/uni-nav-bar/uni-nav-bar.vue"
import talks from "./components/talks.vue"
import data from "./data.js"
export default {
		components: {
			navbar,
			talks,
		},
		
		data() {
			return {
				list:[]
			}
		},
		
		onReachBottom() {
			if(this.list == '') {
				this.list = data.list5More1
			}
			else if(this.list == data.list5More1) {
				this.list = data.list5More2
			}
		},

		
	}
</script>

<style>
* {
	margin: 0;
	padding: 0;
}

.community {
	background-color: #f0f0f0;
	background-image: url("../static/background/background.png");
	background-repeat: no-repeat;
	background-size: 80%;
}

.push {
	width: 100%;
	height: 90rpx;
}

.mainNav {
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
</style>