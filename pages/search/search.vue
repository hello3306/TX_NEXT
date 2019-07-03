<template>
	<view class="page">
		<!-- 搜索框 start -->
		<view class="search-block">
			<view class="search-ico-waper">
				<image src="../../static/icos/search.png" class="search-ico"></image>
			</view>

			<input type="text" confirm-type="search" @confirm="search" placeholder="请输入搜索的内容" focus="true" maxlength="10" class="search-text" />
		</view>
		<!-- 搜索框 end -->

		<!-- 电影列表 start -->

		<view class="page-block movie-list">
			<block v-for="(img,index) in trailerList">
				<view class="movie-wapper" @click="movie(index)">
					<image :src="img" class="poster"></image>
				</view>
			</block>
		</view>

		<!-- 电影列表 end -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				keywords: '',
				trailerList: ["../../static/poster/civilwar.jpg",
					"../../static/poster/civilwar.jpg",
					"../../static/poster/civilwar.jpg",
					"../../static/poster/civilwar.jpg",
					"../../static/poster/civilwar.jpg",
					"../../static/poster/civilwar.jpg",
					"../../static/poster/civilwar.jpg",
					"../../static/poster/civilwar.jpg",
					"../../static/poster/civilwar.jpg",
					"../../static/poster/civilwar.jpg",
					"../../static/poster/civilwar.jpg",
					"../../static/poster/civilwar.jpg",
					"../../static/poster/civilwar.jpg",
					"../../static/poster/civilwar.jpg",
					"../../static/poster/civilwar.jpg",
				],
				page: 1,
				totalPages: 1,
				index: 1
			}
		},
		onReachBottom() {
			var that = this;
			let newTraulerList = ["../../static/poster/justice.png", "../../static/poster/justice.png",
				"../../static/poster/justice.png"
			]

			if (that.index <= 2) {
				that.trailerList = that.trailerList.concat(newTraulerList)
				that.index++;
			} else {
				uni.showToast({
					title: "没有数据了！",
					icon: "success"
				})
			}
		},
		methods: {
			search(e) {
				console.log(e);
				let value = e.detail.value;
				this.keywords = value;
				this.trailerList = ["../../static/poster/civilwar.jpg"];
				uni.showToast({
					title: value,
					icon: "success"
				})
				console.log(value)
			},
			movie(index) {
				uni.navigateTo({
					url:"../movie/movie?index="+index
				})
				console.log(index)
			}
		}
	}
</script>

<style>
	@import url("search.css");
</style>
