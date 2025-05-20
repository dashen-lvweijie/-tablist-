<template>
	<view>
		<!-- 标题区域 -->
		<view class="tab-header" :style="cssVars">
			<view v-for="(tab, index) in tabData" :key="index" @click="handleTabClick(index)"
				:class="{'active': activeTab === index}">
				{{ tab.title }}
			</view>
		</view>

		<!-- 内容区域 -->
		<view v-show="activeTab !== null" class="tab-content fadeout" :style="cssVars">
			<view class="item-container">
				<view v-for="(item, idx) in currentList" :key="idx" class="list-item" @click="handleSelect(idx)"
					:class="{'Nactive': idx === selections[activeTab]}">
					<text class="item-text">{{ item.name }}</text>
				</view>
			</view>

			<!-- 操作按钮 -->
			<view class="btn-group">
				<view @click="handleClear">清空</view>
				<view @click="handleConfirm">确认</view>
			</view>
		</view>

		<!-- 遮罩层 -->
		<view v-if="activeTab !== null" @click="closePanel" class="mask"></view>
	</view>
</template>

<script>
	export default {
		props: {
			tabData: { // 合并后的数据结构
				type: Array,
				default: () => []
			},
			activeColor: {
				type: Array,
				default: () => ['#6579F7', '#F2F4FF']
			}
		},
		data() {
			return {
				activeTab: null, // 当前激活的tab索引
				selectedIndex: -1, // 当前选中项的索引
				selections: [] // 存储所有选项的选择状态
			}
		},
		created() {
			// 初始化选择状态数组
			this.selections = Array(this.tabData.length).fill(-1)
		},
		computed: {
			cssVars() {
				return {
					"--Fcolor": this.activeColor[0],
					"--Bcolor": this.activeColor[1]
				}
			},
			// 当前显示的内容列表
			currentList() {
				return this.activeTab !== null ?
					this.tabData[this.activeTab].list : []
			}
		},
		methods: {
			handleTabClick(index) {
				this.activeTab = this.activeTab === index ? null : index
				this.selectedIndex = this.selections[index] ?? -1
			},

			handleSelect(index) {
				this.$set(this.selections, this.activeTab, index)
			},

			handleConfirm() {
				const selectedData = this.tabData
					.map((tab, tabIndex) => ({
						tabIndex,
						tabTitle: tab.title,
						selectedItem: tab.list[this.selections[tabIndex]] || null
					}))
					.filter(item => item.selectedItem !== null)

				// 返回两种格式数据
				this.$emit('btnOk', {
					values: selectedData.map(d => d.selectedItem.value), // 返回value数组
					fullData: selectedData // 完整数据
				})

				this.activeTab = null
			},

			handleClear() {
				this.$set(this.selections, this.activeTab, -1)
			},
		}
	}
</script>

<style lang="scss" scoped>
	page {
		padding: 0;
		margin: 0;
		box-sizing: border-box;
	}

	.tab-header {
		display: flex;
		justify-content: space-between;
		padding: 20rpx 50rpx;
		font-size: 28rpx;
		align-items: center;
		z-index: 999999;

		>view {
			display: flex;
			align-items: center;
			transition: all 0.3s;

			&.active {
				color: var(--Fcolor);
				font-weight: 700;
			}
		}
	}

	.tab-content {
		box-sizing: border-box;
		background: #fff;
		position: absolute;
		top: 100rpx;
		left: 0;
		width: 100%;
		z-index: 99999;
		padding: 20rpx;
	}

	.item-container {
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;

		>view {
			width: 23%;
			height: 80rpx;
			margin-top: 20rpx;
			display: flex;
			align-items: center;
			justify-content: center;
			border-radius: 15rpx;
			background: rgba(245, 245, 245, 1);
			font-size: 24rpx;
			font-weight: 700;
			transition: all 0.3s;

			&.Nactive {
				background: var(--Bcolor);
				color: var(--Fcolor);
			}
		}
	}

	.btn-group {
		display: flex;
		justify-content: space-between;
		margin: 30rpx 0;
		padding: 0 20rpx;

		>view {
			width: 45%;
			height: 70rpx;
			text-align: center;
			line-height: 70rpx;
			border-radius: 5rpx;

			&:first-child {
				border: 1px solid #ebedf0;
				color: #8c8c8d;
			}

			&:last-child {
				background: rgba(74, 176, 255, 1);
				color: #fff;
			}
		}
	}

	.mask {
		position: fixed;
		top: 200rpx;
		left: 0;
		width: 100%;
		height: 100%;
		background: rgba(0, 0, 0, 0.8);
	}

	.fadeout {
		animation: fadeOut 500ms linear;
	}

	@keyframes fadeOut {
		0% {
			opacity: 0;
		}

		100% {
			opacity: 1;
		}
	}
</style>