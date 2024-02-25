<template>
	<view class="my">
		<!-- 头部 -->
		<view class="my-header">	
			<view class="header-main">
				<view class="header-config"@tap='goConfig'>
					<image class="config-img" src="../../static/img/config.png" mode=""></image>
				</view>
				<view class="header-logo" @tap='goLogin'><!-- 待替头像 -->
					<image class="logo-img" src="../../static/img/hot1.jpg" mode=""></image>
					<view class="logo-name">用户昵称</view>
				</view>
			</view>
		</view>
		
		<view class="my-content">
				<view class="my-content-item">
					<view>我的收藏</view>
				</view>
				<view class="my-content-item">
					<view>碳碳好友</view>
				</view>
				<view class="my-content-item">
					<view>碳币管理</view>
				</view>
				<view class="my-content-item">
					<view>帮助中心</view>
				</view>
				<view class="my-content-item" @tap='goContact'>
					<view >联系客服</view>
				</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			goConfig(){
				uni.navigateTo({
					url:'/pages/my-config/my-config'
				})
			},
			goLogin(){
				uni.navigateTo({
					url:"/pages/login/login"
				})
			},
			goContact(){
				uni.navigateTo({
					url:"/pages/contact/contact"
				})
			}
		}
	}
</script>

<style>
.my-header{
	background: url(../../static/img/mybg.png) no-repeat;
	width: 100%;
	height: 400rpx;
}
.header-main{
	position:relative;
	top:120rpx;
}
.header-config{
	position:absolute;
	left:40rpx;
}
.header-logo{
	position: absolute;//* 居中 */
	left:50%;
	margin-left:-60rpx;
	width:120rpx;
	height:120rpx;
}
.config-img{
	width:40rpx;
	height:40rpx;
}
.logo-img{
	width:120rpx;
	height:120rpx;
	border:rpx solid #FFFFFF;
	border-radius: 50%;
	background-color: #FFFFFF;
	
}
.logo-name{
	font-weight: bold;
	color:#FFFFFF;
}
.my-content{
	margin:20rpx 0;
	padding:0 20rpx;
}
.my-content-item{
	display:flex;
	justify-content: space-between;
	align-items: center;
	padding:20rpx 0;
	border-bottom: 2rpx solid #CCCCCC;
}
</style>
