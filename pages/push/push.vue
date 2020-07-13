<template>
	<view class="publish-wrap bg-white">
		<view class="input-box padding-sm">
			<textarea class="area-top" placeholder="碎碎念..." v-model="content"></textarea>
		</view>
		<view class="cu-form-group img-box">
			<view class="next-title">上传图片（最多9张）</view>
			<view class="img-wrap margin-none">
				<view class="grid col-4 grid-square flex-sub padding-top-lg">
					<view class="bg-img" v-for="(item,index) in imgList" :key="index">
						<image :src="imgList[index]" mode="aspectFill" @tap="ViewImage(index)" class="img-item"></image>
						<image src="@/static/img/publish/img_close.png" @tap.stop="DelImg" :data-index="index" mode="widthFix" class="close-img"></image>
					</view>
					<view class="add-img" @tap="ChooseImage" v-if="imgList.length<9">
						<text class='cuIcon-add link-color'></text>
					</view>
				</view>
			</view>
		</view>
		<view class="bottom-btn flex-center">
			<view class="btn">发布</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				imgList: [],
				content: ''
			};
		},
		methods: {
			// 选择图片
			ChooseImage() {
				let that = this
				uni.chooseImage({
					count: 9, //默认9
					sizeType: ['original'], //可以指定是原图还是压缩图，默认二者都有
					sourceType: ['album'], //从相册选择
					success: (res) => {
						if (that.imgList.length != 0) {
							that.imgList = that.imgList.concat(res.tempFilePaths)
						} else {
							that.imgList = res.tempFilePaths
						}
					}
				});
			},
			//显示删除弹窗
			DelImg(e) {
				let that = this
				that.imgList.splice(e.currentTarget.dataset.index, 1)
			},
			// 预览图片
			ViewImage(index) {
				let that = this
				uni.previewImage({
					current: index,
					urls: that.imgList
				})
			},
		}
	}
</script>

<style lang="less" scoped>
	.publish-wrap {
		.input-box {
			.area-top {
				width: 100%;
				box-shadow: inset 0 -1px 0 0 #ECECEC;
				min-height: 280rpx;
			}
		}

		.img-box {
			padding: 30rpx;
			display: flex;
			flex-direction: column;
			margin-top: 20rpx;
			margin-bottom: 160rpx;

			.next-title {
				width: 100%;
				font-size: 36rpx;
				color: var(--mainColor);
			}

			.font-red {
				color: #ff0000;
			}

			.img-wrap {
				width: 100%;
				font-size: 28rpx;
				line-height: 44rpx;
				color: #999999;
				margin: 20rpx 0;
			}

			.add-img {
				border: 4rpx dashed #999;
				font-size: 40rpx;
			}
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
				color: #FFFFFF;
				border: 1rpx solid var(--activeColor);
				background-color: var(--activeColor);
				box-shadow: 0 1px 10px 0px var(--activeColor);
				width: 400rpx;
				height: 80rpx;
			}
		}
	}

	.bg-img {
		overflow: visible !important;

		.img-item {
			border-radius: 20rpx;
		}

		.close-img {
			position: absolute;
			width: 36rpx !important;
			top: -18rpx;
			right: -18rpx;
		}
	}
</style>
