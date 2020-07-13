<template>
	<view :class="['card-item',radius ? 'radius' : '']">
		<view class="item-head">
			<view class="left-info">
				<view class="img-wrap flex-center" @tap="toOthers(item.id)">
					<image :src="item.avatarUrl" mode="widthFix" class="avatar"></image>
				</view>
				<view class="head-name">{{ item.nickName }}</view>
			</view>
			<text class="color-nine">{{item.createTime}}</text>
		</view>
		<view class="content" @tap="toDetails(item.id)">
			<view class="text-content">{{ item.title }}</view>
			<view class="img-wrap padding-bottom-lg" v-if="item.imgList.length == 1">
				<view class="img-box">
					<image v-for="(child, idx) in item.imgList" :key="idx" :src="child.url" mode="widthFix" class="img" @tap.stop @tap="ViewImage(idx, item.imgList)"></image>
				</view>
			</view>
			<view class="img-list padding-bottom-lg" v-if="item.imgList.length > 1">
				<view class="img-box" v-for="(child, idx) in item.imgList" :key="idx">
					<image :src="child.url" mode="widthFix" class="img" @tap.stop @tap="ViewImage(idx, item.imgList)"></image>
				</view>
			</view>
			<view class="bottom-btn padding-bottom-sm">
				<view class="btn-item flex-center">
					<image class="img" src="../../static/img/diary/img_say.png" mode="widthFix"></image>
					<text>{{ item.commentNum }}</text>
				</view>
				<view class="btn-item flex-center" @tap.stop @tap="handleLike(item.id, item.isLike, item.likeNum)">
					<image class="img" v-if="!item.isLike" src="../../static/img/diary/img_zan.png" mode="widthFix"></image>
					<image class="img" v-else src="../../static/img/diary/img_zan_1.png" mode="widthFix"></image>
					<text>{{ item.likeNum }}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			obj: {
				type: Object
			},
			radius:{
				type: Boolean,
				default: false
			}
		},
		data() {
			return {
				item: this.obj,
				showPop: false,
				commentList: []
			};
		},
		watch: {
			obj(val) {
				this.list = val;
			}
		},
		methods: {
			handleFollow(id) {
				let that = this;
				that.item.follow = !that.item.follow;
			},
			toDetails(id) {
				uni.navigateTo({
					url: '../../pages/diary/details?id=' + id
				});
			},
			handleLike(id, isLike, likeNum) {
				let that = this;
				if (that.item.isLike) {
					that.item.likeNum--;
				} else {
					that.item.likeNum++;
				}
				that.item.isLike = !that.item.isLike;
			},
			toOthers() {
				uni.navigateTo({
					url: '../../pages/mine/other'
				});
			},
			ViewImage(index, arr) {
				let list = [];
				for (let i = 0; i < arr.length; i++) {
					list.push(arr[i].url);
				}
				uni.previewImage({
					current: index,
					urls: list
				});
			}
		}
	};
</script>

<style lang="less" scoped>
	.radius{
		border-radius: 16rpx;
	}
	.card-item {
		padding: 20rpx 30rpx 0rpx;
		background-color: #ffffff;
		box-shadow: 0 20rpx 40rpx 0 rgba(0, 0, 0, 0.1);

		.item-head {
			display: flex;
			align-items: center;
			width: 100%;
			justify-content: space-between;

			.left-info {
				display: flex;
				align-items: center;

				.img-wrap {
					width: 80rpx;
					height: 80rpx;
					overflow: hidden;
					border-radius: 50%;

					.avatar {
						width: 100%;
						height: 80rpx;
					}
				}

				.head-name {
					padding-left: 40rpx;
					color: #666666;
					font-size: 32rpx;
				}
			}

			.follow-btn {
				width: 140rpx;
				height: 60rpx;
				border: 1rpx solid var(--mainColor);
				color: var(--mainColor);
				border-radius: 40rpx;
			}

			.followed {
				color: #fff;
				background: var(--activeColor);
				border: 1rpx solid var(--activeColor);
			}
		}

		.content {
			.text-content {
				padding: 40rpx 0;
				justify-content: space-between;
				color: var(--mainColor);
				font-size: 30rpx;
				text-align: justify;
			}

			.img-list {
				display: flex;
				flex-flow: row wrap;

				.img-box {
					flex: 0 0 30%;
					margin: 0 1% 1%;
					display: flex;
					align-items: center;
					justify-content: center;
					overflow: hidden;
					height: 200rpx;
					border-radius: 4px;
					background-color: #ececec;

					.img {
						width: 100%;
					}
				}
			}

			.img-wrap {
				.img-box {
					width: 100%;
					max-height: 400rpx;
					overflow: hidden;
					display: flex;
					align-items: center;
				}
			}
		}
	}

	.cont {
		--color: var(--activeColor);
		--count: 1;
	}
</style>
