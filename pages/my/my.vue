<template>
	<view>
		<tab @btnOk="btnOk" :tabTitle="tabTitle" :leftList="leftList" :centerList="centerList" :rightList="rightList" :activeColor="activeColor"></tab>
	</view>
</template>

<script>
	import tab from 'components/tablist.vue'
	export default {
		components:{
			tab
		},
		data() {
			return {
				tabTitle:[{name:'星级'},{name:'人气'},{name:'房型'},],//tab标题的数组
				leftList:[{name:'二星'},{name:'三星'},{name:'四星'},{name:'五星'}],//左侧内容区域
				centerList:[{name:'垃圾'},{name:'低级'},{name:'中级'},{name:'高级'}],//中间内容区域
				rightList:[{name:'刘德华'},{name:'张学友'},{name:'郭富城'},{name:'黎明'}],//右侧内容区域
				activeColor:['yellow','red'],//高亮颜色(前面是字体颜色后面是背景颜色)
			}
		},
		methods: {
			btnOk(e){//弹框确认事件(第一个参数是索引，第二个参数是所在位置)
				console.log(e,'00000000000000');
			}
		}
	}
</script>

<style>

</style>
