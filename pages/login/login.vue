<template>
	<view class='login'>
		<swiper vertical="true" style="height: 100vh;">
			<swiper-item>
				<scroll-view>
					<view class='login-tel'>
						<view class='tel-main'>
							<view class='logo'>
								<image class="logo-img" src='../../static/img/logo.png'></image>
							</view>
							<view class="tel" @tap="goLoginTel">手机号注册</view>
							<LoginOther></LoginOther>
								<view class="login-go">
									<view>已有账号,去登录</view>
									<image src="../../static/img/down.png"></image>
								</view>
						</view>
					</view>
				</scroll-view>
			</swiper-item>
			
			<swiper-item>
				<scroll-view>
					<view class='login-tel'>
						<view class='tel-main'>
							<view class="close-center">
								<view class="login-go">
									<image  class='close-img' src="../../static/img/up.png"></image>
									<view>没有账号,去注册</view>
								</view>
								<view></view>
							</view>
							<view class="login-from">
								<view class="login-user">
									<text class='user-text'>账号</text>
									<input type="text" v-model="userName" placeholder="请输入手机号/昵称"/>
								</view>
								<view class="login-user">
									<text class='user-text'>密码</text>
									<input type="text" v-model="userPwd" placeholder="6-16位字符"/>
								</view>
							</view>
							<view class="login-quick">
								<view>忘记密码?</view>
								<view>密码登录</view>
							</view>
							<view class="tel" @tap='submit'>登录</view>
							<view class="reminder">温馨提示:您可以选择免密登录,更加方便</view>
							<LoginOther></LoginOther>
						</view>
					</view>
				</scroll-view>
			</swiper-item>
			
		</swiper>
		
		
		
		
		
	</view>
</template>

<script>
	import LoginOther from '@/components/login/login.vue'
	export default {
		data() {
			return {
				//用户输入的内容
				userName:"",
				userPwd:"",
				//验证规则
				rules:{
					userName:{
						rule:/\S/,
						msg:"账号不能为空"
					},
					userPwd:{
						rule:/^[0-9a-zA-Z]{6,16}$/,
						msg:"密码应该为6-16位字符"
					}
				}
				
			}
		},
		components:{
			LoginOther
		},
		methods: {
			//点击登录
			submit(){
				if(!this.validate('userName')) return ;
				if(!this.validate('userPwd')) return ;
				
				uni.showLoading({
					title:"登录中..."
				})
				
				setTimeout(()=>{
					uni.hideLoading();
					uni.navigateBack({
						delta:1
					})

				},2000)
			},
			//判断验证是否符合要求
			validate(key){
				let bool =true;
				if(!this.rules[key].rule.test(this[key])){
					uni.showToast({
						title:this.rules[key].msg,
						icon:"none"
					})
					bool=false;
					return false;
				}
				return bool;
			},
			//进入手机号注册页面
			goLoginTel(){
				uni.navigateTo({
					url:"/pages/login-tel/login-tel"
				})
			}
		}
	}
</script>

<style scoped>
.login-tel{
	width:100vw;
	height:100vh;
}
.tel-main{
	padding:0 20rpx;
}
.logo{
	padding-top: 50rpx;;
	padding-bottom: 70rpx;
	display:flex;
	justify-content: center;
}
.logo-img{
	height:500rpx;
	width:500rpx;
}
.tel{
	width:100%;
	height:80rpx;
	line-height: 80rpx;
	text-align: center;
	color:#FFFFFF;
	background-color: #248c85;
	border-radius: 40rpx;
}

.login-go{
	display:flex;
	flrx-direction:column;
	justify-content: center;
	align-items: center;
	padding-top:50rpx;
}
.login-go image{
	width:60rpx;
	height:60rpx;
}
/*第二篇*/
.close-center{
	padding:0 20rpx;
}
.close-img{
	width:60rpx;
	height: 60rpx;
}
.login-from{
	padding-top: 150rpx;
}
.login-user{
	font-size: 32rpx;
	padding:10rpx 0;
	display:flex;
	align-items: center;
	border-bottom: 2rpx solid #c1c1c1;
}
.user-text{
	padding-right: 10rpx;
}
.login-quick{
	display:flex;
	justify-content: space-between;
	padding:40rpx 0;
}
.reminder{
	color:#CCCCCC;
	padding:20rpx 0;
	text-align: center;
	font-size: 28rpx;
}
</style>
