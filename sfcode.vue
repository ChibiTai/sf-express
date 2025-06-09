<template>
	<view class="scroll-box">
		<view class="main-height-box flex-center">
			<view class="main-width-box flex-column">
				<view class="title-box flex-column">
					<view class="top-box flex-center">
						<img src="../../static/wakuwaku_square.png"></img>
						<view style="width: 30px; height: 30px;">
							<langbox hidetext="true" sfpage="true"></langbox>
						</view>
					</view>
					<text>購買完成</text>
				</view>
				<view class="content-box flex-column">
					<view class="sf-text-box">
						<text class="sf-station">順豐站 {{sfNo}}</text>
						<text class="tag bg-orange">順豐站立即自取</text>
						<text class="tag bg-aqua">即買即抽</text>
					</view>
					<view class="code-column flex-column">
						<text>取件碼</text>
						<text class="sfcode">{{sfCode}}</text>
						<text>請向順豐站 {{sfNo}} 職員展示</text>
						<text class="warning">請勿離開頁面，如要離開，請先截圖</text>
					</view>
					<view class="sf-btn-box flex-center">
						<button class="black-btn">保存屏幕截圖</button>
						<button class="red-btn" @click="backToShop">繼續購物</button>
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
				sfNo: 'demo1234567',
				sfCode:'demo12345678',
			}
		},
		methods: {
			backToShop(){
				uni.navigateTo({
					url:'/pages/views/sfexpress',
				})
			}
		}
	}
</script>

<style scoped>@import url('/css/sfexpress.css');</style>
