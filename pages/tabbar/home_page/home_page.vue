<!-- 主页 -->
<template>
	<view>
		<!-- #ifndef MP -->
		<!-- 固定在顶部的导航栏 -->
		<uni-nav-bar
			color="#333333"
			background-color="#FFFFFF"
			fixed="true"
			right-icon="scan"
			@click-left="showCity"
			@click-right="scan"
		>
			<block slot="left">
				<view class="city">
					<text>{{ city }}</text>
					<uni-icon type="arrowdown" color="#333333" size="22"></uni-icon>
				</view>
			</block>
			<view class="input-view">
				<uni-icon type="search" size="10"></uni-icon>
				<input
					confirm-type="search"
					@confirm="confirm"
					class="input"
					type="text"
					placeholder="输入搜索关键词"
				/>
			</view>
		</uni-nav-bar>
		<view style="height:80px;"></view>
		<!-- 使用非原生导航栏后需要在页面顶部占位 -->
		<!-- #endif -->
		<!-- 轮播图 start-->
		<view class="uni-padding-wrap">
			<view class="page-section swiper">
				<view class="page-section-spacing ">
					<swiper
						class="swiper "
						:indicator-dots="indicatorDots"
						:autoplay="autoplay"
						:interval="interval"
						:duration="duration"
					>
						<swiper-item><view class="swiper-item uni-bg-red">A</view></swiper-item>
						<swiper-item><view class="swiper-item uni-bg-green">B</view></swiper-item>
						<swiper-item><view class="swiper-item uni-bg-blue">C</view></swiper-item>
					</swiper>
				</view>
			</view>
		</view>

		<!-- 	<view class="swiper-list">
			<view class="uni-list-cell uni-list-cell-pd">
				<view class="uni-list-cell-db">指示点</view>
				<switch :checked="indicatorDots" @change="changeIndicatorDots" />
			</view>
			<view class="uni-list-cell uni-list-cell-pd">
				<view class="uni-list-cell-db">自动播放</view>
				<switch :checked="autoplay" @change="changeAutoplay" />
			</view>
		</view>

		<view class="uni-padding-wrap">
			<view class="uni-common-mt">
				<text>幻灯片切换时长(ms)</text>
				<text class="info">{{duration}}</text>
			</view>
			<slider @change="durationChange" :value="duration" min="500" max="2000" />
			<view class="uni-common-mt">
				<text>自动播放间隔时长(ms)</text>
				<text class="info">{{interval}}</text>
			</view>
			<slider @change="intervalChange" :value="interval" min="2000" max="10000" />
		</view> -->
		<!-- 轮播图 end-->
		<!--  九宫格 start -->
		<uni-grid
			:data="[
				{ image: 'https://img-cdn-qiniu.dcloud.net.cn/img/shu.png', text: '美食/住宿' },
				{ image: 'https://img-cdn-qiniu.dcloud.net.cn/img/lindang.png', text: '推广/优惠' },
				{ image: 'https://img-cdn-qiniu.dcloud.net.cn/img/laoren.png', text: '便利超市' },
				{ image: 'https://img-cdn-qiniu.dcloud.net.cn/img/liwu.png', text: '公司黄页' },
				{ image: 'https://img-cdn-qiniu.dcloud.net.cn/img/maozi.png', text: '出租/转让' },
				{ image: 'https://img-cdn-qiniu.dcloud.net.cn/img/shoutao.png', text: '批发市场' },
				{ image: 'https://img-cdn-qiniu.dcloud.net.cn/img/xueqiao.png', text: '拼车服务' },
				{ image: 'https://img-cdn-qiniu.dcloud.net.cn/img/xunlu.png', text: '其他信息' }
			]"
			column-num="4"
			showBorder="false"
		></uni-grid>
		<!--  九宫格 end -->
		<!-- 公告栏 start -->
		<view class="uni-swiper-msg">
			<view class="uni-swiper-msg-icon">
				<image
					src="https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png"
					mode="widthFix"
				></image>
			</view>
			<swiper autoplay="true" circular="true" interval="5000">
				<swiper-item>
					<navigator>uni-app行业峰会频频亮相，开发者反响热烈</navigator>
				</swiper-item>
				<swiper-item>
					<navigator>DCloud完成B2轮融资，uni-app震撼发布</navigator>
				</swiper-item>
				<swiper-item>
					<navigator>36氪热文榜推荐、CSDN公号推荐 DCloud CEO文章</navigator>
				</swiper-item>
			</swiper>
		</view>
		<!-- 公告栏 end -->
		<!-- 商品列表 start  -->
		<view class="page">
			<view class="uni-product-list">
				<view class="uni-product" v-for="(product, index) in productList" :key="index">
					<view class="image-view">
						<image
							v-if="renderImage"
							class="uni-product-image"
							:src="product.image"
						></image>
					</view>
					<view class="uni-product-title">{{ product.title }}</view>
					<view class="uni-product-price">
						<text class="uni-product-price-favour">￥{{ product.originalPrice }}</text>
						<text class="uni-product-price-original">￥{{ product.favourPrice }}</text>
						<!-- <text class="uni-product-tip">{{ product.tip }}</text> -->
					</view>
				</view>
			</view>
		</view>
		<!-- 商品列表 end -->
	</view>
