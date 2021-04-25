<template>
	<view>
		<u-subsection :list="list" :current="0" active-color="#8080ff"></u-subsection>

		<u-popup v-model="show" mode="bottom" height="600px">
			<view class="popupView">
				<h2>选择资讯</h2>
				<input class="typeInput" type="text" value="" placeholder="输入栏目名称" />
				<view class="segment"><u-subsection :list="typeList" :current="0" active-color="#ff3f80"></u-subsection></view>
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
		<u-button class="createPosterBtn" @click="show = true">创建早报</u-button>

		<u-section title="今日热门" sub-title="查看更多"></u-section>

		<view class="jx">
			<view class="">
				<h2>编辑精选</h2>
				<h3>无需自选 快速生成</h3>
			</view>
			<text>每日9点更新</text>
		</view>

		<button class="createBtn">生成早报</button>
	</view>
</template>

<script>
export default {
	data() {
		return {
			show: false,
			list: [{ name: '资讯' }, { name: '封面' }, { name: '其他内容' }],
			typeList: [{ name: '独家' }, { name: '财经' }, { name: '区块' }],
			current: 0,
			items: [
				{
					value: 'USA',
					name: '美国'
				},
				{
					value: 'CHN',
					name: '中国',
					checked: 'true'
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
			]
		};
	},

	methods: {
		clickConfirm: function(e) {
			this.show = false;
		},
		checkboxChange: function(e) {
			var items = this.items,
				values = e.detail.value;
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
	position: absolute;
	bottom: 0;
	width: 100%;
	height: 44px;
}
</style>
