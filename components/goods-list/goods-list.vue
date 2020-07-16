<template>
	<view class="goods_list">
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
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		},
		props: ['goodsList']
	}
</script>

<style lang="less">
	.goods_list {
		padding: 0 15px;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		.goods_item {
			background-color: #fff;
			width: 335rpx;
			margin: 10rpx 0;
			padding: 15rpx;
			box-sizing: border-box;
			image {
				width: 80%;
				height: 150px;
				display: block;
				margin: auto;
			}
			.price {
				color: #b50e03;
				font-size: 30rpx;
				margin: 20rpx 0 5rpx 0;
				text:nth-child(2) {
					color: #ccc;
					font-size: 28rpx;
					margin-left: 17rpx;
					text-decoration: line-through;
				}
			}
			.name {
				font-size: 28rpx;
				line-height: 50rpx;
				padding-bottom: 15rpx;
				padding-top: 10rpx;
			}
		}
	}
</style>
