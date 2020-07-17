<template>
	<view class="news">
		<!-- <view class="news-item" v-for="(item,index) in newsList" :key="index">
			<image :src="item.img_url"></image>
			<view class="right">
				<view class="title">
					{{ item.title }}
				</view>
				<view class="info">
					<text>发表时间：{{ item.add_time }}</text>
					<text>浏览：{{ item.click }}</text>
				</view>
			</view>
		</view> -->
		<newsItem :newsList="newsList" @itemClick="goDetail"></newsItem>
	</view>
</template>

<script>
	import newsItem from '../../components/news-item/news-item.vue'
	
	export default {
		data() {
			return {
				newsList: []
			}
		},
		components: {
			newsItem
		},
		onLoad() {
			this.getNews()
		},
		methods: {
			async getNews() {
				const res = await this.$myRequest({
					url: '/api/getnewslist'
				})
				// console.log(res)
				this.newsList = res.data.message
			},
			goDetail(id) {
				uni.navigateTo({
					url: '/pages/news-detail/news-detail?id=' + id
				})
			}
		}
	}
</script>

<style lang="less">
	.news {
		
	}
</style>
