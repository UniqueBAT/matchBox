<template>
	<view class="like-wrap">
		<template v-if="cardList && cardList.length > 0">
		<view class="margin-bottom" v-for="(item, index) in cardList" :key="index">
			<y-DiaryItem :obj="item" />
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
				cardList: [],
				startNum: 1
			}
		},
		onLoad() {
			that = this
			that.getDiary()
		},
		methods: {
			getDiary() {
				that.cardList = that.$store.state.diary.cardList
			},
		}
	}
</script>

<style lang="less" scoped>

</style>
