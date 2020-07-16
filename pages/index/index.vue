<template>
	<view class="home">
		<swiper indicator-dots circular>
			<swiper-item v-for="(item,index) in swipers" :key="index">
				<image :src="item.img"></image>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swipers: []
			}
		},
 		onLoad() {
			this.getSwipers()
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
</style>
