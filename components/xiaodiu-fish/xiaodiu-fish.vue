<template name="fish">
	<view class="xd-drift">
		<image style="width: 100%; height: 100%; "    src="../../static/xiaodiu-fish/fish_home.png" ></image>
		 
		<view class="drift-bo1"  :style="{left:(btleft-5)+'px'}" >
			<image    v-for="one in bolist1" class="drift-mbo"     src="../../static/xiaodiu-fish/fish_mbo1.png" ></image>
			
		</view>
		   <view class="drift-bo2"  :style="{left:btleft+'px'}" >
		   	<image    v-for="one in bolist1" class="drift-mbo"     src="../../static/xiaodiu-fish/fish_mbo2.png" ></image>
		   	
		   </view>
		   
		   <image v-for="one in fishlist" class="fish" :style="{left:one.x+'px',top:one.y+'px'}" src="../../static/xiaodiu-fish/fish_fish.png">  </image> 	 
	       <image class="px" src="../../static/xiaodiu-fish/fish_px.png">  </image>
	 	 
		 
	</view>
</template>

<script>
	export default {
	    name: "fish",
	    //属性
		 data () {
		    return {
		      btleft: 0,
			  btleft1:0,
			  bolist1:30,
			  windowWidth:0, 
			  plpadd:1,
			  fishlist:[],
		    }
		  },
	    props: { 
			fishmaxspeed:{
						  type:Number,
						  default : 1,
			} ,
		  bospeed:{
		  			  type:Number,
		  			  default : 1,
		  } ,
		  fishsum:{
		  			  type:Number,
		  			  default : 2,
		  } 
	        
	    },
	    //组件生命周期
	    created:function(e){
			var that=this;
			uni.getSystemInfo({
			    success: function (res) {
			        
					that.windowWidth=res.windowWidth;
					this.btleft=100-res.windowWidth;
					 
			    }
			});
		//初始化鱼的数目
		for(var m=0;m<this.fishsum;m++){
			         var vote = {};
			          vote.x = Math.random()*this.windowWidth;
			          vote.y = 80+Math.random()*140;
					  vote.s=Math.random()*this.fishmaxspeed*10+10;
			          this.fishlist.push(vote);
			 
		}
			
			
	     this.beijing();
		 
	    },
	    methods: {
	        showBt:function(obj){
	         
	        },
			addfish(sum){
				//+鱼的数目
				for(var m=0;m<sum;m++){
					         var vote = {};
					          vote.x = Math.random()*this.windowWidth;
					          vote.y = 80+Math.random()*140;
							  vote.s=Math.random()*this.fishmaxspeed*10+10;
					          this.fishlist.push(vote);
					 
				}
			},
			reducefish(sum){
				//+鱼的数目
				this.fishlist.splice(0,sum);
				// for(var m=0;m<sum;m++){
				// 	   this.fishlist.splice(0,1);
				// 	 
				// }
				return this.fishlist
			},
			beijing:function(){
				
				this.btleft+=this.bospeed;
				 
				if(this.btleft+100>=0) this.btleft=100-this.windowWidth;
				
				
				//鱼游动
				for(var m=0;m<this.fishlist.length;m++){
					this.fishlist[m].x+=this.fishlist[m].s/10;
					if(this.fishlist[m].x>this.windowWidth) this.fishlist[m].x=-30;
				}
				
				var that=this;
				setTimeout(function () {
				  that.beijing();
				}, 100);
			}
	    }
	}
</script>


<style>
.xd-drift{
 
	width:100%;
	height:250px; 
}

 .fish{
	 width:40px;
	 height:30px;
	 position:fixed;
	 bottom:80px;
	 left:260px;
 }
 
 .px{
	 width:30px;
	 height:30px;
	 position:relative;
	 bottom:40px;
	 left:120px;
 }

.drift-bo1{
	position:fixed;
	top:70px;
	left:0;
	width:200%;
	 height: 25px; 
	 overflow:hidden
}

.drift-bo2{
	position:fixed;
	top:80px;
	left:0;
	width:200%;
	 height: 25px; 
	 overflow:hidden
}

.drift-mbo{
	 width: 44px; 
	height: 22px; 
	 
}
 
 
</style>