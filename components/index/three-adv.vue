<template>
	<!-- 左边w:373 h530 -->
	<view class="d-flex">
		<image :src="resdata.big.src"
		lazy-load
		@tap="event(resdata.big)"
		style="width: 373upx;height: 530upx; border-right: 2upx solid #F5F5F5;">
		</image>
		<view class="d-flex flex-column">
			<image @tap="event(resdata.smalltop)" :src="resdata.smalltop.src" style="width: 374upx;height: 264upx; border-bottom: 2upx solid #F5F5F5;"></image>
			<image @tap="event(resdata.smallbottom)" :src="resdata.smallbottom.src" style="width: 374upx;height: 266upx;"></image>
		</view>
	</view>
</template>

<script>
	export default{
		props:{
			resdata:Object
		},
		methods:{
			event(obj){
				console.log(obj)
			}
		}
	}
</script>

<style>
</style>
