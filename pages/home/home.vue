<template>
	<view class="wholeView">
		<!-- segment -->
		<u-sticky><u-subsection :list="list" :current="current" active-color="#8080ff" @change="segmentChange"></u-subsection></u-sticky>

		<!-- popup -->
		<u-popup v-model="show" mode="bottom" height="600px">
			<view class="popupView">
				<h2>选择资讯</h2>
				<input class="typeInput" type="text" value="" placeholder="输入栏目名称" />
				<view class="segment"><u-subsection :list="typeList" :current="columnIndex" active-color="#ff3f80" @change="columnChange"></u-subsection></view>
				<view class="uni-list">
					<checkbox-group @change="checkboxChange">
						<u-cell-group v-for="item in items" :key="item.value">
							<u-cell-item :title="item.name" :arrow="false"><checkbox :value="item.value" :checked="item.checked" /></u-cell-item>
						</u-cell-group>
					</checkbox-group>
				</view>
			</view>
			<button class="confirmNews" @click="clickConfirm()">确认</button>
		</u-popup>

		<view class="contentArea">
			<view v-show="current == 0">
				<u-cell-group v-for="item in datas" :key="item.value"><u-cell-item :title="item.name" :arrow="false"></u-cell-item></u-cell-group>
				<u-button class="createPosterBtn" @click="show = true">创建早报</u-button>
			</view>
			<view v-show="current == 1"><coverList></coverList></view>
			<view v-show="current == 2"><newsList></newsList></view>
		</view>

		<!-- call popup -->
		<!-- <u-section title="今日热门" sub-title="查看更多"></u-section> -->

		<!-- <view class="jx">
			<view class="">
				<h2>编辑精选</h2>
				<h3>无需自选 快速生成</h3>
			</view>
			<text>每日9点更新</text>
		</view> -->
		<button class="createBtn" @click="makeReport()">生成早报</button>
	</view>
</template>

<script>
import newsList from './newsList.vue';
import coverList from './coverList.vue';

export default {
	components: {
		newsList: newsList,
		coverList: coverList
	},
	data() {
		return {
			datas: [],
			show: false,
			list: [{ name: '资讯' }, { name: '封面' }, { name: '其他内容' }],
			typeList: [{ name: '独家' }, { name: '财经' }, { name: '区块' }],
			current: 0,
			columnIndex: 0,
			newsList: []
		};
	},
	computed: {
		// 计算属性的 getter
		items: function() {
			// `this` 指向 vm 实例
			return this.fetchNewsList(this.columnIndex);
		}
	},
	created() {
		this.fetchNewsApi();
	},
	methods: {
		fetchNewsApi() {
			this.newsList = [
				[
					{
						value: 'USA',
						name: '美国'
					},
					{
						value: 'CHN',
						name: '中国'
					},
					{
						value: 'BRA',
						name: '巴西'
					},
					{
						value: 'JPN',
						name: '日本'
					},
					{
						value: 'ENG',
						name: '英国'
					},
					{
						value: 'FRA',
						name: '法国'
					}
				],
				[
					{
						value: 'story',
						name: '股市'
					},
					{
						value: 'money',
						name: '汇率'
					}
				],
				[
					{
						value: 'block',
						name: '布洛克'
					},
					{
						value: 'eth',
						name: '以太坊'
					}
				]
			];
		},
		fetchNewsList(index) {
			return this.newsList[index];
		},
		segmentChange(index) {
			this.current = index;
		},
		columnChange(index) {
			this.columnIndex = index;
		},
		makeReport: function(e) {
			uni.navigateTo({
				url: '../reportDetail/reportDetail?id=222'
			});
		},
		clickConfirm: function(e) {
			this.show = false;
			this.datas = [];

			for (let i = 0; i < this.newsList.length; i++) {
				let arr = this.newsList[i];

				arr.forEach(element => {
					if (element.checked == true) {
						this.datas.push(element);
					}
				});
			}

			// var items = this.fetchNewsList(this.columnIndex);
			// this.datas = items.filter(d => {
			// 	return d.checked == true;
			// });
		},
		checkboxChange: function(e) {
			var items = this.fetchNewsList(this.columnIndex);
			var values = e.detail.value;
			for (var i = 0, lenI = items.length; i < lenI; ++i) {
				const item = items[i];
				if (values.includes(item.value)) {
					this.$set(item, 'checked', true);
				} else {
					this.$set(item, 'checked', false);
				}
			}
		}
	}
};
</script>

<style scoped>
.typeInput {
	width: 90%;
}
.uni-list-cell {
	justify-content: flex-start;
}
.uni-list {
	width: 90%;
}
.createPosterBtn {
	margin: 0 auto;
	width: 80%;
	height: 80%;
}

.segment {
	background-color: #606266;
	width: 90%;
}
.popupView {
	display: flex;
	align-items: center;
	/* justify-content: center; */
	flex-direction: column;
	margin-bottom: 20px;
}
.jx {
	background-color: #606266;
	margin: 10px;
	padding: 10px;
}
.createBtn {
	position: fixed;
	bottom: 0;
	width: 100%;
	height: 44px;
}
.wholeView {
	min-height: 100%;
}

.contentArea {
	position: relative;
	min-height: 100%;
	padding-bottom: 44px;
}
</style>
