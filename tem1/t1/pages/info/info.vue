<template>
	<view class="content">
		<view class="title">
			{{title}}
		</view>
		<view class="art-content">
			<rich-text class="richText" :nodes="strings"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: "",
				strings: ''
			}
		},
		onLoad(e) {
			console.log('info onload e', e);
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news/36kr/' + e.newsid,
				method: 'GET',
				data: {},
				success: res => {
					console.log('info页面成功', res);
					this.title = res.data.title;
					this.strings = res.data.content;
				},
				fail: () => {},
				complete: () => {}
			});

			wx.setNavigationBarTitle({
				title: '当前页面' + e.newsid
			})
		},
		methods: {

		}
	}
</script>

<style>
	.content {
		padding: 10upx 2%;
		width: 2%;
		flex-wrap: wrap;
	}

	.title {
		line-height: 2em;
		font-weight: 700;
		font-size: 38upx;
	}

	.art-content {
		line-height: 2em;
	}
</style>