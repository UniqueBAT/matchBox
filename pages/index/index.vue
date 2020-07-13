<template>
	<view class="home">
		<view class="card-bottom">
			<!-- 顶部分页栏 -->
			<view class="top-tab">
				<view :class="['tab-item flex-center', activeTab == index ? 'active' : '']" @tap="handleTab(index)" v-for="(item, index) in tabList" :key="index">{{ item.title }}</view>
			</view>
			<y-Refresh ref="mixPulldownRefresh" :top="100" @refresh="onPulldownReresh">
				<view class="scroll-wrapper">
					<!-- 漂流瓶 -->
					<view v-if="activeTab == 0">
						<view class="margin-bottom" v-for="(item, index) in cardList" :key="index">
							<y-DiaryItem :obj="item" />
						</view>
					</view>
					<!-- 聚集岛 -->
					<view v-else>
						<view class="margin-bottom" v-for="(item, index) in rightList" :key="item.id">
							<y-DiaryItem :obj="item" />
						</view>
					</view>
					<y-LoadMore :status="loadMoreStatus" />
				</view>
			</y-Refresh>
			<!-- 右下角按钮 -->
			<y-Fab :bottom="140" :right="40" :btnList="fabList" @click="handleFab" />
		</view>
	</view>
</template>

<script>
var that;
export default {
	data() {
		return {
			startNum: 0,
			activeTab: 0,
			// tab的名称
			tabList: [
				{
					title: '漂流瓶'
				},
				{
					title: '聚集岛'
				}
			],
			cardList: [],
			rightList: [],
			loadMoreStatus: 1, //0加载前，1加载中，2没有更多了
			//fab的设置
			fabList: [
				{
					bgColor: '#16C2C2',
					text: '发布',
					fontSize: 28,
					color: '#fff'
				},
				{
					bgColor: '#37b59d',
					text: '分享',
					fontSize: 28,
					color: '#fff'
				}
			]
		};
	},
	onLoad() {
		that = this;
		that.loadData('add');
		that.rightList = that.$store.state.diary.rightList
	},
	onReachBottom() {
		that.startNum++;
		//上滑加载
		that.loadData('add');
	},
	methods: {
		toDetails(id){
			uni.navigateTo({
				url: '../diary/details/details?id=' + id 
			})
		},
		toOther(id){
			uni.navigateTo({
				url: '../mine/other/other?id=' + id
			})
		},
		loadData(type) {
			if (type === 'add') {
				// 上拉加载
				let list = that.cardList;
				if (list.length == 8) {
					that.loadMoreStatus = 2;
				} else if (list.length > 0) {
					that.cardList = that.cardList.concat({
						id: 2,
						time: '06-17',
						avatarUrl: 'https://6d61-matchbox-79a395-1302390714.tcb.qcloud.la/matchbox/cat.jpg',
						nickName: '小黄鸭',
						title: '洛稚喜欢盛淮南谁也不知道',
						follow: false,
						isLike: false,
						likeNum: '24',
						commentNum: '0',
						imgList: [
							{
								url: 'https://6d61-matchbox-79a395-1302390714.tcb.qcloud.la/matchbox/1e942ff08083714184afbf42eba0d87.jpg'
							}
						]
					});
				} else {
					that.cardList = that.$store.state.diary.cardList
				}
			} else {
				//下拉刷新
				that.$refs.mixPulldownRefresh && that.$refs.mixPulldownRefresh.endPulldownRefresh();
			}
		},
		//下拉刷新
		onPulldownReresh() {
			that.loadData('refresh');
		},
		handleTab(index) {
			that.activeTab = index;
		},
		//点击右下角tab按钮
		handleFab(e) {
			let index = e.index;
			switch (index) {
				case 0:
					uni.navigateTo({
						url: '../push/push'
					});
					break;
				case 1:
					console.log(1);
					break;
			}
		}
	}
};
</script>

<style lang="less" scoped>
.home {
	padding-top: 120rpx;

	.top-barrage {
		width: 100%;
		height: 320rpx;
		overflow: hidden;
	}

	.card-bottom {
		width: 100%;

		.top-tab {
			display: flex;
			height: 120rpx;
			position: fixed;
			top: 0;
			width: 100%;
			z-index: 100;
			background-color: #ffffff;

			.tab-item {
				flex: 1;
				color: #999;
				border-bottom: 4rpx solid #ececec;
			}

			.active {
				color: var(--mainColor);
				border-bottom: 4rpx solid var(--mainColor);
			}
		}
	}
}
</style>
