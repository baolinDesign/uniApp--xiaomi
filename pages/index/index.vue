<template>
	<view>
		<!-- 顶部选项卡 -->
		<scroll-view scroll-x class="border-bottom scroll-row"
		style="height: 80rpx; line-height: 80rpx;" :scroll-into-view="scrollinto" :scroll-with-animation="true">
			<view class="scroll-row-item px-3"
			@click="changeTab(index)" style="height: 80rpx;"
			v-for="(item,index) in tabBars" :key="index"
			:class="tabIndex === index ? 'main-text-color' : ''" :id="'tab'+index">
				<text class="font-md">{{item.name}}</text>
			</view>
		</scroll-view>
		
		<swiper :duration="1500 " :current="tabIndex" :style="'height:'+scrollH+'px;'" @change="onChangeTab">
			<swiper-item v-for="(item,index) in tabBars" :key="index">
				<scroll-view scroll-y="true" :style="'height:'+scrollH+'px;'">
					<view v-for="i in 100" :key="i">{{i}}</view>
				</scroll-view>
			</swiper-item>
		</swiper>
		
		
		<!-- 轮播图组件 -->
		<!-- <swiper-image :resdata="swipers"></swiper-image> -->
		<!-- 首页分类 -->
		<!-- <index-nav :resdata="indexnavs"></index-nav> -->
		<!-- 全局分割线 -->
		<!-- <divider></divider> -->
		<!-- 三图广告 -->
		<!-- <three-adv :resdata="threeAdv"></three-adv> -->
		
		<!-- <divider></divider> -->
		
		<!-- 写基础卡片组件 -->
		<!-- <card headTitle="每日精选" bodyCover="/static/images/demo/demo4.jpg"></card> -->
		<!-- <card :showhead="false">
			<block slot="title">标题</block>
			<image src="/static/images/demo/demo4.jpg" mode="widthFix"></image>
		</card> -->
		
		<!-- 公共列表组件 -->
		<!-- <view class="row j-sb">
			<block v-for="(item,index) in commonlist" :key="index">
				<common-list :item="item" :index="index"></common-list>
			</block>
		</view> -->
	</view>
</template>

<script>
	import swiperImage from "@/components/index/swiper-image.vue"
	import indexNav from "@/components/index/index-nav.vue"
	import threeAdv from "@/components/index/three-adv.vue"
	import card from "@/components/common/card.vue"
	import commonList from "@/components/common/common-list.vue"
	export default {
		components:{
			swiperImage,
			indexNav,
			threeAdv,
			card,
			commonList
		},
		data() {
			return {
				scrollinto:"",
				scrollH: 500,
				tabIndex:0,
				tabBars:[{
					name:"推荐"
				},{
					name:"关注"
				},{
					name:"体育"
				},{
					name:"热点"
				},{
					name:"财经"
				},{
					name:"娱乐"
				},{
					name:"军事"
				},{
					name:"历史"
				},{
					name:"本地"
				}],
				swipers:[
					{src:"../../static/images/demo/demo4.jpg"},
					{src:"../../static/images/demo/demo4.jpg"},
					{src:"../../static/images/demo/demo4.jpg"}
				],
				indexnavs:[
					{src:"/static/indexnav/1.png", text:"新品发布"},
					{src:"/static/indexnav/2.gif", text:"小米众筹"},
					{src:"/static/indexnav/3.gif", text:"依旧换新"},
					{src:"/static/indexnav/4.gif", text:"1分拼团"},
					{src:"/static/indexnav/5.gif", text:"超值特卖"},
					{src:"/static/indexnav/6.gif", text:"小米秒杀"},
					{src:"/static/indexnav/7.gif", text:"真心想要"},
					{src:"/static/indexnav/8.gif", text:"电视特卖"},
					{src:"/static/indexnav/9.gif", text:"家电热卖"},
					{src:"/static/indexnav/10.gif", text:"米粉卡"}
				],
				threeAdv:{
					big:{
						src:"/static/images/demo/demo1.jpg"
					},
					smalltop:{src:"/static/images/demo/demo2.jpg"},
					smallbottom:{src:"/static/images/demo/demo3.jpg"}
				},
				commonlist:[
					{
						cover:"/static/images/demo/list/1.jpg",
						title:"米家空调",
						desc:"1.5匹变频",
						oprice:"2699",
						pprice:"1399"
					},
					{
						cover:"/static/images/demo/list/1.jpg",
						title:"米家空调",
						desc:"1.5匹变频",
						oprice:"2699",
						pprice:"1399"
					},
					{
						cover:"/static/images/demo/list/1.jpg",
						title:"米家空调",
						desc:"1.5匹变频",
						oprice:"2699",
						pprice:"1399"
					},
					{
						cover:"/static/images/demo/list/1.jpg",
						title:"米家空调",
						desc:"1.5匹变频",
						oprice:"2699",
						pprice:"1399"
					},
					
				]
			}
		},
		onLoad() {
			// 获取可视区域高度
			uni.getSystemInfo({
				success: (res) => {
					console.log(res)
					this.scrollH = res.windowHeight - uni.upx2px(82)
				}
			})
		},
		methods: {
			// 切换选项卡
			changeTab(index){
				if(this.tabIndex === index){
					return;
				}
				this.tabIndex = index
				this.scrollinto = 'tab'+index
			},
			// 监听滑动列表
			onChangeTab(e){
				console.log(e)
				this.changeTab(e.detail.current)
			}
		}
	}
</script>

<style>
</style>
