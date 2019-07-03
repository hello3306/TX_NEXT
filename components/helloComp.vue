<template name="helloComp">
	<view>
		{{myval}}
	
	</view>
</template>

<script>
	export default {
		name: "helloComp",
		data() {
			return {
				msg: "自定义组件"
			};
		},
		// 定义组件内部使用的属性
		props: {
			myval:{
				type:String,
				}
		}
	}
</script>

<style>

</style>
