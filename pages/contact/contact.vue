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
					<image class="arrow-icon" src="/static/img/right.png"></image>
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
						name:'猫',
						phone:'12312432432'
					},
					{
						name:'陈',
						phone:'12312432432'
					},
					{
						name:'周',
						phone:'12312432432'
					}
				]
			}
		},
		methods: {

		}
	}
</script>

<style lang="scss">
	.passenger-list {
		color: #333;
		font-size: 28rpx;
		padding-bottom: 80rpx;

		.passenger-item {
			display: flex;
			align-items: center;
			background: #fff;
			padding: 25rpx;
			margin-bottom: 8rpx;

			.icon {
				width: 50rpx;
				height: 50rpx;
				margin-right: 25rpx;
			}

			.passenger-content {
				flex: 1;
				display: flex;
				align-items: center;

				.content {
					flex: 1;
					line-height: 50rpx;
				}

				.arrow-icon {
					margin-right: 10rpx;
					width: 40rpx;
					height: 40rpx;
				}
			}
		}
	}

	.passenger-add {
		position: fixed;
		bottom: 0;
		background: #1989fa;
		color: #fff;
		width: 100%;
		height: 80rpx;
		font-size: 28rpx;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.edit-content {
		color: #333;
		font-size: 26rpx;
		background: #fff;
		border-radius: 10rpx;
		width: 710rpx;
		padding: 0rpx 20rpx;
		box-sizing: border-box;
		margin: 20rpx auto 0;

		.edit-item {
			display: flex;
			padding: 30rpx 10rpx;
			border-bottom: 1rpx solid #ebedf0;

			.edit-name {
				width: 140rpx;
				display: flex;

				.must {
					color: red;
					margin-right: 4rpx;
				}
			}

			.edit-input {
				flex: 1;
			}
		}

		.edit-item:last-of-type {
			border-bottom: none;
		}
	}

	.edit-default {
		color: #333;
		font-size: 26rpx;
		background: #fff;
		width: 710rpx;
		margin: 20rpx auto 0;
		box-sizing: border-box;
		padding: 20rpx;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.edit-button-content {
		margin: 80rpx 0;

		.edit-button {
			color: #333;
			width: 690rpx;
			height: 80rpx;
			font-size: 26rpx;
			border-radius: 80rpx;
			text-align: center;
			line-height: 80rpx;
			margin: 30rpx auto 0;
			font-weight: bold;
			border: 1rpx solid #dcdee0;
			background: #fff;

			&.save {
				background: #1989fa;
				color: #fff;
				border: none;
				border: 1rpx solid #1989fa;
			}

			&.del {
				background: orangered;
				color: #fff;
				border: none;
				border: 1rpx solid orangered;
			}
		}

	}
</style>