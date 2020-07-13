<template>
	<view class="mine-wrap">
		<view class="info-box">
			<y-PersionInfo :info="info" @change="handleMenu" />
		</view>
		<view class="mine-menu-list">
			<view class="cu-form-group mainColor" @tap="toTimeLine">
				<view class="title">碎碎念</view>
				<text class="cuIcon-right "></text>
			</view>
			<view class="cu-form-group mainColor" @tap="handleEdit">
				<view class="title">编辑资料</view>
				<text class="cuIcon-right"></text>
			</view>
			<!-- #ifdef MP-WEIXIN -->
			<button open-type="contact" class="cu-form-group mainColor">
				<view class="title">我的客服</view>
				<text class="cuIcon-right"></text>
			</button>
			<!-- #endif -->
			<view class="cu-form-group mainColor" @tap="handleMoney">
				<view class="title">赞赏作者</view>
				<text class="cuIcon-right"></text>
			</view>
		</view>
	</view>
</template>

<script>
	var that;
	export default {
		data() {
			return {
				info: {
					gender: 0,
					avatarUrl: 'https://6d61-matchbox-79a395-1302390714.tcb.qcloud.la/matchbox/huochai.jpg',
					nickName: '小黄鸭'
				}
			};
		},
		onLoad() {
			that = this;
			that.getUserInfo()
			let info = that.$store.state.user.userInfo
			console.log(info)
			if (info.avatarUrl) {
				that.info = info;
			}
		},
		methods: {
			getUserInfo() {

			},
			handleMenu(index) {
				switch (index) {
					case 0:
						uni.navigateTo({
							url: './like'
						});
						break;
					case 1:
						uni.navigateTo({
							url: './fans?type=' + 0
						});
						break;
					case 2:
						uni.navigateTo({
							url: './fans?type=' + 1
						});
						break;
				}
			},
			handleMoney() {
				let list = ['https://vkceyugu.cdn.bspapp.com/VKCEYUGU-matchbox/ce488c20-aacd-11ea-a30b-e311646dfaf2.jpg'];
				uni.previewImage({
					current: 0,
					urls: list
				});
			},
			toTimeLine() {
				uni.navigateTo({
					url: './timeLine'
				});
			},
			handleEdit() {
				uni.navigateTo({
					url: './edit'
				});
			}
		}
	};
</script>

<style lang="less" scoped>
	.mine-wrap {
		.info-box {
			padding-bottom: 100rpx;
		}

		.mine-menu-list {
			display: flex;
			flex-direction: column;

			.cu-form-group {
				width: 100%;
				border-bottom: 1px solid #ececec !important;

				&::after {
					border: none !important;
				}
			}
		}
	}
</style>
