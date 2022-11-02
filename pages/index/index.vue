<template>
	<view>
		<view class="background"></view>
		<view class="container">
			<view class="panel">
				<view class="header">请扫描以下任意二维码或条形码</view>
				<view>
					<w-barcode :options="bar"></w-barcode>
					<view class="barnum">{{ code }}</view>
				</view>
				<view style="display: flex;justify-content:space-between ;width: 80%;flex-wrap: wrap;">
					<w-qrcode @press="longtap" style="margin-top: 1rem;" v-for="(item,index) in arrList" :key="index" :options="item" ref="qrcode" @generate="hello"></w-qrcode>
				</view>
			</view>
		</view>
		<u-popup
		      :show="showLoginPopup"
		      :safe-area-inset-bottom="false"
		      mode="center"
		      round="10"
		      closeable
		      class="content"
		      @close="closeHandler"
		      @open="openHandler"
		      @closeOnClickOverlay="closeHandler"
		    >
		      <view class="content">
		        <view class="we-app-login-button">
		          <u-button>请登录</u-button>
		        </view>
		      </view>
		    </u-popup>
	</view>
</template>

<script>
export default {
	data() {
		return {
			show: true,
			code: 'E01181016286106',
			title: '条码 二维码',
			background: {
				backgroundColor: '#1b82d2'
			},
			arrList: [
				{
					code: 'https://qm.qq.com/cgi-bin/qm/qr?k=LKqML292dD2WvwQfAJXBUmvgbiB_TZWF&noverify=0',
					size: 260, // 二维码大小
				},
				{
					code: 'https://qm.qq.com/cgi-bin/qm/qr?k=LKqML292dD2WvwQfAJXBUmvgbiB_TZWF&noverify=0',
					size: 260, // 二维码大小
					level: 1, //等级 0～4
				},
				{
					code: 'https://qm.qq.com/cgi-bin/qm/qr?k=LKqML292dD2WvwQfAJXBUmvgbiB_TZWF&noverify=0',
					size: 260, // 二维码大小
					padding: 25,
					src: '/static/bg6.png',
				},
				{
					code: 'https://qm.qq.com/cgi-bin/qm/qr?k=LKqML292dD2WvwQfAJXBUmvgbiB_TZWF&noverify=0',
					size: 260, // 二维码大小
					padding: 40,
					src: '/static/bg5.png',
					// bgColor: 'red', //二维码背景色 默认白色 transparent透明
					type: 'none',
					// border: {
					// 	opacity: 0.2,
					// 	degree: 20,
					// 	color: ['#e96443','#904e95'], //边框颜色支持渐变色
					// 	lineWidth: 5 //边框宽度
					// },
					img: {
						degree: 8,
						src: '/static/logo.png',
						size: 20,
						type: 'round',
						color: '#ffffff',
						width: 5
					},
				},
				{
					code: 'https://qm.qq.com/cgi-bin/qm/qr?k=LKqML292dD2WvwQfAJXBUmvgbiB_TZWF&noverify=0',
					size: 260, // 二维码大小
					type: 'none',
					padding: 10,
					border: {
						opacity: 0.5,
						degree: 10,
						color: ['#e96443','#904e95'], //边框颜色支持渐变色
						lineWidth: 5 //边框宽度
					},
					img: {
						src: '/static/logo.png',
						size: 20,
						type: 'r',
						color: '#ffffff',
						width: 10
					},
					color:['#45B649','#00c3ff', '#ee0979','#e96443','#904e95'] //边框颜色支持渐变色
				},
				{
					code: 'https://qm.qq.com/cgi-bin/qm/qr?k=LKqML292dD2WvwQfAJXBUmvgbiB_TZWF&noverify=0',
					size: 260, // 二维码大小
					padding: 40,
					src: '/static/bg11.png',
					// bgColor: 'red', //二维码背景色 默认白色 transparent透明
					type: 'none',
					img: {
						degree: 8,
						src: '/static/logo.png',
						size: 20,
						type: 'round',
						color: '#ffffff',
						width: 5
					},
				},
				{
					code: 'https://qm.qq.com/cgi-bin/qm/qr?k=LKqML292dD2WvwQfAJXBUmvgbiB_TZWF&noverify=0',
					size: 460, // 二维码大小
					padding: 40,
					src: '/static/bg7.png',
					// bgColor: 'red', //二维码背景色 默认白色 transparent透明
					type: 'none',
					img: {
						src: '/static/logo.png',
						size: 20,
						type: 'circle',
						color: '#ffffff',
						width: 10
					},
					text:{
						// opacity: 1,
						//当前字体样式的属性。符合 CSS font 语法 的 DOMString 字符串，至少需要提供字体大小和字体族名。默认值为 normal 20px system-ui。
						font: "normal 25px system-ui",// 默认normal 20px system-ui
						color: ['#000000'],
						content: "你 好 啊"
					},
					color:['#45B649','#00c3ff', '#ee0979','#e96443','#904e95'] //边框颜色支持渐变色
				},
			],
			bar: {
				code: 'E01181016286106',
				color:['#45B649','#00c3ff', '#ee0979','#e96443','#904e95'], // 条形码的颜色
				bgColor: '#FFFFFF', // 背景色
				width: 670, // 宽度
				height: 100 // 高度
			},
			showLoginPopup: true,
		};
	},
	onReady() {
		
	},
	methods: {
		longtap (e){
			console.log(e)
		},
		
		hello(res) {
			try {
				// console.log(321, res)
			} catch (e) {}
		},
		async saveCode(){//手动触发获取图片
			const res = await this.$refs.qrcode.GetCodeImg();
			// console.log(res)
		},
		closeHandler() {
		    this.$emit('input', false);
		  },
		  openHandler() {
		    // TODO 打开时的处理
		  }
	}
};
</script>
<style scoped lang="less">
page {
	background-color: #1b82d2;
}

.background {
	width: 100%;
	height: 100%;
	position: absolute;
	z-index: -1;
	background-color: #1b82d2;
}

.container {
	display: flex;
	justify-content: center;
}

.panel {
	margin-top: 80rpx;
	display: flex;
	overflow: hidden;
	flex-direction: column;
	justify-content: space-between;
	align-items: stretch;
	align-items: center;
	width: 95%;
	border-radius: 10rpx;
	background-color: #fff;
	padding-bottom: 80rpx;
}

.header {
	width: 100%;
	height: 140rpx;
	background-color: #f0f0f0;
	border-radius: 10rpx 10rpx 0 0;
	text-align: center;
	line-height: 140rpx;
	font-weight: bold;
	letter-spacing: 2px;
	margin-bottom: 40rpx;
	color: #1b82d2;
}

.barnum {
	width: 670rpx;
	height: 100rpx;
	line-height: 100rpx;
	font-size: 38rpx;
	font-weight: bold;
	text-align: center;
	letter-spacing: 5rpx;
	white-space: nowrap;
}

  .content {
    width: 600rpx;
    height: 60vh;
    position: relative;
    display: flex;
    justify-content: center;
    align-content: center;
    .we-app-login-button {
      position: absolute;
      bottom: 44rpx;
    }
  }
</style>
