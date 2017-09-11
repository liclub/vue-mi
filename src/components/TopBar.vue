<template>
  <a class="header-herf" href="https://item.mi.com/product/5781.html">
	<img class="headImg" src="https://i1.mifile.cn/a4/cms_15046672397294_wpvTa.jpg">
  </a>
  <header class="top-header">
  	<div class="header-content">
  		<ul>
	  		<li v-for="nav in navs">
	  			<a class="menuName" href="{{nav.url}}">{{nav.name}}</a>
	  			<span v-show="$index != '8'"> |</span>
	  		</li>
	  	</ul>
	  	<div class="top-handle">
	  		<a href="http://order.mi.com/site/login?redirectUrl=http://www.mi.com/index.html" class="menuName">登陆</a> | 
	  		<a href="https://account.xiaomi.com/pass/register" class="menuName" id="top-logout">注册</a>
	  		<a href="#" class="buycar" @mouseenter="mouseInBuyCar" @mouseleave="mouserOutBuyCar">购物车(0)</a>
	  	</div>
	  	<div class="by-cararea" v-show="isShow" @mouseenter="mouseInBuyCar" @mouseleave="mouserOutBuyCar" transition="fadein">
	  		购物车中还没有商品,赶快选购吧!
	  	</div>
  	</div>
  </header>
</template>

<script>
export default {
	data () {
		return {
			navs: [
				{name: '小米商城', url: '//www.mi.com/index.html'},
				{name: 'MIUI', url: 'http://www.miui.com/'},
				{name: '米聊', url: 'http://www.miliao.com/'},
				{name: '游戏', url: 'http://game.xiaomi.com/'},
				{name: '多看阅读', url: 'http://www.duokan.com/'},
				{name: '云服务', url: 'https://i.mi.com/'},
				{name: '金融', url: 'https://jr.mi.comfrom=micom'},
				{name: '米币', url: 'https://mibi.mi.com/'},
				{name: '小米商城手机版', url: '//www.mi.com/appdownload/'},
				{name: '问题反馈', url: '//static.mi.com/feedback/'},
				{name: 'Select Region', url: '#'}
			],
			isShow: false,
			timer: ''
		}
	},
	methods: {
		mouseInBuyCar: function () {
			this.isShow = true
			clearInterval(this.timer)
		},
		mouserOutBuyCar: function () {
			let self = this
			this.timer = setTimeout(function () {
				self.isShow = false
			}, 300)
		}
	}
}
</script>

<style scoped>
	.header-herf {
		display: block;
		width: 100%;
		height: 120px;
		text-indent: -50em;
	}
	.top-header {
	    height: 40px;
		width: 100%;
		background: #333;
	}
	.header-content{
		width:1226px;
		position: relative;
		margin: 0 auto;
	}
	.top-header ul {overflow: hidden;width: 80%;}
	.top-header ul li {
		float: left;
		height: 40px;
		line-height: 40px;
		margin:0 5px 0 5px;
		color:#b0b0b0;
	}
	a {
		color:#b0b0b0;
		cursor: pointer;
		font-size: 10px;
	}
	.menuName:hover{
		color: #fff
	} 
	.top-handle{
		float: right;
	    position: absolute;
	    top: 0;
	    color: #b0b0b0;
	    right:0px;
	    height: 40px;
	    line-height: 40px;
	}
	.top-handle #top-logout{
		margin-right: 20px
	}
	.by-cararea{
		width: 300px;
	    height: 100px;
	    font-size: 13px;
	    line-height: 80px;
	    text-align: center;
	    color: #b0b0b0;
	    position: absolute;
	    right: 0;
	    box-shadow: 0px 1px 1px 1px #eee;
	    cursor: pointer;
	    overflow: hidden;
	    background: #fff;
	    z-index: 999
	}
	.fadein-transition {
	  transition: all .5s ease;
	  height: 96px;
	}
	.fadein-enter, .fadein-leave {
	  height: 0;
	}
	.buycar {
		width: 120px;
	    height: 100%;
	    display: block;
	    float: right;
	    text-align: center;
	    background: #424242;
	}
	.buycar:hover {
		color:red;
		background:#fff;
	}
</style>
