<template>
	<view class="goods_list">
		<goodsList :goodsList="goodsList"></goodsList>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list'
	
	export default {
		data() {
			return {
				pageindex: 1,
				goodsList: []
			}
		},
		components: {
			goodsList
		},
		onLoad() {
			this.getGoodsList()
		},
		methods: {
			// 获取商品列表的数据
			async getGoodsList() {
				const res = await this.$myRequest({
					url: '/api/getgoods?pageindex='+this.pageindex
				})
				// console.log(res)
				this.goodsList = res.data.message
			}
		}
	}
</script>

<style lang="less">
	.goods_list {
		background-color: #eee;
	}
</style>
