<template>
	<view>
		<!-- tabs切换栏 -->
		<view style="display: flex;justify-content: space-between;padding: 20rpx 50rpx;font-size: 28rpx;align-items: center;z-index: 999999;">
			<!-- 接收传过来的tab标题数据 -->
			<view :style="cssVars" v-for="(val,index) in tabTitle" :key="index">
				<view @click="active=index" :class="{'active':active===index}" style="display: flex;align-items: center;">
					<view style="margin-right: 10rpx;">{{val.name}}</view>
				</view>
			</view>
		</view>
		<view style="border-bottom: 1px solid rgba(245, 245, 245, 1);height: 10rpx;width: 100%;margin-bottom: 20rpx;"></view>
		<!-- 弹出框左 -->
		<view class="fadeout" v-show="active===0" :style="cssVars" style="background-color: #fff;position: absolute;top: 100rpx;left: 0;width: 100%;z-index: 99999;">
			<view style="padding: 20rpx;display: flex;justify-content: space-between;flex-wrap: wrap;">
				<view @click="Xactive=index" v-for="(val,index) in leftList" :key="index" class="item" :class="{'Nactive':Xactive===index}">
					<view style="font-size: 24rpx;font-weight: 700;text-align: center;">{{val.name}}</view>
				</view>
			</view>
			<view style="border-bottom: 1px solid rgba(245, 245, 245, 1);height: 10rpx;width: 100%;margin-bottom: 20rpx;"></view>
			<!-- 按钮 -->
			<view style="display: flex;justify-content: space-between;margin-top: 3%;padding: 20rpx;">
				<view @click="btnDel('左')" style="color: #8c8c8d;width: 25%;height: 70rpx;text-align: center;
				line-height: 70rpx;border-radius: 5rpx;border: 1px solid #ebedf0;">
					清空
				</view>
				<view @click="btnOk(Xactive,leftList)" style="background-color: rgba(74, 176, 255, 1);color: #fff;width: 25%;
				height: 70rpx;text-align: center;line-height: 70rpx;
				border-radius: 5rpx;">确认</view>
			</view>
		</view>
		<!-- 弹出框中 -->
		<view class="fadeout" v-show="active===1" :style="cssVars" style="background-color: #fff;position: absolute;top: 100rpx;left: 0;width: 100%;z-index: 99999;">
			<view style="padding: 20rpx;display: flex;justify-content: space-between;flex-wrap: wrap;">
				<view @click="Ractive=index" v-for="(val,index) in centerList" :key="index" class="item" :class="{'Nactive':Ractive===index}">
					<view style="font-size: 24rpx;font-weight: 700;text-align: center;">{{val.name}}</view>
				</view>
			</view>
			<view style="border-bottom: 1px solid rgba(245, 245, 245, 1);height: 10rpx;width: 100%;margin-bottom: 20rpx;"></view>
			<!-- 按钮 -->
			<view style="display: flex;justify-content: space-between;margin-top: 3%;padding: 20rpx;">
				<view @click="btnDel('中')" style="color: #8c8c8d;width: 25%;height: 70rpx;text-align: center;
				line-height: 70rpx;border-radius: 5rpx;border: 1px solid #ebedf0;">
					清空
				</view>
				<view @click="btnOk(Ractive,centerList)" style="background-color: rgba(74, 176, 255, 1);color: #fff;width: 25%;height: 70rpx;text-align: center;line-height: 70rpx;
				border-radius: 5rpx;">确认</view>
			</view>
		</view>
		<!-- 弹出框右 -->
		<view class="fadeout" v-show="active===2" :style="cssVars" style="background-color: #fff;position: absolute;top: 100rpx;left: 0;width: 100%;z-index: 99999;">
			<view style="padding: 20rpx;display: flex;justify-content: space-between;flex-wrap: wrap;">
				<view @click="Factive=index" v-for="(val,index) in rightList" :key="index" class="item" :class="{'Nactive':Factive===index}">
					<view style="font-size: 24rpx;font-weight: 700;text-align: center;">{{val.name}}</view>
				</view>
			</view>
			<view style="border-bottom: 1px solid rgba(245, 245, 245, 1);height: 10rpx;width: 100%;margin-bottom: 20rpx;"></view>
			<!-- 按钮 -->
			<view style="display: flex;justify-content: space-between;margin-top: 3%;padding: 20rpx;">
				<view @click="btnDel('右')" style="color: #8c8c8d;width: 25%;height: 70rpx;text-align: center;
				line-height: 70rpx;border-radius: 5rpx;border: 1px solid #ebedf0;">
					清空
				</view>
				<view @click="btnOk(Factive,rightList)" style="background-color: rgba(74, 176, 255, 1);color: #fff;width: 25%;
				height: 70rpx;text-align: center;line-height: 70rpx;
				border-radius: 5rpx;">确认</view>
			</view>
		</view>
		<!-- 搜索结果 -->
		<view v-if="active!==null" @click="active=null" class="mask"></view>
	</view>
</template>

<script>
	export default {
		props:{
			tabTitle:{//tab标题的数组
				type:Array,
				required:true
			},
			leftList:{//左侧内容区域
				type:Array,
				required:true
			},
			centerList:{//中间内容区域
				type:Array,
				required:true
			},
			rightList:{//右侧内容区域
				type:Array,
			},
			activeColor:{//自定义高亮颜色
				type:Array,
				default:()=>{
					return ['#6579F7','#F2F4FF']
				}
			}
		},
		computed:{
			cssVars() {
			    return {
			    "--Fcolor":this.activeColor[0],
				"--Bcolor":this.activeColor[1]
			    };
			 }
		},
		created() {
		},
		data() {
			return {
				active:null,//tab标题高亮
				Xactive:undefined,
				Ractive:undefined,
				Factive:undefined,
			}
		},
		methods: {
			btnOk(e,arr){
				this.active=null
				this.$emit('btnOk',arr[e]?arr[e].name:'')
			},
			btnDel(e){
				this.active=null
				if(e==='左'){
					this.Xactive=undefined
				}else if(e==='中'){
					this.Ractive=undefined
				}else{
					this.Factive=undefined
				}
			}
		},
	}
</script>

<style lang="scss" scoped>
	.item{//数据每一项
		display: flex;
		align-items: center;
		justify-content: center;
		margin-top: 20rpx;
		width: 23%;
		height: 80rpx;
		border-radius: 15rpx;
		background-color: rgba(245, 245, 245, 1);
	}
	.mask{//遮罩
		position: fixed;
		left: 0;
		top: 200rpx;
		width: 100%;
		height: 100%;
		background-color: rgba(0, 0, 0, .8);
	}
	.Nactive{
		background-color:var(--Bcolor,#F2F4FF);
		color:var(--Fcolor,#6579F7) ;
	}
	.active{
		color:var(--Fcolor,#6579F7) ;
		font-weight: 700;
	}
	// 淡出效果
	.fadeout{
		animation: fadeOut 500ms linear;
	}
	@keyframes fadeOut{
		0%{
			opacity: 0;
		}
		100%{
			opacity: 1;
		}
	}
</style>
