<template>
	<view class="wrap">
		<view class="pre-box" v-if="!showUploadList">
			<view class="pre-item" v-for="(item, index) in lists" :key="index">
				<image class="pre-item-image" :src="item.url" mode="aspectFill"></image>
			</view>
		</view>
		<u-upload :custom-btn="true" ref="uUpload" :show-upload-list="showUploadList" :action="action"> 
			<view slot="addBtn" class="slot-btn" hover-class="slot-btn__hover" hover-stay-time="150">
				<u-icon class="addIcon" name="plus" size="120" color="#c0c4cc"></u-icon>
			</view>
		</u-upload>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				action: 'http://www.example.com', // 演示地址
				showUploadList: false, 
				// 如果将某个ref的组件实例赋值给data中的变量，在小程序中会因为循环引用而报错
				// 这里直接获取内部的lists变量即可
				lists: []
			}
		},
		// 只有onReady生命周期才能调用refs操作组件
		mounted() {
			// 得到整个组件对象，内部图片列表变量为"lists"
			this.lists = this.$refs.uUpload.lists;
		}
	}
</script>

<style lang="scss" scoped>
	.wrap {
		padding: 24rpx;
	}
	.addIcon{
		left: 375rpx;
		margin-left: 300rpx;
	}
	.slot-btn {

		// width: 90%;
		// height: auto;
		// display: flex;
		// justify-content: center;
		// align-items: center;
		// background: rgb(244, 245, 246);
		border-radius: 10rpx;
		
	}

	.slot-btn__hover {
		background-color: rgb(235, 236, 238);
	}

	.pre-box {
		display: flex;
		align-items: center;
		justify-content: space-between;
		flex-wrap: wrap;
	}

	.pre-item {
		flex: 0 0 98.5%;
		border-radius: 10rpx;
		height: 250rpx;
		overflow: hidden;
		position: relative;
		margin-bottom: 20rpx;
	}

	.pre-item-image {
		width: 100%;
		// height: 140rpx;
	}
</style>