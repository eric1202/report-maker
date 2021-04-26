<template>
	<view class="section">
		<!-- <r-canvas ref="rCanvas"></r-canvas> -->

		<u-cell-group :title="item.title" v-for="item in datas" :key="item.groupId">
			<u-cell-item :title="obj.title" v-for="obj in item.contents" :key="obj.index"></u-cell-item>
		</u-cell-group>
	</view>
</template>

<script>
import rCanvas from '@/components/r-canvas/r-canvas.vue';

export default {
	components: {
		rCanvas
	},
	data() {
		return {
			datas: [
				{ groupId: 1, title: '宏观', contents: [{ title: '世纪东方开始了' }, { title: '1111111世纪东方开始了' }] },
				{
					groupId: 2,
					title: '微观',
					contents: [{ title: '世纪东方开始了' }, { title: '世纪东方开始了' }, { title: '世纪东方开始了' }, { title: '1111111世纪东方开始了' }]
				},

				{ groupId: 4, title: '财富圈', contents: [{ title: '世纪东方开始了' }] }
			]
		};
	},
	mounted() {
		console.log('call methord onReady!!');

		this.$nextTick(async () => {
			// 初始化

			await this.$refs.rCanvas.init({
				canvas_id: 'rCanvas'
			});

			// 画图
			await this.$refs.rCanvas
				.drawImage({
					url: '../../static/posterBg.jpeg',
					x: 0,
					y: 0,
					w: 375,
					h: 630
				})
				.catch(err_msg => {
					uni.showToast({
						title: err_msg,
						icon: 'none'
					});
				});

			// 画文字
			await this.$refs.rCanvas
				.drawText({
					text: 'FUNDTP财经早报',
					max_width: 0,
					x: 38,
					y: 90,
					font_color: 'rgb(255, 255, 255)',
					font_size: 30
				})
				.catch(err_msg => {
					uni.showToast({
						title: err_msg,
						icon: 'none'
					});
				});

			await this.$refs.rCanvas.drawText({
				text: '2020.07.28',
				max_width: 0,
				x: 38,
				y: 190,
				font_color: 'rgb(255, 255, 255)',
				font_size: 30
			});

			// // 生成海报
			// await this.$refs.rCanvas.draw(res => {
			// 	//res.tempFilePath：生成成功，返回base64图片
			// 	// 保存图片
			// 	this.$refs.rCanvas.saveImage(res.tempFilePath);
			// });
		});
	}
	// mounted:function(){
	// 	console.log('call methord mounted!!')
	// 	// this.onReady();
	// },
};
</script>

<style></style>
