<template>
	<view class="page">


		<!-- 轮播图  start-->
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" class="carousel">
			<swiper-item>
				<image src="../../static/carousel/batmanvssuperman.png" class="carousel"></image>
			</swiper-item>
			<swiper-item>
				<image src="../../static/carousel/spiderman.png" class="carousel"></image>
			</swiper-item>
		</swiper>
		<!-- 轮播图  end-->

		<!-- 热门超英 start -->
		<view class="page-block super-hot">
			<view class="hot-title-wapper">
				<image src="../../static/icos/hot.png" class="hot-ico"></image>
				<view class="hot-title">热门超英</view>
			</view>
		</view>

		<scroll-view scroll-x='true' class="page-block hot">
			<block v-for="i in 5">

				<view class="singel-poster" @click="play">
					<view class="poster-wapper">
						<image src="../../static/poster/justice.png" class="poster"></image>
						<view class="move-name">蝙蝠侠蝙蝠侠蝙蝠侠</view>
					</view>
					<!-- 星级评分插件 -->
					<trailerStars :innerScore="6" :showNum="1"> </trailerStars>
				</view>

			</block>
		</scroll-view>
		<!-- 热门超英 end -->

		<!-- 热门预告 start -->
		<view class="page-block super-hot">
			<view class="hot-title-wapper">
				<image src="../../static/icos/interest.png" class="hot-ico"></image>
				<view class="hot-title">热门预告</view>
			</view>
		</view>

		<view class="hot-movies page-block">
			<video v-for="t in 2" :src="video" :poster="poster" class="hot-movies-single" controls>
			</video>
		</view>

		<!-- 热门预告 end -->

		<!-- 猜你喜欢  start-->
		<view class="page-block super-hot">
			<view class="hot-title-wapper">
				<image src="../../static/icos/guess-u-like.png" class="hot-ico"></image>
				<view class="hot-title">猜你喜欢</view>
			</view>
		</view>
		<block v-for="(i,gindex) in 5">
			<view class="page-block guess-u-like">
				<view class="single-like-movie">
					<image src="../../static/poster/justice.png" class="like-movie"></image>
					<view class="movie-desc">
						<view class="movie-title">
							蝙蝠侠蝙蝠侠蝙蝠侠
						</view>
						<trailerStars :innerScore="6" :showNum="0"> </trailerStars>
						<view class="movie-info">
							2018 / 美国 / 科幻 动作
						</view>
						<view class="movie-info">
							迈克尔·基顿 / 乔治·克鲁尼 / 克里斯蒂安·贝尔 / 本·阿弗莱克
						</view>
					</view>

					<view class="movie-oper" :data-gindex="gindex" @click="praiseMe">
						<image src="../../static/icos/praise.png" class="praise-ico"></image>
						<view class="praise-me">点赞</view>
						<view :animation="animationDataArr[gindex]" class="praise-me animation-opacity">+1</view>
					</view>
				</view>
			</view>
		</block>

		<!-- 猜你喜欢 end -->

	</view>
</template>

<script>
	import common from '../../common/common.js'
	import request from "../../common/request.js"

	// 导入自定义组件
	import helloComp from "../../components/helloComp.vue";
	import trailerStars from "../../components/trailerStars.vue";
	export default {
		data() {
			return {
				carouselList: [],
				hotSuperheroList: [],
				hotTrailerList: [],
				video: "https://gzkst-web.oss-cn-beijing.aliyuncs.com/video/INTL_FeelsGood_30_CN%206%E6%9C%886%E6%97%A5%20%E6%B5%B4%E7%81%AB%E5%AF%B9%E5%86%B3.mp4",
				poster: "http://tva1.sinaimg.cn/large/0060lm7Tly1g4dqtuqv77j31900u0kjl.jpg",
				animationData: {},
				animationDataArr: [{}, {}, {}, {}, {}]
			}
		},
		onUnload() {
			// 页面卸载的时候清除动画数据
			this.animation = {};
			this.animationDataArr = [{}, {}, {}, {}, {}];
		},

		onLoad() {
			//#ifdef APP-PLUS || MP-WEIXIN
			// 在页面创建的时候，创建临时的动画
			this.animation = uni.createAnimation()
			// #endif


			// let baseUrl=this.baseUrl;
			// 
			// 			uni.request({
			// 				url: common.baseUrl,
			// 				method: "GET",
			// 				success: (res) => {
			// 					if (res.statusCode == 200) {
			// 						this.text="200";
			// 						console.log(res);
			// 						uni.showToast({
			// 							title: '请求成功',
			// 							icon: 'success',
			// 							mask: true
			// 						})
			// 					}
			// 
			// 				}
			// 			})
		},
		// 下拉刷新函数
		onPullDownRefresh() {
			uni.showLoading({
				title: '刷新ing',
				// 防止用户点击
				mask:true 
			})
			// 导航栏刷新显示
			// uni.showNavigationBarLoading();
			
			setTimeout(function() {
				uni.stopPullDownRefresh()
				uni.showToast({
					title: '刷新成功',
					icon: 'success',
				})
			}, 2000);
		},

		methods: {
			play(res) {
				console.log(res);
				uni.showToast({
					title: '点击',
					icon: 'success',
				})

			},
			// 实现点赞动画效果
			praiseMe(e) {
				var gindex = e.currentTarget.dataset.gindex;
				//#ifdef APP-PLUS || MP-WEIXIN

				// 构建动画数据，并且通过step来表示这组动画完成
				this.animation.translateY(-60).opacity(1).step({
					duration: 400
				});
				// 导出动画数据到view组件，实现组件的动画效果
				// this.animationData = this.animation.export();
				this.animationData = this.animation;
				this.animationDataArr[gindex] = this.animationData.export();

				// 还原动画
				setTimeout(function() {
					this.animation.translateY(0).opacity(0).step({
						duration: 0
					});
					this.animationData = this.animation;
					this.animationDataArr[gindex] = this.animationData.export();
				}.bind(this), 600);
				// #endif

			}
		},
		components: {
			helloComp,
			trailerStars
		}
	}
</script>

<style>
	@import url("index.css");
</style>
