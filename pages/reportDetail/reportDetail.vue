<template>
	<view class="container">
		<view class="logo">fdtp</view>
		<view class="title">fundtp 财金直播</view>
		<view class="date">2020.07.17</view>
		<view class="dataList" v-for="a in news" :key="a.title"><fcard :title="a.title" :contents="a.contents"></fcard></view>
		<view class="qrcodeArea">
			<view class="qrcode"><image src="../../static/uview/example/js.png" style="width: 100%;height: 100%;"></image></view>
			<view class="rightSide">
				<view class="text">扫码关注，获取更多资讯</view>
				<view class="website">www.fundtp.com</view>
			</view>
		</view>
	</view>
</template>

<script>
import fcard from './fcard.vue';

export default {
	components: {
		fcard: fcard
	},
	data() {
		return {
			news: [
				{
					title: '要问来了',
					contents: ['在起始页面跳转到test.vue页面并传递参数', '因通联新闻数据分类质量偏差，因此需要重新采集日报所需的新闻因通联新闻数据分类质量偏差，', 'aafffa']
				},
				{ title: '热点聚焦', contents: ['因通联新闻数据分类质量偏差，因此需要重新采集日报所需的新闻因通联新闻数据分类质量偏差2，', 'aaa'] },
				{ title: '国际十月', contents: ['因通联新闻数据分类质量偏差，因此需要重新采集日报所需的新闻因通联新闻数据分类质量偏差4，', 'aaa5'] },
				{ title: '投资理财', contents: ['sssss', 'aaa22'] }
			]
		};
	},
	methods: {}
};
</script>

<style scoped>
.container {
	background-color: #2979ff;
	/* height: 1336rpx; */
	width: 750rpx;
	display: flex;
	flex-direction: column;
	justify-content: center;
}
.dataList{
	margin-top: 40rpx;

}
.logo {
	width: 200rpx;
	height: 200rpx;
	margin-top: 40rpx;
	margin-left: 40rpx;
	background-color: #18b566;
}

.title {
	text-align: center;
	color: white;
	font-weight: 700;
	font-size: 60rpx;
}

.date {
	text-align: center;
	margin-left: 50rpx;
	margin-right: 50rpx;
	background-color: red;
	height: 68rpx;
	line-height: 68rpx;
	color: white;
	font-weight: 400;
	font-size: 40rpx;
}

.qrcodeArea {
	display: flex;
	/* background-color: #19be6b; */
	margin-right: 60rpx;
	height: 120rpx;
	margin-left: 60rpx;
	margin-top: 20rpx;
}

.qrcode {
	width: 120rpx;
	height: 120rpx;
}
.rightSide {
	margin-left: 20rpx;
	display: flex;
	flex-flow: column;
	justify-content: center;
}
</style>
