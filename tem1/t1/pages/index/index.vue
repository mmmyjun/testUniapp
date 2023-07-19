<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
			<!-- #ifdef APP-PLUS -->
			app-plus~~
			<image src="../../static/pink.jpg" mode="widthFix"></image>
			<!-- #endif -->
			<!-- #ifdef MP-WEIXIN -->
			MP-WEIXIN~~~
			<image src="../../static/yellow.jpg" style="width: 30px;height: 30px"></image>
			<!-- #endif -->
			啊啊
		</view>

		<view class="uni-list">
				<view class="uni-media-list" v-for="item in news" @tap="openInfo" :data-newsid="item.id">
					<image :src="item.author_avatar" class="uni-media-list-logo"></image>
					<view class="uni-media-list-body">
						<view class="uni-media-list-text-top">{{item.title}}</view>
						<view class="uni-media-list-text-bottom">{{item.created_at}}</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				news: []
			}
		},
		onLoad() { // 页面加载成功了
			console.log('page index onload..')
			uni.showLoading({
				title: '加载中...'
			})
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news',
				method: 'GET',
				data: {},
				success: res => {
					console.log(res, '打印结果')
					this.news = res.data || [];
					uni.hideLoading();
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {
			openInfo(e) {
				console.log('opening.........',e)
				let newsid = e.currentTarget.dataset.newsid;
				uni.navigateTo({
					url: '../info/info?newsid=' + newsid
				});
			}
		},
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
	.uni-media-list-logo {
		width: 80rpx;
	}
</style>