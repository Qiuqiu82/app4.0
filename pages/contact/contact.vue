<template>
	<view>
		<view class="passenger-list" v-if="passengerList.length">
			<view class="passenger-item" v-for="item in passengerList" :key="item.id">
				<image class="icon" src="/static/img/person.png"></image>
				<view class="passenger-content">
					<view class="content">
						<view>姓名：{{item.name}}</view>
						<view>电话：{{item.phone}}</view>
					</view>
					<image class="arrow-icon" src="/static/img/arrow.png"></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				passengerList:[
					{
						name:'客服A',
						phone:'15314562432'
					},
					{
						name:'客服B',
						phone:'18312443432'
					},
					{
						name:'客服C',
						phone:'13312432332'
					}
				]
			}
		},
		methods: {

		}
	}
</script>

<style>
	.passenger-list {
		color: #333;
		font-size: 28rpx;
		padding-bottom: 80rpx;
	}
	
	.passenger-item {
		display: flex;
		align-items: center;
		background: #fff;
		padding: 25rpx;
		margin-bottom: 8rpx;
	}
	
	.icon {
		width: 50rpx;
		height: 50rpx;
		margin-right: 25rpx;
	}
		
	.passenger-content {
		flex: 1;
		display: flex;
		align-items: center;
	}
	
	.content {
		flex: 1;
		line-height: 50rpx;
	}
	
	.arrow-icon {
		margin-right: 10rpx;
		width: 40rpx;
		height: 40rpx;
	}

</style>