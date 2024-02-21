<template>
	<div>
		<!-- 小程序名称 -->
		<el-text class="text-top">碳迹汇</el-text>

		<!-- 顶部 -->
		<el-row class="button-row">
			<el-button class="top-button">低碳出行</el-button>
		</el-row>

		<!-- 文字链接 -->
		<el-row class="text-center">
			<img class="icon" src="../../static/img/汽车行程.png" alt="汽车行程图标" @click="showDialog('noteway')">
			<el-text @click="showDialog('noteway')">今日汽车行程</el-text>
		</el-row>
		<el-row class="text-center">
			<img class="icon" src="../../static/img/自行车.png" alt="自行车图标" @click="showDialog('notetime')">
			<el-text @click="showDialog('notetime')">短途自行车，步行行程</el-text>
		</el-row>
		<el-row class="text-center">
			<img class="icon" src="../../static/img/高铁.png" alt="高铁图标" @click="showDialog('carbonnumber')">
			<el-text @click="showDialog('carbonnumber')">长途汽车高铁行程</el-text>
		</el-row>

		<!-- 矩形按钮 -->
		<el-row class="button-row">
			<el-button class="action-button" @click="showDialog('noteway')">路程记录</el-button>
			<el-button class="action-button" @click="showDialog('carbonnumber')">减碳排量</el-button>
		</el-row>
		

		<!-- 文字链接 -->
		<el-row class="text-center">
			<el-text>电动汽车出行推荐一览（暂未开放）</el-text>
		</el-row>
	</div>
</template>


<script>
export default {
	data() {
		return {
			dialogVisible: false,
			dialogType: '',
			inputData: null,
			todayCarway: 0,
			bikeway: 0,
			longtravel: 0
		}
	},
	methods: {
		redirectTonoteway() {
			uni.navigateTo({
				url: '/pages/noteway/noteway'
			});
		},
		redirectTonotetime() {
			uni.navigateTo({
				url: '/pages/notetime/notetime'
			});
		},
		redirectTotimeclassify() {
			uni.navigateTo({
				url: '/pages/timeclassify/timeclassify'
			});
		},
		redirectTocarbonnumber() {
			uni.navigateTo({
				url: '/pages/carbonnumber/carbonnumber'
			});
		},
		redirectTotodaycarway() {
			uni.navigateTo({
				url: '/pages/todaycarway/todaycarway'
			});
		},
		redirectTobikeway() {
			uni.navigateTo({
				url: '/pages/bikeway/bikeway'
			});
		},
		redirectTolongtravel() {
			uni.navigateTo({
				url: '/pages/longtravel/longtravel'
			});
		},
		
		showDialog(type) {
			this.dialogVisible = true;
			this.dialogType = type;
		},
		handleConfirm() {
			switch (this.dialogType) {
				case 'noteway':
					console.log('路程记录输入的数据为：', this.inputData);
					break;
				case 'notetime':
					console.log('时长记录输入的数据为：', this.inputData);
					break;
				case 'timeclassify':
					console.log('时间分类输入的数据为：', this.inputData);
					break;
				case 'carbonnumber':
					let carbonOffset = (0.01 * this.todayCarway + 0.001 * this.bikeway + 0.01 * this.longtravel) * this.inputData;
					this.inputData = carbonOffset;
					console.log('减碳排量为：', carbonOffset);
					break;
				default:
					break;
			}
			this.dialogVisible = false;
		}
	}
}
</script>

<style>
.action-button {
	padding: 12px 10px;
	border: 2px solid #41a863;
	background-color: #41a863;
	color: #ffffff;
	border-radius: 30px 30px;
	font-size: 16px;
	cursor: pointer;
	transition: background-color 0.3s;
	margin-top: 50px;
}

.button-row {
	display: flex;
	justify-content: space-around;
	margin: 0px 10px;
}

.top-button {
	padding: 1px 24px;
	border: 2px solid #41a863;
	background-color: transparent;
	color: #41a863;
	border-radius: 8px;
	font-size: 16px;
	cursor: pointer;
	transition: background-color 0.3s;
}

.text-center {
	font-weight: bold;
	display: flex;
	justify-content: center;
	margin-top: 40px;
	font-size: 18px
}

.text-top {
	font-weight: bold;
	display: flex;
	font-size: 20px
}
.icon {
    width: 50px; /* 设置图片宽度 */
    height: 80rpx; 
}
</style>
