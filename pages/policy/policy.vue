<template>
	<view>
		<el-text class="text-top">碳迹汇</el-text>
		<!-- 顶部 -->
		<el-row class="button-row">
			<el-button class="top-button">政策导向</el-button>
		</el-row>
		<!-- 政策文字 -->
		<view class="policy-list" v-if="policyList.length">
			<view class="policy-item" v-for="item in policyList" :key="item.id">
				<view class="policy-content">
					<view class="content">
						<view>{{item.name}}</view>
						<view>{{item.policycontent}}</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				policyList:[
					{
						name:'党政方针',
						policycontent:'党和国家对减碳和环境治理的最新政策，指导绿色产业和减碳工作实施'
					},
					{
						name:'激励政策',
						policycontent:'探索个人碳配额金融激励措施，将个人生活和消费行为与减碳相联系，推动民众重视减碳;制定相关激励政策，呼吁全民参与，提高全民绿色消费意识。'
					},
					{
						name:'分配标准',
						policycontent:'根据年度个人生活碳排放数据监测，确认个人碳配额范围，为居民个体设置整体碳排放量限制，引导民众主动选择低碳生活消费方式'
					}
				],
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>
/* 顶部 */
.button-row {
	display: flex;
	justify-content: space-around;
	margin: 5px;
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
.text-top {
	font-weight: bold;
	display: flex;
	font-size: 20px
}
/* 文字样式 */
.policy-list {
	color: #333;
	font-size: 28rpx;
	padding-bottom: 80rpx;
}
.policy-item {
	display: flex;
	align-items: center;
	background: #fff;
	padding: 25rpx;
	margin-bottom: 8rpx;
	}
.policy-content {
	flex: 1;
	display: flex;
	align-items: center;
}		
.content {
	flex: 1;
	line-height: 50rpx;
}
</style>
