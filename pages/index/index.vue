<template>
	<view class="home">
		<!-- 轮播图数据 -->
		<swiper indicator-dots circular>
			<swiper-item v-for="(item,index) in swipers" :key="index">
				<image :src="item.img"></image>
			</swiper-item>
		</swiper>
		
		<!-- 导航区域 -->
		<view class="nav">
			<!-- <view class="nav-item">
				<view class="iconfont icon-ziyuan"></view>
				<text>黑马超市</text>
			</view>
			<view class="nav-item">
				<view class="iconfont icon-guanyuwomen"></view>
				<text>联系我们</text>
			</view>
			<view class="nav-item">
				<view class="iconfont icon-tupian"></view>
				<text>社区图片</text>
			</view>
			<view class="nav-item">
				<view class="iconfont icon-shipin"></view>
				<text>学习视频</text>
			</view> -->
			<view class="nav-item" v-for="(item,index) in navs" :key="index" @click="navItemClick(item.path)">
				<view :class="item.icon"></view>
				<text>{{ item.title }}</text>
			</view>
		</view>
		
		
		<!-- 推荐商品区域 -->
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<!-- <view class="goods_list">
				<view class="goods_item" v-for="(item,index) in goodsList" :key="index">
					<image :src="item.img_url"></image>
					<view class="price">
						<text>￥{{ item.sell_price }}</text>
						<text>￥{{ item.market_price }}</text>
					</view>
					<view class="name">
						{{ item.title }}
					</view>
				</view>
			</view> -->
			<goodsList :goodsList="goodsList"></goodsList>
		</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list'
	
	export default {
		data() {
			return {
				swipers: [],
				goodsList: [],
				navs: [
					{
						icon: 'iconfont icon-ziyuan',
						title: '天天超市',
						path: '/pages/goods/goods'
					},
					{
						icon: 'iconfont icon-guanyuwomen',
						title: '联系我们',
						path: '/pages/contact/contact'
					},
					{
						icon: 'iconfont icon-tupian',
						title: '社区图片',
						path: '/pages/pics/pics'
					},
					{
						icon: 'iconfont icon-shipin',
						title: '学习视频',
						path: '/pages/videos/videos'
					}
				]
			}
		},
 		onLoad() {
			this.getSwipers()
			this.getHotGoods()
		},
		components: {
			goodsList
		},
		methods: {
			// 获取轮播图的数据
			async getSwipers() {
				//  uni.request({
				// 	url: 'http://localhost:8082/api/getlunbo',
				// 	success: res => {
				// 		console.log(res)
				// 		if (res.data.status !== 0) {
				// 			return uni.showToast({
				// 				title: '获取轮播图数据失败'
				// 			})
				// 		} else {
				// 			this.swipers = res.data.message
				// 		}
				// 	}
				// })
				
				const res = await this.$myRequest({
					url: '/api/getlunbo'
				})
				// console.log(res)
				this.swipers = res.data.message
			},
			// 获取热门商品列表数据
			async getHotGoods() {
				const res = await this.$myRequest({
					url: '/api/getgoods?pageindex=1'
				})
				// console.log(res)
				this.goodsList = res.data.message
			},
			// 导航点击的处理函数
			navItemClick(url) {
				// console.log(url)
				uni.navigateTo({
					url
				})
			}
		}
	}
</script>

<style lang="less">
	.home {
		swiper {
			width: 750rpx;
			height: 380rpx;
			image {
				width: 100%;
				height: 100%;
			}
		}
	}
	.nav {
		display: flex;
		.nav-item {
			width: 25%;
			text-align: center;
			view {
				width: 120rpx;
				height: 120rpx;
				background: #b50e03;
				border-radius: 60rpx;
				margin: 10px auto;
				line-height: 120rpx;
				color: #fff;
				font-size: ;
			}
			.iconfont {
				font-size: 55rpx;
			}
			text {
				font-size: 30rpx;
			}
		}
	}
	.hot_goods {
		background: #eee;
		overflow: hidden;
		margin-top: 10px;
		.tit {
			height: 50px;
			line-height: 50px;
			color: #b50e03;
			text-align: center;
			letter-spacing: 20px;
			background: #fff;
			margin: 7rpx 0;
		}
		// .goods_list {
		// 	padding: 0 15px;
		// 	display: flex;
		// 	flex-wrap: wrap;
		// 	justify-content: space-between;
		// 	.goods_item {
		// 		background-color: #fff;
		// 		width: 335rpx;
		// 		margin: 10rpx 0;
		// 		padding: 15rpx;
		// 		box-sizing: border-box;
		// 		image {
		// 			width: 80%;
		// 			height: 150px;
		// 			display: block;
		// 			margin: auto;
		// 		}
		// 		.price {
		// 			color: #b50e03;
		// 			font-size: 30rpx;
		// 			margin: 20rpx 0 5rpx 0;
		// 			text:nth-child(2) {
		// 				color: #ccc;
		// 				font-size: 28rpx;
		// 				margin-left: 17rpx;
		// 				text-decoration: line-through;
		// 			}
		// 		}
		// 		.name {
		// 			font-size: 28rpx;
		// 			line-height: 50rpx;
		// 			padding-bottom: 15rpx;
		// 			padding-top: 10rpx;
		// 		}
		// 	}
		// }
	}
</style>
