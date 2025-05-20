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
								name: '二星',
								value: 2
							}, // 新增value属性
							{
								name: '三星',
								value: 3
							},
							{
								name: '四星',
								value: 4
							},
							{
								name: '五星',
								value: 5
							}
						]
					},
					{
						title: '人气',
						list: [{
							name: '垃圾',value: 1
						}, {
							name: '低级',value: 2
						}, {
							name: '中级',value: 3
						}, {
							name: '高级',value: 4
						}]
					},
					{
						title: '房型',
						list: [{
								name: '刘德华',value: 'liu'
							}, {
								name: '张学友',value: 'zhang'
							}, {
								name: '郭富城',value:'guo'
							}, {
								name: '黎明',value:'li'
							},
						]
					},
				],
				activeColor: ['yellow', 'red']
			}
		},
		methods: {
			btnOk(val) {
				console.log(val);
			}
		}
	}
</script>