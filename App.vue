<script>
	// #ifdef H5
	import pageAnimation from './components/y-pageAnimation/index.vue'
	// #endif
	export default {
		// #ifdef H5
		mixins: [pageAnimation],
		// #endif
		onLaunch() {
			let that = this;
		}
	};
</script>

<style lang="less">
	@import 'colorui/main.css';
	@import 'colorui/icon.css';
	@import 'colorui/animation.css';
	
	/*每个页面公共css */
	@font-face {
		font-family: 'AliR';
		src: url(https://vkceyugu.cdn.bspapp.com/VKCEYUGU-matchbox/a003f470-a6fa-11ea-a30b-e311646dfaf2.otf);
	}

	@font-face {
		font-family: 'AliM';
		src: url(https://vkceyugu.cdn.bspapp.com/VKCEYUGU-matchbox/9ff65fe0-a6fa-11ea-a30b-e311646dfaf2.otf);
	}

	page {
		--mainColor: #435257;
		--activeColor: #36b39b;
	}

	body {
		font-family: 'AliR';
		background-color: #f5f8f9;
	}

	view {
		box-sizing: border-box;
	}

	.flex-center {
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.mainColor {
		color: var(--mainColor);
	}

	.aColor {
		color: var(--activeColor);
	}
	
	.color-nine{
		color: #999999;
	}

	.main-btn {
		border-radius: 40upx;
		display: flex;
		align-items: center;
		justify-content: center;
		color: var(--mainColor);
		border: 1upx solid var(--mainColor);
		padding: 10rpx 40rpx;
	}

	.active-btn {
		color: #FFFFFF !important;
		background-color: var(--activeColor) !important;
		border: 1upx solid var(--activeColor) !important;
	}

	/* 点赞和评论 */
	.bottom-btn {
		display: flex;

		.btn-item {
			flex: 1;
			color: var(--mainColor);

			.img {
				width: 50rpx;
				height: 50rpx;
				margin-right: 20rpx;
			}
		}
	}
</style>
