<template>
	<view class="fans-wrap">
		<template v-if="fansList && fansList.length > 0">
			<view class="fans-item" v-for="(item,index) in fansList" :key="index">
				<view class="left-wrap">
					<view class="img-wrap flex-center margin-right" @tap="toOthers">
						<image :src="item.avatar" mode="widthFix" class="avatar"></image>
					</view>
					<text>{{item.name}}</text>
				</view>
				<view :class="['right-btn main-btn',item.isFollow ? 'active-btn' : '']" @tap="handleLike(item.id)">{{item.isFollow ? '已关注' : '关注'}}</view>
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
				fansList: []
			}
		},
		onLoad(options) {
			that = this;
			if(options && options.type && options.type == 0){
				that.fansList = [{
					id: 1,
					avatar: 'https://6d61-matchbox-79a395-1302390714.tcb.qcloud.la/matchbox/avatar.png',
					name: 'xhy',
					isFollow: false
				}, {
					id: 2,
					avatar: 'https://6d61-matchbox-79a395-1302390714.tcb.qcloud.la/matchbox/avatar.png',
					name: '小黄吖',
					isFollow: true
				}]
				uni.setNavigationBarTitle({
				　　title: '关注'
				})
			}else{
				uni.setNavigationBarTitle({
				　　title: '粉丝'
				})
			}
		},
		methods: {
			toOthers(){
				uni.navigateTo({
					url: './other'
				})
			},
			handleLike(id){
				let list = that.fansList
				list.forEach(item => {
					if(item.id == id){
						item.isFollow = !item.isFollow
					}
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.fans-wrap {
		.fans-item {
			padding: 20rpx 30rpx;
			display: flex;
			align-items: center;
			justify-content: space-between;
			background-color: #FFFFFF;
			border-bottom: 1rpx solid #ececec;

			.left-wrap {
				display: flex;
				align-items: center;
				font-size: 28rpx;
				color: var(--mainColor);

				.img-wrap {
					width: 70rpx;
					height: 70rpx;
					border-radius: 50%;
					overflow: hidden;
					border: 1rpx solid #ECECEC;

					.avatar {
						width: 100%;
						height: 100rpx;
					}
				}
			}

			.right-btn {
				width: 170rpx;
			}
		}
	}
</style>
