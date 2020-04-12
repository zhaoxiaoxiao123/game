<template>
	<view>
		<view>
			<fish ref = "fish"  :fishsum="fishsum"  :bospeed="bospeed" :fishmaxspeed="fishmaxspeed" @list="list()"></fish>
		</view>
		<view class="content">
			<view class="fish">
				<span class="sum">{{fishsum}}</span>
				<span class="title">我的金币</span>
			</view>
			<button @click="addfish(sum)" class="add" :disabled="fishsum==0">购买小鱼</button>
			<button @click="reducefish(sum)" class="reduce" :disabled="curr">卖出小鱼</button>
		</view>
	</view>
</template>

<script>
	import fish from "@/components/xiaodiu-fish/xiaodiu-fish.vue"
	export default {
		data() {
			return {
				sum: 1,
				fishsum:5,
				bospeed:2,
				fishmaxspeed:3,
				fishlist:[],
				curr:false
			}
		},
		components:{
			fish
		},
		onLoad() {

		},
		methods: {
			addfish(sum){
				this.$refs.fish.addfish(sum);
				this.fishsum-=sum;
				if(this.fishsum==0){
					uni.showToast({
					    title: '金币不足',
					    duration: 2000,
						image:'../../static/xiaodiu-fish/money.jpg'
					});
				}
			},
			reducefish(sum){
				var list=this.$refs.fish.reducefish(sum);
				this.fishsum+=sum;
				this.fishlist=list
				if(this.fishlist.length==0) {
					this.curr=true;
					uni.showToast({
					    title: '小鱼不足',
					    duration: 2000,
						image:'../../static/xiaodiu-fish/fish_fish.png'
					});
				}
			},
			
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content:center;
		padding:20rpx 40rpx;
		font-size: 15rpx;
	}

	.fish {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: space-between;
	}
	
	.add{
		border-radius: 50rpx;
		background-color:#4CD964;
	}
	
	.reduce{
		border-radius:50rpx;
		background-color: #DD524D;
	}
	
	.add,.reduce{
		font-size: 35rpx;
	}
	
	.title{
		font-size: 30rpx;
	}
	
	.sum{
		font-size: 55rpx;
		font-weight: bold;
	}
</style>