</template>

<script>
import uniNavBar from '../../../components/uni-nav-bar.vue';
import uniIcon from '../../../components/uni-icon.vue';
import uniGrid from '../../../components/uni-grid.vue';

export default {
	data() {
	    //模拟数据
		return {
			title: 'Hello',
			city: '北京',
			background: ['color1', 'color2', 'color3'],
			indicatorDots: true,
			autoplay: true,
			interval: 2000,
			duration: 500,
			productList: [
				{
					image: 'https://img-cdn-qiniu.dcloud.net.cn/uploads/example/product1.jpg',
					title: 'Apple iPhone X 256GB 深空灰色 移动联通电信4G手机',
					originalPrice: 9999,
					favourPrice: 8888,
					tip: '自营'
				},
				{
					image: 'https://img-cdn-qiniu.dcloud.net.cn/uploads/example/product2.jpg',
					title: 'Apple iPad 平板电脑 2018年新款9.7英寸',
					originalPrice: 3499,
					favourPrice: 3399,
					tip: '优惠'
				},
				{
					image: 'https://img-cdn-qiniu.dcloud.net.cn/uploads/example/product3.jpg',
					title:
						'Apple MacBook Pro 13.3英寸笔记本电脑（2017款Core i5处理器/8GB内存/256GB硬盘 MupxT2CH/A）',
					originalPrice: 12999,
					favourPrice: 10688,
					tip: '秒杀'
				},
				{
					image: 'https://img-cdn-qiniu.dcloud.net.cn/uploads/example/product4.jpg',
					title: 'Kindle Paperwhite电纸书阅读器 电子书墨水屏 6英寸wifi 黑色',
					originalPrice: 999,
					favourPrice: 958,
					tip: '秒杀'
				},
				{
					image: 'https://img-cdn-qiniu.dcloud.net.cn/uploads/example/product5.jpg',
					title:
						'微软（Microsoft）新Surface Pro 二合一平板电脑笔记本 12.3英寸（i5 8G内存 256G存储）',
					originalPrice: 8888,
					favourPrice: 8288,
					tip: '优惠'
				},
				{
					image: 'https://img-cdn-qiniu.dcloud.net.cn/uploads/example/product6.jpg',
					title:
						'Apple Watch Series 3智能手表（GPS款 42毫米 深空灰色铝金属表壳 黑色运动型表带 MQL12CH/A）',
					originalPrice: 2899,
					favourPrice: 2799,
					tip: '自营'
				}
			],
			renderImage: true
		};
	},
	onLoad() {},
	methods: {
		show() {},
		back() {
			uni.navigateBack({
				delta: 1
			});
		},
		showMenu() {
			uni.showToast({
				title: '菜单'
			});
		},
		clickLeft() {
			uni.showToast({
				title: '左侧按钮'
			});
		},
		search() {
			uni.showToast({
				title: '搜索'
			});
		},
		showCity() {
			uni.showToast({
				title: '选择城市'
			});
		},
		scan() {
			uni.showToast({
				title: '扫码'
			});
		},
		confirm() {
			uni.showToast({
				title: '搜索'
			});
		},
		changeIndicatorDots(e) {
			this.indicatorDots = !this.indicatorDots;
		},
		changeAutoplay(e) {
			this.autoplay = !this.autoplay;
		},
		intervalChange(e) {
			this.interval = e.target.value;
		},
		durationChange(e) {
			this.duration = e.target.value;
		},
		onPullDownRefresh() {
			console.log('onPullDownRefresh');
			setTimeout(function() {
				uni.stopPullDownRefresh();
				console.log('stopPullDownRefresh');
			}, 1000);
		}
	},
	components: {
		uniNavBar,
		uniIcon,
		uniGrid
	},
	created() {

	}
};
</script>

<style>
.content {
	text-align: center;
	height: 400upx;
	/* margin-top: 200upx; */
}
.title {
	font-size: 15px;
	line-height: 20px;
	color: #333333;
	padding: 15px;
}

.city {
	display: flex;
	flex-direction: row;
	align-items: center;
	justify-content: center;
	width: 100%;
	margin-left: 8px;
}

.input-view {
	width: 92%;
	display: flex;
	background-color: #e7e7e7;
	height: 30px;
	border-radius: 15px;
	padding: 0 4%;
	flex-wrap: nowrap;
	margin: 7px 0;
	line-height: 30px;
}

.input-view .uni-icon {
	line-height: 30px !important;
}

.input-view .input {
	height: 30px;
	line-height: 30px;
	width: 94%;
	padding: 0 3%;
}
/* 轮播图样式 start */
.swiper {
	/* padding-top: 5upx;
	padding-bottom: 5upx; */
	height: 300upx;
}
.swiper-item {
	display: block;
	height: 300upx;
	line-height: 300upx;
	text-align: center;
}

/* .swiper-list {
		margin-top: 40upx;
		margin-bottom: 0;
	} */

/* .uni-common-mt{
		margin-top:60upx;
		position:relative;
	} */

/* .info {
		position: absolute;
		right:20upx;
	} */
/* 轮播图样式 end */
</style>
