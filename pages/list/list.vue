<template>
	<view>
		<u-empty text="暂无数据,稍后再试..." mode="list" v-if="ListData.length === 0" style="margin-top: 100rpx;"></u-empty>
		<u-cell-group v-else>
			<u-cell :arrow="false" v-for="item in ListData" :key="item.num" :label="item.code">
				<view slot="title">
					<w-barcode :options="findCode(item)"></w-barcode>
				</view>
			</u-cell>
		</u-cell-group>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				ListData: [],
				config: {
					bar: {
						code: 'E01181016286106',
						color: '#12c2e9', // 条形码的颜色
						bgColor: '#FFFFFF', // 背景色
						width: 670, // 宽度
						height: 100 // 高度
					},
					qrc: {
						code: "https://weixin.qq.com/g/AwYAAHO3aO4zlasEij6bLsk4hlZd5XNFkkBmqyS55mLPFxmn5c9PaI1omqLhd24fABCD23333",
						size: 460, // 二维码大小
						level: 4, //等级 0～4
						bgColor: '#FFFFFF', //二维码背景色 默认白色
						border: {
							color: ['#8A2387', '#F27121'], //边框颜色支持渐变色
							lineWidth: 3, //边框宽度
						},
						// img: '/static/logo.png', //图片
						// iconSize: 40, //二维码图标的大小
						color: ['#56CCF2', '#2F80ED'], //边框颜色支持渐变色
					}
				}
			}
		},
		onReady() {
			uni.showLoading({
				title:"加载中..."
			})
			setTimeout(()=>{
				this.ListData = [
					{num:1,color: "#f12711",code: "E01181016286100"},
					{num:2,color: "#C6FFDD",code: "E01181016286101"},
					{num:3,color: "#c471ed",code: "E01181016286102"},
					{num:4,color: "#29ffc6",code: "E01181016286103"},
					{num:5,color: "#000",code: "E01181016286104"}
				]
				uni.hideLoading()
			},1500)
		},
		methods: {
			findCode (item){
				try{
					const obj =  {
						...this.config.bar,
						code:item.code,
						color: item.color,
					}
					return obj
				}catch(e){}
			}
		}
	}
</script>

<style>

</style>
