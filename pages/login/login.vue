<template>
	<view class="login-wrap flex-center">
		<image src="@/static/logo.png" mode="widthFix" class="img"></image>
		<button open-type="getUserInfo" @getuserinfo="getUserInfo" class="login-btn flex-center">微信一键登录</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			};
		},
		onLoad() {},
		methods: {
			getUserInfo(e) {
				uni.showLoading({
					title: '登录中...'
				});
				let userInfo = e.mp.detail.userInfo
				uniCloud.callFunction({
					name: 'user-center',
					data: {
						action: 'updateUser',
						params: {
							nickName: userInfo.nickName,
							province: userInfo.province,
							sex: userInfo.gender,
							avatarUrl: userInfo.avatarUrl
						}
					},
					success(e) {
						uni.showModal({
							showCancel: false,
							content: JSON.stringify(e.result)
						})
					},
					fail(e) {
						console.error(e)
						uni.showModal({
							showCancel: false,
							content: '微信登录失败，请稍后再试'
						})
					}
				})
				uni.hideLoading();
			},
		}
	}
</script>

<style lang="less" scoped>
	.login-wrap {
		height: 100vh;
		padding-bottom: 320rpx;
		flex-direction: column;

		.img {
			width: 160rpx;
			height: 160rpx;
		}

		.login-btn {
			width: 500rpx;
			height: 80rpx;
			border-radius: 40rpx;
			background-color: var(--mainColor);
			color: #FFFFFF;
			font-size: 32rpx;
			margin-top: 200rpx;
		}
	}
</style>
