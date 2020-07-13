<template>
	<view class="other">
		<view class="info-box">
			<y-PersionInfo :info="info" @change="handleMenu" />
		</view>
		<view class="diary-box" v-if="cardList && cardList.length > 0">
			<view class="scroll-wrapper">
				<!-- 日记list -->
				<view class="margin-bottom" v-for="(item, index) in cardList" :key="index">
					<y-DiaryItem :obj="item" :radius="true" />
				</view>
				<y-LoadMore :status="loadMoreStatus" />
			</view>
		</view>
		<view class="empty" v-else>
			<y-Empty />
		</view>
	</view>
</template>

<script>
	var that;
	export default {
		data() {
			return {
				info: {},
				cardList: [],
				loadMoreStatus: 2
			};
		},
		onLoad() {
			that = this;
			that.info = that.$store.state.user.userInfo;
			that.cardList = that.$store.state.diary.cardList;
		},
		methods: {
			handleMenu(index) {
				switch (index) {
					case 0:
						uni.navigateTo({
							url: './like'
						});
						break;
					case 1:
						uni.navigateTo({
							url: './fans'
						});
						break;
					case 2:
						uni.navigateTo({
							url: './fans'
						});
						break;
				}
			},
		}
	};
</script>

<style lang="less" scoped>
	.other {
		.info-box {
			padding-bottom: 110rpx;
		}

		.diary-box {
			margin: 0 40rpx;
		}
	}
</style>
