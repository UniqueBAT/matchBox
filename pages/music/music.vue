<template>
	<view class="music-wrap">
		<view class="music-img flex-center">
			<image src="https://6d61-matchbox-79a395-1302390714.tcb.qcloud.la/matchbox/lonely.jpg" mode="widthFix" class="img"></image>
		</view>
		<view class="music-desc">
			<view class="music-title padding-lg">虽然你我会下落不明，你知道我曾为你动过情</view>
		</view>
		<view class="bottom-music">
			<slider class="audio-slider" backgroundColor="#999" activeColor="#37b59d" block-size="12" v-model="currentTime" :max="audioTime"
			 @changing="changing" @change="change"></slider>
			<view class="control-btn">
				<image src="../../static/img/music/img_play.png" @tap="handlePlay" v-if="!audioPlay" mode="widthFix" class="img"></image>
				<image src="../../static/img/music/img_pause.png" @tap="handlePlay" v-else mode="widthFix" class="img"></image>
			</view>
		</view>
	</view>
</template>

<script>
	var that;
	const audioContext = uni.createInnerAudioContext();
	export default {
		data() {
			return {
				audioTime: '0', //音频时长
				currentTime: '0', //当前音乐播放位置
				audioPlay: false,
				audioUrl: 'https://vkceyugu.cdn.bspapp.com/VKCEYUGU-matchbox/63a5fc40-aa41-11ea-b94e-47f67ecf8268.flac'
			};
		},
		onLoad() {
			that = this
			audioContext.autoplay = false;
			audioContext.src = that.audioUrl
			audioContext.onCanplay(() => {
				that.audioPlay = audioContext.paused;
				that.audioTime = audioContext.duration
			});
			audioContext.onTimeUpdate(() => {
				that.currentTime = audioContext.currentTime
			})
		},

		methods: {
			handlePlay() {
				if (that.audioPlay) {
					audioContext.play();
				} else { //
					audioContext.pause();
				}
				that.audioPlay = !that.audioPlay
			},
			//完成拖动事件
			change(e) {
				audioContext.seek(e.detail.value)
			},
			changing(e) {
				that.currentTime = e.detail.value
			},
		},
		onHide() {
			audioContext.pause();
			that.audioPlay = true
		}
	}
</script>

<style lang="less">
	.music-wrap {
		.music-img {
			width: 100%;
			max-height: 800rpx;
			overflow: hidden;

			.img {
				width: 100%;
				height: 800rpx;
			}
		}

		.music-desc {
			padding: 0 60rpx;

			.music-title {
				font-size: 32rpx;
				color: var(--mainColor);
				text-align: center;
				line-height: 52rpx;
				font-family: aliM;
			}
		}

		.bottom-music {
			display: flex;
			justify-content: center;
			flex-direction: column;
			position: fixed;
			/* #ifdef H5 */
			bottom: 120rpx;
			/* #endif */
			/* #ifdef MP-WEIXIN */
			bottom: 40rpx;
			/* #endif */
			width: 100%;

			.control-btn {
				width: 100%;
				text-align: center;
				margin: 20rpx 0;

				.img {
					width: 100rpx;
					height: 100rpx;
				}
			}
		}
	}
</style>
