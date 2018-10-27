<template>
	<view class="content">
		<view class="title">{{title}}</view>
		<view class="art-content">
			<rich-text class="richText" :nodes="strings"><!-- {{strings}} --></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '',
				strings : '',
			}
		},
		onLoad:function(e){
			uni.showLoading({
				title: '加载中...',
				mask: false
			});
			console.log(e);
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news/36kr/'+e.newsid,
				method: 'GET',
				data: {},
				success: res => {
					uni.hideLoading();
					console.log(res.data);
					this.title = res.data.title;
					this.strings = res.data.content;//new String(res.data.content);
					// this.strings.replace("\r\n","");//("\r\n","",this.strings);
					console.log(this.strings);
					
				},
				fail: () => {
					this.strings = "加载失败！"
				},
				complete: () => {}
			});
		}
	}
</script>

<style>
.content{
	padding:10upx 2%;
	width: 96%;
	flex-wrap:wrap;
}
.title{line-height:2em;font-weight:700;font-size:38upx}
.art-content{line-height:2em}
</style>
