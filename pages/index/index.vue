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
		
		<swiper :duration="150 " :current="tabIndex" :style="'height:'+scrollH+'px;'" @change="onChangeTab">
			<swiper-item v-for="(item,index) in newsitems" :key="index">
				<scroll-view scroll-y="true" :style="'height:'+scrollH+'px;'" @scrolltolower="loadmore(index)">
					
					
					<block v-for="(list,listIndex) in item.list" :key="listIndex">
						<!-- 轮播图组件 -->
						<swiper-image v-if="list.type === 'swiper'" :resdata="list.data"></swiper-image>
						<template v-else-if="list.type === 'indexnavs'">
							<!-- 首页分类 -->
							<index-nav :resdata="list.data"></index-nav>
							<!-- 全局分割线 -->
							<divider></divider>
						</template>
						<template  v-else-if="list.type === 'threeAdv'">
							<!-- 三图广告 -->
							<three-adv :resdata="list.data"></three-adv>
							<divider></divider>
						</template>
						
						<!-- 写基础卡片组件 -->
						<!-- <card headTitle="每日精选" bodyCover="/static/images/demo/demo4.jpg"></card> -->
						<!-- <card :showhead="false">
							<block slot="title">标题</block>
							<image src="/static/images/demo/demo4.jpg" mode="widthFix"></image>
						</card> -->
						
						<!-- 公共列表组件 -->
						<view class="row j-sb" v-else-if="list.type === 'commonlist'">
							<block v-for="(item2,index2) in list.data" :key="index2">
								<common-list :item="item2" :index="index2"></common-list>
							</block>
						</view>
					</block>
					<!-- 上拉加载更多 -->
					<divider></divider>
					<view class="d-flex a-center j-center text-light-muted font-md py-3">
						{{item.loadtext}}
					</view>
					
					
				</scroll-view>
			</swiper-item>
		</swiper>
		
		
		
	</view>
</template>

<script>
	// 模拟后端数据
	let demoTabBars = [
		{
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
		}
	];
	let demo1 =[
		{
			type:"swiper",
			data:[
				{src:"../../static/images/demo/demo4.jpg"},
				{src:"../../static/images/demo/demo4.jpg"},
				{src:"../../static/images/demo/demo4.jpg"}
			]
		},
		{
			type:"indexnavs",
			data:[
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
			]
		},
		{
			type:"threeAdv",
			data:{
				big:{
					src:"/static/images/demo/demo1.jpg"
				},
				smalltop:{src:"/static/images/demo/demo2.jpg"},
				smallbottom:{src:"/static/images/demo/demo3.jpg"}
			},
		},
		{
			type:"commonlist",
			data:[
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
				}
			]
		}
	];
	let demo2 = [
		{
			type:"swiper",
			data:[
				{src:"../../static/images/demo/demo4.jpg"},
				{src:"../../static/images/demo/demo4.jpg"},
				{src:"../../static/images/demo/demo4.jpg"}
			]
		},
		{
			type:"indexnavs",
			data:[
				{src:"/static/indexnav/1.png", text:"新品发布"},
				{src:"/static/indexnav/2.gif", text:"小米众筹"},
				{src:"/static/indexnav/3.gif", text:"依旧换新"},
				{src:"/static/indexnav/4.gif", text:"1分拼团"},
				{src:"/static/indexnav/5.gif", text:"超值特卖"}
			]
		},
		{
			type:"commonlist",
			data:[
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
				}
			]
		}
	]
	
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
				tabBars:[],
				newsitems:[]
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
			// 初始化事件
			this.__init()
		},
		methods: {
			// 初始化事件
			__init() {
				// 获取顶部选项卡
				this.tabBars = demoTabBars
				// 根据顶部选项卡生成页面
				let arr = []
				for (var i = 0; i < this.tabBars.length; i++) {
					let obj = {
						list:[],
						// 1，上拉加载更多 2，上拉加载中... 3，没有更多了
						loadtext:"上拉加载更多"
					}
					// 获取首屏数据
					if (i === 0) {
						obj.list = demo1
					}
					arr.push(obj)
				}
				this.newsitems = arr
			},
			// 切换选项卡
			changeTab(index){
				if(this.tabIndex === index){
					return;
				}
				this.tabIndex = index
				this.scrollinto = 'tab'+index
				this.addData()
			},
			// 监听滑动列表
			onChangeTab(e){
				console.log(e)
				this.changeTab(e.detail.current)
			},
			// 加载数据
			addData(){
				// 拿到当前索引
				let index = this.tabIndex
				// 请求数据库
				this.newsitems[index].list = demo2
			},
			// 上拉加载更多
			loadmore(index){
				let item = this.newsitems[index]
				// 是否处于可加载状态
				 if (item.loadtext !== '上拉加载更多'){
					 return;
				 }
				 // 模拟加载
				 item.loadtext = '加载中...'
				 setTimeout(()=>{
					 // 加载数据
					 item.list = [
							 ...item.list,
							 ...demo2
						 ]
					 // 恢复状态
					  item.loadtext = '上拉加载更多'
				 },2000)
			}
		}
	}
</script>

<style>
</style>
