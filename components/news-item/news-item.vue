<template>
	<view>
		<view class="news-item" v-for="(item,index) in newsList" :key="index" @click="goDetail(item.id)">
			<image :src="item.img_url"></image>
			<view class="right">
				<view class="title">
					{{ item.title }}
				</view>
				<view class="info">
					<text>发表时间：{{ item.add_time| formatDate }}</text>
					<text>浏览：{{ item.click }}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props: ['newsList'],
		filters: {
			formatDate(date) {
				const nDate = new Date(date)
				const year = nDate.getFullYear()
				const month = nDate.getMonth().toString().padStart(2,0)
				const day = nDate.getDay().toString().padStart(2,0)
				return year + '-' + month + '-' + day
			}
		},
		methods: {
			goDetail (id) {
				this.$emit('itemClick', id)
			}
		}
	}
</script>

<style lang="less">
	.news-item {
		display: flex;
		padding: 10rpx 20rpx;
		border-bottom: 1px solid #b50e03;
		image {
			width: 200rpx;
			height: 150rpx;
			min-width: 200rpx;
			max-width: 200rpx;
		}
		.right {
			margin-left: 15rpx;
			display: flex;
			flex-direction: column;
			justify-content: space-between;
			.title {
				font-size: 30rpx;
			}
			.info {
				font-size: 24rpx;
				text:nth-child(2) {
					margin-left: 30rpx;
				}
			}
		}
	}
</style>
