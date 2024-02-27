<template>
	<view class="content">
		<h1 class="wrapper">碳际汇</h1>
		<h4 class="title">
			<!-- <el-image style="width: 30px;height: 30px;" :src="img" alt="衣服图片"></el-image> -->
			低碳衣着
		</h4>

		<view id="chart_one">
			<view style="text-align: center;margin: 30rpx 0 65rpx 0;">
				<view style="font-size: 36rpx;font-weight: bold;">月购物衣服数</view>
				<view style="font-size: 28rpx;color: #666;margin-top: 10rpx;">衣服类别分布</view>
			</view>
			<view class="add" @click="add">添加数据</view>
			<view>
				<canvas canvas-id="myid" id="myid" class="charts" @tap="tap" />
			</view>
		</view>

		<view class="title2">点击查看您的超额比(跳转)</view>
		<view class="title3">推荐减排品牌</view>
		<view>
			<ul style="margin-left: 30rpx;">
				<li>
					<span class="hex first"><span class="hexIn"></span></span>
				</li>
				<li>
					<span class="hex two"><span class="hexIn"></span></span>
				</li>
				<li>
					<span class="hex three"><span class="hexIn"></span></span>
				</li>
			</ul>
			<view class="bigcircle">
				<view class="smallcircle">
					<span>推荐衣物</span>
				</view>
			</view>
		</view>
		<u-popup :show="dialogFormVisible" mode="center" length="60%" @close="closepop" border-radius="14">
			<view class="rele-Popup">
				<view class="title-head">衣物数据</view>
				<u--form labelPosition="left">
					<u-form-item :label="item.name" borderBottom ref="item1" v-for="(item,index) in clothingData"
						:key="index">
						<u--input v-model="item.value" type="number"></u--input>
					</u-form-item>
				</u--form>
				<view class="buttom-c" @click="renderChart">确定</view>
			</view>
		</u-popup>
	</view>
</template>

<script>
	import uCharts from '@/node_modules/@qiun/ucharts/u-charts';
	var uChartsInstance = {};
	export default {
		data() {
			return {
				dialogFormVisible: false,
				// 模拟数据，替换为你的实际数据
				clothingData: [{
						name: "T恤",
						value: 20,
						labelText: "T恤"
					},
					{
						name: "裤子",
						value: 30,
						labelText: "裤子"
					},
					{
						name: "外套",
						value: 40,
						labelText: "外套"
					},
					// 添加其他类别和对应的购物数量
				],
				// img


				cWidth: 676,
				cHeight: 500
			};
		},
		mounted() {
			// // 使用ECharts初始化图表
			// this.initClothingPieChart();
		},

		onReady() {
			//这里的 750 对应 css .charts 的 width
			this.cWidth = uni.upx2px(676);
			//这里的 500 对应 css .charts 的 height
			this.cHeight = uni.upx2px(500);
			this.getServerData();
		},
		methods: {
			add() {
				this.dialogFormVisible = true
			},
			getServerData() {
				//模拟从服务器获取数据时的延时
				setTimeout(() => {
					//模拟服务器返回数据，如果数据格式和标准格式不同，需自行按下面的格式拼接
					let res = {
						series: [{
							data: this.clothingData
						}]
					};
					this.drawCharts('myid', res);
				}, 500);
			},
			drawCharts(id, data) {
				const ctx = uni.createCanvasContext(id, this);
				uChartsInstance[id] = new uCharts({
					type: "pie",
					context: ctx,
					width: this.cWidth,
					height: this.cHeight,
					series: data.series,
					animation: true,
					background: "#FFFFFF",
					color: ["#1890FF", "#91CB74", "#FAC858", "#EE6666", "#73C0DE", "#3CA272", "#FC8452", "#9A60B4",
						"#ea7ccc"
					],
					padding: [5, 5, 5, 5],
					enableScroll: false,
					extra: {
						pie: {
							activeOpacity: 0.5,
							activeRadius: 10,
							offsetAngle: 0,
							labelWidth: 15,
							border: false,
							borderWidth: 3,
							borderColor: "#FFFFFF"
						}
					}
				});
			},
			tap(e) {
				uChartsInstance[e.target.id].touchLegend(e);
				uChartsInstance[e.target.id].showToolTip(e);
			},


			// 渲染表格
			renderChart() {
				this.dialogFormVisible = false
				//这里的 750 对应 css .charts 的 width
				this.cWidth = uni.upx2px(720);
				//这里的 500 对应 css .charts 的 height
				this.cHeight = uni.upx2px(500);
				this.clothingData.map(item => {
					item.value = Number(item.value)
				})
				console.log(this.clothingData, "cldata");
				this.getServerData();
			},
			// initClothingPieChart() {
			// 	// 基于准备好的dom，初始化echarts实例
			// 	const myChart = echarts.init(document.getElementById("clothingPieChart"));

			// 	// 指定图表的配置项和数据
			// 	const option = {
			// 		title: {
			// 			text: "月购物衣服数",
			// 			subtext: "衣服类别分布",
			// 			x: "center",
			// 		},
			// 		tooltip: {
			// 			trigger: "item",
			// 			formatter: "{a} <br/>{b}: {c} ({d}%)",
			// 		},
			// 		legend: {
			// 			orient: "vertical",
			// 			left: 10,
			// 			data: this.clothingData.map((item) => item.name),
			// 		},
			// 		series: [{
			// 			name: "购物数量",
			// 			type: "pie",
			// 			radius: "55%",
			// 			center: ["50%", "60%"],
			// 			data: this.clothingData,
			// 			emphasis: {
			// 				itemStyle: {
			// 					shadowBlur: 10,
			// 					shadowOffsetX: 0,
			// 					shadowColor: "rgba(0, 0, 0, 0.5)",
			// 				},
			// 			},
			// 		}, ],
			// 	};

			// 	// 使用刚指定的配置项和数据显示图表。
			// 	myChart.setOption(option);
			// },
		},
	};
