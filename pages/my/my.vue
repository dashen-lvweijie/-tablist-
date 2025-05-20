<template>
	<view>
		<tablistVue @btnOk="btnOk" :tabData="combinedData" :activeColor="activeColor"></tablistVue>
	</view>
</template>

<script>
	import tablistVue from '../../components/tablist.vue';
	export default {
		components: {
			tablistVue
		},
		data() {
			return {
				combinedData: [{
						title: '星级',
						list: [{
							name: '二星'
						}, {
							name: '三星'
						}, {
							name: '四星'
						}, {
							name: '五星'
						}]
					},
					{
						title: '人气',
						list: [{
							name: '垃圾'
						}, {
							name: '低级'
						}, {
							name: '中级'
						}, {
							name: '高级'
						}]
					},
					{
						title: '房型',
						list: [{
							name: '刘德华'
						}, {
							name: '张学友'
						}, {
							name: '郭富城'
						}, {
							name: '黎明'
						},
						{
							name: '黎明'
						}]
					},
					{
						title: '房型1',
						list: [{
							name: '刘德华1'
						}, {
							name: '张学友1'
						}, {
							name: '郭富城1'
						}, {
							name: '黎明1'
						}]
					}
				],
				activeColor: ['yellow', 'red']
			}
		},
		methods:{
			btnOk(val){
				console.log(val);
			}
		}
	}
</script>