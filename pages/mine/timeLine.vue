<template>
	<view class="line-box">
		<template v-if="cardList.length > 0">
			<view class="cu-timeline" v-for="(item,index) in cardList" :key="index">
				<view class="cu-time">{{item.time}}</view>
				<view class="cu-item text-cyan">
					<view class="content">
						<view class="cu-capsule radius">
							<view class="cu-tag bg-cyan">{{item.createTime}}</view>
						</view>
						<view class="margin-top line-text">{{item.title}}</view>
						<scroll-view scroll-x class="img-info nav margin-top" v-if="item.imgList.length > 0" scroll-with-animation>
							<view class="img-box flex-center" v-for="(child,idx) in item.imgList" :key="idx">
								<image :src="child.url" mode="aspectFill" class="img" @tap="ViewImage(item.imgList,idx)"></image>
							</view>
						</scroll-view>
					</view>
				</view>
			</view>
		</template>
		<template v-else>
			<y-Empty />
		</template>

	</view>
</template>

<script>
	var that;
	export default {
		data() {
			return {
				cardList: []
			};
		},
		onLoad() {
			that = this
			that.cardList = that.$store.state.diary.cardList
		},
		methods: {
			// 预览图片
			ViewImage(list, index) {
				let that = this
				let arr = []
				for (let i = 0; i < list.length; i++) {
					arr.push(list[i].url)
				}
				uni.previewImage({
					current: index,
					urls: arr
				})
			},
		}
	}
</script>

<style lang="less" scoped>
	.line-box {
		min-height: 100vh;

		.cu-timeline {

			.content {
				background-color: #f5f8f9;
			}

			.cu-time {
				color: var(--mainColor);
			}

			.line-text {
				color: var(--mainColor);
			}

			.img-info {
				.img-box {
					width: 144rpx;
					height: 144rpx;
					overflow: hidden;
					display: inline-block;
					margin-right: 20rpx;
					border-radius: 16rpx;

					.img {
						height: 100%;
					}
				}
			}
		}
	}
</style>