</script>

<style lang="scss">
	.rele-Popup {
		padding: 24rpx;
		width: 90vw;

		.title-head {
			font-size: 36rpx;
			color: #3c3a3a;
			padding-bottom: 20rpx;
		}

		.buttom-c {
			color: white;
			background: rgba(254, 114, 0, 1);
			width: max-content;
			padding: 20rpx 20rpx;
			margin: auto;
			border-radius: 25rpx;
			font-size: 32rpx;
			width: 50%;
			text-align: center;
			margin-top: 20rpx;
		}
	}

	.content {
		position: relative;
		// min-width: 500px;

		// background-color: pink;
		.wrapper {
			margin: 20rpx 0px 0px 175rpx;
			background-image: -webkit-linear-gradient(top, #7c7c7c, #576667, #aa9c98);
			-webkit-background-clip: text;
			-webkit-text-fill-color: transparent;
			letter-spacing: 2px;
			color: #a00000;
			text-align: left;
			/* 文字设为透明 */
			font-size: 48rpx;
			font-weight: bold;
		}

		.title {
			margin: 0;
			text-align: center;
			font-size: 48rpx;
			letter-spacing: 8rpx;
			font-weight: 400;
			color: #6c6c6c;
			font-family: "Arial", "Verdana", "Helvetica", sans-serif;
			display: flex;
			align-items: center;
			justify-content: center;

			image {
				width: 40rpx;
				height: 40rpx;
			}
		}

		#chart_one {
			width: 385px;
			margin: 40rpx auto;
			border: 1rpx solid #ccc;
			height: 400px;
			box-shadow: 0 0 2px 2px #ccc;
			// position: relative;

			.add {
				position: absolute;
				top: 200rpx;
				left: 55rpx;
				width: 160rpx;
				height: 50rpx;
				border: 1rpx solid #ccc;
				text-align: center;
				line-height: 50rpx;
				font-size: 26rpx;
				border-radius: 8rpx;
			}
		}

		.title2 {
			margin-top: 30rpx;
			text-align: center;
			font-size: 28rpx;
			letter-spacing: 2px;
			font-weight: 700;
		}

		.title3 {
			margin-top: 40rpx;
			font-size: 32rpx;
			letter-spacing: 8rpx;
			font-weight: 700;
			text-align: center;
			color: royalblue;
		}

		ul {
			position: relative;
			width: 180rpx;
			display: flex;
			flex-wrap: wrap;
			top: 30rpx;
		}

		ul li {
			// float: left;
			border-radius: 1px;
		}

		.hex {
			overflow: hidden;
			display: block;
			width: 70rpx;
			height: 78rpx;
			transform: rotate(-60deg) skewY(30deg);
			border-radius: 1px;
		}

		.hexIn {
			background-color: #ccc;
			display: block;
			width: 70rpx;
			height: 78rpx;
			line-height: 78rpx;
			text-align: center;
			border-radius: 1px;
			transform: skewY(-30deg) rotate(60deg);
		}

		.first {
			span {
				background-color: #27da9d;
				filter: brightness (12)
			}
		}

		.two {
			span {
				background-color: #f6c428;
			}
		}

		.three {
			position: relative;
			top: -25%;
			left: 45%;

			span {
				background-color: #4b7cfa;
			}
		}

		.bigcircle {
			position: relative;
			top: -150rpx;
			left: 400rpx;
			width: 150rpx;
			height: 150rpx;
			border-radius: 50%;
			background-color: #b8d2f5;
			margin-left: 150rpx;

			.smallcircle {
				position: relative;
				top: 10rpx;
				width: 120rpx;
				height: 120rpx;
				border-radius: 50%;
				background-color: #3b7deb;
				text-align: center;
				line-height: 120rpx;
				font-size: 24rpx;

				text {
					position: absolute;
					left: 50%;
					top: 50%;
					transform: translate(-50%, -50%);
					font-size: 14px;
					font-weight: 700;
				}
			}
		}

		.charts {
			width: 676rpx;
			height: 500rpx;
		}

		// .qq {

		// }
	}
</style>