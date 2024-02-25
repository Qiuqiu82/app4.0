<template>
	<div>
		<!-- 小程序名称 -->
		<el-text class="text-top">碳迹汇</el-text>

		<!-- 顶部 -->
		<el-row class="button-row">
			<el-button class="top-button">低碳饮食</el-button>
		</el-row>

		<!-- 顶部右侧 -->
		<el-row class="text-right" @tap="redirectTocall">
			<el-text >倡议</el-text>
		</el-row>

		<!-- 文字链接 -->
		<el-row class="text-center">
			<el-text @click="redirectTomonthvegecheck">每月素食打卡区</el-text>
		</el-row>

		<!-- 点击上传 -->
		<el-row class="text-upload">
			<el-text @click="redirectTomonthvegecheck">（点击上传图片）</el-text>
		</el-row>

		<!-- 进度 -->
		<el-row class="button-row">
			<el-input v-model="days" placeholder="本月打卡天数"></el-input>
			<el-button class="action-button" @click="calculateProgress">查看进度</el-button>
			 <el-button class="action-button" @click="calculatePoints">查看积分</el-button>
		</el-row>	

		<!-- 推荐 -->
		<el-text class="text-center">推荐绿色饮食</el-text>
		
		<!-- 推荐绿色饮食 -->
		<!-- <el-table :data="list" border style="width: 100%" class="centered-table">
			<el-table-column prop="type" label="类别" width="180" />
			<el-table-column prop="effect" label="效用" width="180" />
		</el-table> -->
		<view class="text-list" v-if="textList.length">
			<view class="text-item" v-for="item in textList" :key="item.id">
				<view class="text-content">
					<view class="content">
						<view>{{item.name}}</view>
						<view>{{item.textcontent}}</view>
					</view>
				</view>
			</view>
		</view>
		
	</div>
</template>

<script>
export default {
    data() {
        return {
			textList:[
				{
					name:'蔬菜类',
					textcontent:'富含大量维生素C有益于人体健康，防止坏血病，提高人体免疫力'
				},
				{
					name:'瓜果类',
					textcontent:'富含大量维生素C有益于人体健康，防止坏血病，提高人体免疫力'
				},
				{
					name:'蛋奶类',
					textcontent:'尽量通过蛋奶类饮食代替肉类，既能低碳，又能减少过度摄入肉类饱和脂肪酸对人体的危害'
				}
			],
            days: null,
            progress: 0,
			points: 0// 新增积分字段
        }
    },
    methods: {
        redirectTocall() {
            // 跳转到倡议页面
            uni.navigateTo({
                url: '/pages/call/call'
            });
        },
        redirectTomonthvegecheck() {
            // 跳转到打卡页面
            uni.navigateTo({
                url: '/pages/checkIn/checkIn'
            });
        },
        calculateProgress() {
            if (this.days !== null && !isNaN(this.days) && this.days >= 0) {
                this.progress = (this.days / 25) * 100;
            } else {
                // 输入无效，给出提示或者处理方式
                alert("请输入有效的天数！");
            }
        },
		calculatePoints() {
		    if (this.days !== null && !isNaN(this.days) && this.days >= 0) {
		        if (this.days <= 25) {
		            this.points = this.days * 10;
		        } else {
		            this.points = 25 * 10 + (this.days - 25) * 10;
		        }
		    } else {
		        // 输入无效，给出提示或者处理方式
		        alert("请输入有效的天数！");
		    }
		},
    }
}
</script>

<style scoped>
.text-list {
	color: #333;
	font-size: 28rpx;
	padding-bottom: 80rpx;
}
.text-item {
	display: flex;
	align-items: center;
	background: #fff;
	padding: 25rpx;
	margin-bottom: 8rpx;
	}
.text-content {
	flex: 1;
	display: flex;
	align-items: center;
}
			
.content {
	flex: 1;
	line-height: 50rpx;
}

.action-button {
	padding: 12px 10px;
	border: 2px solid #41a863;
	background-color: #41a863;
	color: #ffffff;
	border-radius: 30px 30px;
	font-size: 16px;
	cursor: pointer;
	transition: background-color 0.3s;
	margin-top: 30px;
}

.button-row {
	display: flex;
	justify-content: space-around;
	margin: 5px;
}

.button-bottom {
	display: flex;
	justify-content: space-around;
	margin: 0px 0px;
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
	margin-top: 30px;
	font-size: 18px
}

.text-upload {
	display: flex;
	justify-content: center;
	margin-top: 10px;
	font-size: 12px
}

.text-top {
	font-weight: bold;
	display: flex;
	font-size: 20px
}

.text-right {
	font-weight: bold;
	display: flex;
	justify-content: flex-end;
	font-size: 20px
}

.title-button {
	padding: 1px 16px;
	border: 2px solid #41a863;
	background-color: transparent;
	color: #41a863;
	border-radius: 8px;
	font-size: 16px;
	cursor: pointer;
	transition: background-color 0.3s;
	margin-top: 2px;
}

.word-button {
	padding: 2px 1px;
	background-color: transparent;
	color: #000000;
	font-size: 8px;
	cursor: pointer;
	transition: background-color 0.3s;
	margin-top: 2px;
}

.centered-table {
  display: flex;
  justify-content: center;
}

</style>