<template>
	<view class="page">
		<!-- 视频播放 start -->
		<view class="player">
			<video id="myTrailer" :src="video" :poster="poster" class="movie" controls></video>
		</view>
		<!-- 视频播放 end -->

		<!-- 影片基本信息  start-->
		<view class="movie-info">

			<image src="../../static/poster/justice.png" mode="aspectFit" class="cover"></image>
			<view class="movie-desc">
				<view class="title">X战警：黑凤凰</view>
				<view class="basic-info">片 长 114分钟 </view>
				<view class="basic-info">外文名 X-Men: Dark Phoenix </view>
				<view class="basic-info">上映时间 2019年6月6日（中国大陆）2019年6月7日（北美）</view>
				<view class="score-block">
					<view class="big-score">
						<view class="score-words">综合评分:</view>
						<block v-if="score>=0">
							<view class="movie-score">{{score}}</view>
						</block>
					</view>
					<view class="scroll-stars">
						<block v-if="score>=0">
							<trailerStars :innerScore="score" :showNum="0"> </trailerStars>
						</block>
						<view class="prise-counts">18965人点赞</view>
					</view>
				</view>
			</view>
		</view>
		<!-- 影片基本信息 end-->

		<view class="line-wapper">
			<view class="line"></view>
		</view>

		<!-- 剧情介绍 start -->
		<view class="plots-block">
			<view class="plots-title">剧情介绍</view>
			<view class="plots-desc">{{plotsdesc}}</view>
		</view>
		<!-- 剧情介绍 end -->
	</view>
</template>

<script>
	import trailerStars from "../../components/trailerStars.vue";
	
	export default {
		components: {
			trailerStars
		},
		data() {
			return {
				video: "https://gzkst-web.oss-cn-beijing.aliyuncs.com/video/INTL_FeelsGood_30_CN%206%E6%9C%886%E6%97%A5%20%E6%B5%B4%E7%81%AB%E5%AF%B9%E5%86%B3.mp4",
				poster: "http://tva1.sinaimg.cn/large/0060lm7Tly1g4dqtuqv77j31900u0kjl.jpg",
				score: 8.6,
				plotsdesc: "琴·葛蕾（索菲·特纳饰）意外吸收了来自太空的宇宙能量，不仅没死，反而变得更加强大，接着琴·葛蕾一路发现自己身世的真相，失控之后，让跟着那股宇宙能量来到地球的外星人有机可乘。为了拿回那股宇宙能量，外星人领导Vuk（杰西卡·查斯坦饰）抓着琴·葛蕾的“身份认同”问题，挑拨她与X战警间的矛盾 [5]  。随着琴·葛蕾的失控，面对“毁灭黑凤凰”还是“拯救琴·葛蕾”的艰难抉择，X战警分崩离析，走向分裂。为了对抗这位黑化的昔日挚友、同时也是宇宙最强的变种人，他们不得不拼尽全力，迎接这场没有胜者的战争 [6]  。"
			}
		},
		onLoad: function(option) {
			console.log(option.index); //打印出上个页面传递的参数。

		},
		methods: {

		}
	}
</script>

<style>
	@import url("movie.css");
</style>
