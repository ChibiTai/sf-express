<template>
	<view class="scroll-box">
		<view class="main-height-box flex-center">
			<view class="main-width-box flex-column">
				<view class="fix-box flex-column">
					<view class="top-box flex-center">
						<img src="../../static/wakuwaku_square.png"></img>
						<view style="width: 30px; height: 30px;">
							<langbox hidetext="true" sfpage="true"></langbox>
						</view>
					</view>
					<text>{{isActiveTab==1?'商品購買':'關於卡舖'}}</text>
					<view class="tab-index-box">
						<text :class="{isActiveTab:isActiveTab==1}" @click="activeTab(1)">商品</text>
						<text :class="{isActiveTab:isActiveTab==2}" @click="activeTab(2)">關於卡舖</text>
					</view>
					<view class="common-box flex-center">
						<img v-if="this.$i18n.locale=='jp'||this.$i18n.locale=='en'" src="../../static/LOGO_EN_JP.png"></img>
						<img v-else src="../../static/LOGO_ZH_SC.png"></img>
						<view class="common-right flex-column">
							<view class="common-text-box">
								<img src="../../static/golden_cup.png" style="width:20px;margin-right: 2px"></img>
								<text>香港No.1遊戲卡牌福袋 \n 好多嘢送，等你一擊即中！</text>
							</view>
							<button class="black-red-btn" @click="toHomepage">一擊即中</button>
						</view>
					</view>
				</view>
						
				<view class="content-box content-top-padding flex-center">
					<view v-if="isActiveTab==1" class="tab-box flex-column">
						<view class="tab1-top-box">
							<view class="text-box">
								<text class="sf-station">順豐站 {{sfNo}}</text>
								<text class="tag bg-orange">順豐站立即自取</text>
								<text class="tag bg-aqua">即買即抽</text>
							</view>
							<view class="sort-btn" @click="showSort=!showSort">
								<img src="../../static/right-menu.svg"></img>
								<text>分類</text>
							</view>
							<view v-if="showSort" class="sort-menu">
								<view @click="order='';showSort=false" 
									class="order-selection" :class="{isActiveOrder:order==''}">
									<img src="@/static/yes.png"></img>
									<text>推薦</text>
								</view>
								<view @click="order='asc';showSort=false" 
									class="order-selection" :class="{isActiveOrder:order=='asc'}">
									<img src="@/static/yes.png"></img>
									<text>價格從高至低</text>
								</view>
								<view @click="order='desc';showSort=false"
									class="order-selection" :class="{isActiveOrder:order=='desc'}">
									<img src="@/static/yes.png"></img>
									<text>價格從低至高</text>
								</view>
							</view>
						</view>
						<view class="item-box" v-for="(item,index) in productList" :key="index">
							<view class="item-box-left">
								<image class="item-img product-img" :src="item.productImg" mode="widthFix"></image>
								<view class="item-des">
									<image class="shop-logo" :src="item.shopLogo" mode="heightFix"></image>
									<text class="price-text">{{item.price}}</text>
									<text class="series-text">{{item.series}}</text>
									<text class="name-text">{{item.name}}</text>
								</view>			
							</view>
							<view class="item-box-right">
								<button class="red-btn" v-if="item.availability" @click="purchaseItem">立即購買</button>
								<button class="grey-btn" v-else>售罄</button>
								<view class="availability-box flex-center">
									<text>庫存:</text>
									<img v-if="item.availability" src="../../static/selected.png"></img>
									<img v-else src="../../static/cross.png"></img>
								</view>
							</view>
						</view>
					</view>
					<view v-if="isActiveTab==2" class="tab-box flex-column">
						<view class="item-box" v-for="(item,index) in shopList" :key="index">
							<view class="item-box-left">
								<image class="item-img shop-img" :src="item.logo" mode="widthFix"></image>
								<view class="item-des">
									<text class="tag bg-orange">地址</text>
									<text class="shop-text">{{item.address}}</text>
									<text class="tag bg-orange">電話</text>
									<text class="shop-text">{{item.phone}}</text>
								</view>
							</view>
							<button class="black-btn shop-link-btn" @click="linkShop(item.link)">瀏覽網站</button>
						</view>
					</view>
				</view>
			</view>
		</view>
		<footerPage :showCoop="false" :showSocialMedia="false"></footerPage>
	</view>
</template>

<script>
	import langbox from "@/pages/sidebar/langbox.vue";
	import footerPage from "@/pages/footer/footer.vue";
	export default {
		components: {
			langbox,
			footerPage
		},
		data() {
			return {
				isActiveTab: 1,
				showSort: false,
				order: 'default',
				sfNo: 'demo1234567',
				productList:[ //demo
					{
						name:'寶可夢日本版 原盒',
						productImg:'../../static/cooperate/generalcardshop.png',
						shopLogo:'../../static/cooperate/generalcardshop.png',
						price:'HKD 820',
						series:'SV11W',
						availability: true, //庫存
					},
					{
						name:'寶可夢日本版 原盒',
						productImg:'../../static/cooperate/playerclub.png',
						shopLogo:'../../static/cooperate/playerclub.png',
						price:'HKD 820',
						series:'SV11B',
						availability: false, //庫存
					},
					{
						name:'寶可夢日本版 原盒',
						productImg:'../../static/cooperate/playerclub.png',
						shopLogo:'../../static/cooperate/playerclub.png',
						price:'HKD 820',
						series:'SV11B',
						availability: false, //庫存
					},
					{
						name:'寶可夢日本版 原盒',
						productImg:'../../static/cooperate/playerclub.png',
						shopLogo:'../../static/cooperate/playerclub.png',
						price:'HKD 820',
						series:'SV11B',
						availability: false, //庫存
					},
					{
						name:'寶可夢日本版 原盒',
						productImg:'../../static/cooperate/playerclub.png',
						shopLogo:'../../static/cooperate/playerclub.png',
						price:'HKD 820',
						series:'SV11B',
						availability: false, //庫存
					}
				],
				shopList:[ //demo
					{
						logo:'../../static/cooperate/generalcardshop.png',
						address:'xxxxxxxx',
						phone:'12345678',
						link: 'https://www.generalcardshop.com/', 
					},
					{
						logo:'../../static/cooperate/generalcardshop.png',
						address:'xxx yyyyyyyy',
						phone:'12345678',
						link: 'https://www.generalcardshop.com/', 
					}
				]
			}
		},
		methods: {
			activeTab(tab){
				this.isActiveTab = tab;
			},
			linkShop(link){
				window.open(link);
			},
			purchaseItem(){
				uni.navigateTo({
					url:'/pages/views/sfcode',
				})
			},
			toHomepage(){
				uni.navigateTo({
					url:'/pages/views/index',
				})
			}
		}
	}
</script>

<style scoped>@import url('/css/sfexpress.css');</style>
