<template>
	<view class="goods_list">
		<goodsList :goodsList="goodsList" @itemClick="goGoodsDetail"></goodsList>
		<view class="isOver" v-if="flag">-----我是有底线的-----</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list'
	
	export default {
		data() {
			return {
				pageindex: 1,
				goodsList: [],
				flag: false
			}
		},
		components: {
			goodsList
		},
		onLoad() {
			this.getGoodsList()
		},
		onReachBottom() {
			if (this.goodsList.length < this.pageindex*10 ) return this.flag = true
			// console.log('触底了')
			this.pageindex++
			this.getGoodsList()
		},
		onPullDownRefresh() {
			console.log('下拉刷新')
			this.pageindex = 1
			this.goodsList = []
			this.flag = false
			setTimeout(() =>{
				this.getGoodsList(() => {
					uni.stopPullDownRefresh()
				})
			}, 1000)
		},
		methods: {
			// 获取商品列表的数据
			async getGoodsList(callback) {
				const res = await this.$myRequest({
					url: '/api/getgoods?pageindex='+this.pageindex
				})
				// console.log(res)
				// this.goodsList = res.data.message
				// 进行数据的拼接，将老数据与响应获得的数据进行拼接
				this.goodsList = [...this.goodsList,...res.data.message]
				callback && callback()
			},
			// 导航到商品详情页
			goGoodsDetail(id) {
				uni.navigateTo({
					url: '/pages/goods-detail/goods-detail?id=' + id
				})
			}
		}
	}
</script>

<style lang="less">
	.goods_list {
		background-color: #eee;
	}
	.isOver {
		width: 100%;
		height: 50px;
		line-height: 50px;
		text-align: center;
		// background: #fff;
		font-size: 28rpx;
	}
</style>
