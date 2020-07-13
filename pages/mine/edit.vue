<template>
	<view class="edit-box">
		<view class="cu-list menu">
			<view class="cu-item arrow" style="height: 80px;" @tap="ChooseImage">
				<view class="content">头像</view>
				<view class="img-wrap flex-center">
					<image :src="avatarUrl" mode="widthFix" class="img"></image>
				</view>
			</view>
			<view class="cu-item arrow">
				<view class="content">昵称</view>
				<view class="title"><input class="text-input text-grey" type="text" maxlength="6" v-model="nickName" /></view>
			</view>
			<view class="cu-item arrow">
				<view class="content">性别</view>
				<picker mode="selector" :range="sexArr" :value="sex" @change="handleSex">
					<view class="uni-input text-grey">{{ sexArr[sex] }}</view>
				</picker>
			</view>
			<view class="cu-item arrow">
				<view class="content">出生日期</view>
				<picker class="title" mode="date" :value="birthday" start="1992-01-01" end="2030-12-31" @change="bindDateChange">
					<view class="uni-input text-grey">{{ birthday }}</view>
				</picker>
			</view>
			<view class="cu-form-group margin-top"><textarea maxlength="30" @input="inputChange" placeholder="与君共勉"></textarea></view>
		</view>
		<view class="bottom-btn flex-center">
			<view class="btn">保存</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				avatarUrl: require('@/static/logo.png'),
				nickName: '小黄吖',
				motto: '',
				birthday: '1996-12-11',
				sex: 0,
				sexArr: ['小姐姐', '男']
			};
		},
		methods: {
			inputChange(e) {
				this.motto = e.detail.value;
			},
			bindDateChange(e) {
				this.birthday = e.detail.value;
			},
			handleSex(e) {
				this.sex = e.detail.value;
			},
			// 选择图片
			ChooseImage() {
				let that = this
				uni.chooseImage({
					count: 1, //默认9
					sizeType: ['original'], //可以指定是原图还是压缩图，默认二者都有
					sourceType: ['album'], //从相册选择
					success: (res) => {
						if (res.tempFilePaths && res.tempFilePaths.length > 0) {
							that.avatarUrl = res.tempFilePaths[0]
						}
					}
				});
			},
		}
	};
</script>

<style lang="less" scoped>
	.edit-box {
		.content {
			color: #333333;
		}

		.img-wrap {
			width: 100rpx;
			height: 100rpx;
			border-radius: 50%;
			overflow: hidden;

			.img {
				width: 100%;
			}
		}

		.text-input {
			text-align: right;
		}

		.bottom-btn {
			position: fixed;
			bottom: 0;
			width: 100%;
			padding: 20rpx 0;

			.btn {
				border-radius: 40rpx;
				display: flex;
				align-items: center;
				justify-content: center;
				color: var(--mainColor);
				border: 1rpx solid var(--mainColor);
				width: 400rpx;
				height: 80rpx;
			}
		}
	}
</style>
