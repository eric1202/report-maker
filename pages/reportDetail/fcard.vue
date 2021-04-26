<template>
	<view class="container">
		<view class="contents">
			<view class="badge">
				<text class="title">{{ title }}</text>
			</view>
			<view class="contentArea">
				<h4 v-for="(item, index) in contents">{{ index }}.{{ item }}</h4>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	props: {
		title: '',
		contents: [],
	},
	data() {
		return {};
	},
	methods: {}
};
</script>

<style scoped>
.contents {
	display: flex;
	align-items: center;
	flex-direction: column;
	border-radius: 20rpx;
	/* width: 600rpx; */
	/* height: 400rpx; */
	background-color: #ffffff;
	/* margin: 20rpx; */
	margin-left: 40rpx;
	margin-right: 40rpx;
}

.contentArea {
	margin-top: 20rpx;
	padding-left: 40rpx;
	padding-right: 40rpx;
	margin-bottom: 40rpx;
	width: 100%;
}

.badge {
	background-color: red;
	width: 300rpx;
	height: 40rpx;
}
.title {
	display: block;
	color: white;
	text-align: center;
}
h4 {
	color: #000000;
}
</style>
