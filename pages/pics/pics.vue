<template>
	<view class="pics">
		<!-- <scroll-view class="left" scroll-y>
			<view>居家生活</view>
			<view>居家生活</view>
			<view>居家生活</view>
			<view>居家生活</view>
			<view>居家生活</view>
			<view>居家生活</view>
			<view>居家生活</view>
			<view>居家生活</view>
			<view>居家生活</view>
			<view>居家生活</view>
			<view>居家生活</view>
			<view>居家生活</view>
		</scroll-view> -->
		<!-- 左侧导航数据 -->
		<scroll-view class="left" scroll-y>
			<view v-for="(item,index) in cates" :key="index" :class="active === index ? 'active': ''" @click="leftClickHandle(index,item.id)">{{ item.title }}</view>
		</scroll-view>
		
		<!-- 右侧详情数据 -->
		<scroll-view class="right" scroll-y>
			<view  class="item" v-for="(item,index) in secondData" :key="index">
				<image :src="item.img_url" @click="previewImg(item.img_url)"></image>
				<text>{{ item.title }}</text>
			</view>
			<text v-if="secondData.length === 0">暂无数据</text>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cates: [],
				active: 0,
				secondData: []
			}
		},
		onLoad() {
			this.getPicsCate()
		},
		methods: {
			async getPicsCate() {
				const res = await this.$myRequest({
					url: '/api/getimgcategory'
				})
				console.log(res)
				this.cates = res.data.message
				// 根据一级分类获取二级分类数据
				this.leftClickHandle(0,this.cates[0].id)
			},
			async leftClickHandle(index,id) {
				this.active = index
				// 获取右侧的数据
				const res = await this.$myRequest({
					url: '/api/getimages/' + id
				})
				this.secondData = res.data.message
			},
			previewImg(current){
				const urls = this.secondData.map(item => {
					return item.img_url
				})
				uni.previewImage({
					current,
					urls
				})
			}
		}
	}
</script>

<style lang="less">
page {
	height: 100%;
}
.pics {
	height: 100%;
	display: flex;
	.left {
		width: 200rpx;
		height: 100%;
		border-right: 1px solid #eee;
		view {
			height: 60px;
			line-height: 60px;
			color: #333;
			text-align: center;
			font-size: 30rpx;
			border-top: 1px solid #eee;
		}
		.active {
			background:  #b50e03;
			color: #fff;
		}
	}
	.right {
		width: 520rpx;
		height: 100%;
		margin: 10rpx auto;
		.item {
			image {
				width: 520rpx;
				height: 520rpx;
				border-radius: 5px;
			}
			text {
				font-size: 30rpx;
				line-height: 60rpx;
			}
		}
	}
}

</style>
