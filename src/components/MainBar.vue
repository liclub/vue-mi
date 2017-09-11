<template>
	<div class="bar">
		<div class="mainBar">
			<div class="milog">
				<img src='../assets/img/icon-mi.png'>
			</div>
			<div class="migift">
				<img src='../assets/img/win.gif'>
			</div>
			<ul class="mainMenu">
				<li v-for="item in items">
					<template v-if="item.type">
						<a :href="item.sourceUrl"  @mouseenter="mainMenuEnter(item.type)" @mouseleave="mainMenuLeave()">{{item.name}}</a>
					</template>
					<template v-else>
						<a :href="item.sourceUrl">{{item.name}}</a>
					</template>
				</li>
			</ul>
			<div class="bar-earch"  v-bind:class="{borderRed : isRed}" >
				<ul class="on-input" transition="fadein" v-show="!isRed">
					<li v-for="i in inputItems">
						<a>{{i.name}}</a>
					</li>
				</ul>
				<input type="text" @focus="searchFocus" @blur="searchBlur"/>
				<label class="seachBtn" v-bind:class="{borderLeftred : isRed}">
					<img src="../assets/img/icon-search.png">
				</label>
				<ul class="searchUl" v-show="isRed">
					<li v-for="search in searchItems">
						<span class="search-name">{{search.name}}</span>
						<span class="search-count">约有{{search.count}}件</span>
					</li>
				</ul>
			</div>
		</div>
		<div @mouseenter="mainMenuEnter()" @mouseleave="mainMenuLeave()" class="main_menuInfo" v-show="menuShow"  transition="hfadein">
			<ul>
				<li v-for="info in infoDetails">
					<a :href="info.sourcePath">
						<img :src="info.imgUrl" alt="info.name">
					</a>
					<div class="infoName">{{info.name}}</div>
					<div class="infoPrice">{{info.price}}</div>
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
export default {
	data () {
		return {
			items: [
				{name: '小米手机', type: 'xiaomi'},
				{name: '红米', type: 'red'},
				{name: '平板·笔记本', type: 'flats'},
				{name: '电视', type: 'tv'},
				{name: '盒子·影音', type: 'box'},
				{name: '路由器', type: 'router'},
				{name: '智能硬件', type: 'hardware'},
				{name: '服务', sourceUrl: '//www.mi.com/service/'},
				{name: '社区', sourceUrl: 'http://www.xiaomi.cn'}
			],
			inputItems: [
				{name: '红米pro', url: '#'},
				{name: '小米笔记本air', url: '#'}
			],
			searchItems: [
				{name: '小米手机5', count: '11'},
				{name: '空气净化器2', count: '1'},
				{name: '活塞耳机', count: '2'},
				{name: '小米路由器', count: '13'},
				{name: '移动电源', count: '5'},
				{name: '运动相机', count: '6'},
				{name: '小米摄像机', count: '9'},
				{name: '小米体重秤', count: '20'},
				{name: '小米插线板', count: '12'},
				{name: '配件优惠套装', count: '34'},
				{name: '小米跑鞋', count: '12'}
			],
			xiaomi: [
				{name: '小米Max', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/maxdingbu!160x110.jpg', sourcePath: 'http://www.mi.com/mimax/', price: '1299元起'},
				{name: '小米手机5', imgUrl: 'http://c1.mifile.cn/f/i/16/goods/nav/mi5!160x110.jpg', sourcePath: 'http://www.mi.com/mimax/', price: '1499元起'},
				{name: '小米手机4c', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/mi4c!160x110.jpg', sourcePath: 'http://www.mi.com/mimax/', price: '1099元'}
			],
			red: [
				{name: '红米pro', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/hongmipro-320!160x110.jpg', sourcePath: 'http://www.mi.com/mimax/', price: '1499元起'},
				{name: '红米note3', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/video/hongmi3s!160x110.jpg', sourcePath: 'http://www.mi.com/mimax/', price: '899元起'},
				{name: '红米手机3S', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/note3!160x110.jpg', sourcePath: 'http://www.mi.com/mimax/', price: '699元起'},
				{name: '红米手机3', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/hongmi3!160x110.jpg', sourcePath: 'http://www.mi.com/mimax/', price: '699元起'},
				{name: '红米手机3X', imgUrl: 'http://c1.mifile.cn/f/i/g/doodle/320-220!160x110.jpg', sourcePath: 'http://www.mi.com/mimax/', price: '799元'}
			],
			flats: [
				{name: '小米平板2 16GB', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/hongmipro-320!160x110.jpg', sourcePath: 'http://www.mi.com/mimax/', price: '999元'},
				{name: '小米平板2 64GB', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/mipad2-64!160x110.jpg', sourcePath: 'http://www.mi.com/mimax/', price: '1299元'},
				{name: '小米平板2 64GB Windows版', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/mipad2-64-win!160x110.jpg', sourcePath: 'http://www.mi.com/mimax/', price: '1299元'},
				{name: '小米笔记本Air 12.5', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/video/bijiben32012.5!160x110.jpg', sourcePath: 'http://www.mi.com/mimax/', price: '3499元'},
				{name: '小米笔记本Air 13.3', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/bijiben320!160x110.jpg', sourcePath: 'http://www.mi.com/mimax/', price: '4999元'}
			],
			tv: [
				{name: '小米电视3S 43英寸', imgUrl: 'http://c1.mifile.cn/f/i/16/goods/nav/mitv3s-43!160x110.jpg', sourcePath: 'http://www.mi.com/mitv3s/43/', price: '1499元'},
				{name: '小米电视3S 48英寸', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/mitv3s48!160x110.jpg', sourcePath: 'http://www.mi.com/mitv3s/48/', price: '1999元'},
				{name: '小米电视3 55英寸', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/mitv355!160x110.jpg', sourcePath: 'http://www.mi.com/mitv3/55/', price: '3299元起'},
				{name: '小米电视3 60英寸', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/mitv3-60!160x110.jpg', sourcePath: 'http://www.mi.com/mitv3/60/', price: '3499元'},
				{name: '小米电视3S 65英寸 曲面', imgUrl: 'http://c1.mifile.cn/f/i/16/goods/nav/mitv3s-65!160x110.jpg', sourcePath: 'http://www.mi.com/mimax/', price: '8999元'},
				{name: '小米电视3 70英寸', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/mitv70!160x110.jpg', sourcePath: 'http://www.mi.com/mitv3/70/', price: '8999元'}
			],
			box: [
				{name: '小米盒子mini版', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/hezimini.png', sourcePath: 'http://www.mi.com/hezimini/', price: '179元'},
				{name: '小米盒子3', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/hezi3.png', sourcePath: 'http://www.mi.com/hezi3/', price: '249元'},
				{name: '小米盒子3 增强版', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/hezi3s!160x110.jpg', sourcePath: 'http://www.mi.com/hezi3s/', price: '399元'},
				{name: '小米电视主机', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/zhuji!160x110.jpg', sourcePath: 'http://www.mi.com/tvzj/', price: '999元'},
				{name: '小米家庭音响 金属版', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/jinshuban!160x110.jpg', sourcePath: 'http://item.mi.com/1160800073.html', price: '899元'},
				{name: '小米家庭音响 标准版', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/putonban!160x110.jpg', sourcePath: 'http://item.mi.com/1160800074.html', price: '699元'}
			],
			router: [
				{name: '全新小米路由器', imgUrl: 'http://c1.mifile.cn/f/i/16/goods/nav/mitv3s-43!160x110.jpg', sourcePath: 'http://www.mi.com/mitv3s/43/', price: '699元起'},
				{name: '小米路由器 3', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/miwifi-3!160x110.jpg', sourcePath: 'http://www.mi.com/miwifi3/', price: '149元'},
				{name: '小米路由器 mini', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/miwifimini!160x110.jpg', sourcePath: 'http://www.mi.com/miwifimini/', price: '119元'},
				{name: '小米路由器 3C', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/mitv3-60!160x110.jpg', sourcePath: 'http://www.mi.com/mitv3/60/', price: '99元'},
				{name: '小米路由器 青春版', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/miwifilite!160x110.jpg', sourcePath: 'http://www.mi.com/miwifilite/', price: '69元'},
				{name: '小米WiFi放大器', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/wifiExtension!160x110.jpg', sourcePath: 'http://item.mi.com/1153200003.html', price: '35元'}
			],
			hardware: [
				{name: '九号平衡车', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/nav/scooter!160x110.jpg', sourcePath: 'http://www.mi.com/scooter/', price: '1999元'},
				{name: '小米净水器', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/water2!160x110.jpg', sourcePath: 'http://www.mi.com/water/', price: '1299元起'},
				{name: '米家压力IH电饭煲', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/dianfanbao!160x110.jpg', sourcePath: 'http://www.mi.com/dianfanbao/', price: '999元'},
				{name: '小米空气净化器 2', imgUrl: 'http://c1.mifile.cn/f/i/16/goods/nav/air2!160x110.jpg', sourcePath: 'http://www.mi.com/air2/', price: '649元'},
				{name: '智能摄像机', imgUrl: 'http://c1.mifile.cn/f/i/g/doodle/zhinengyingjian!160x110.jpg', sourcePath: 'http://list.mi.com/accessories/tag?id=shexiangji', price: '149元起'}
			],
			isRed: false,
			infoDetails: '',
			menuShow: false,
			timer: ''
		}
	},
	methods: {
		searchFocus: function () {
			this.isRed = true
		},
		searchBlur: function () {
			this.isRed = false
		},
		mainMenuEnter: function (type) {
			if (type) {
				this.infoDetails = this[type]
			}
			this.menuShow = true
			clearTimeout(this.timer)
		},
		mainMenuLeave: function (type) {
			let self = this
			this.timer = setTimeout(function () {
				self.menuShow = false
			}, 300)
		}
	}
}
</script>

<style scoped>
	.bar {
		width: 100%;
		height: 100px;
	}
	.mainBar {
		position: relative;
		width: 1226px;
		height: 100px;
		text-align: center;
		margin: 0 auto;
		display: flex;
		flex-flow: row;
		flex-wrap: nowrap;
		justify-content: flex-start;
		align-items: center;
	}
	.migift{margin-left: 19px;}
	.mainMenu {overflow: hidden;}
	.mainMenu li {
		float: left;
		height: 100px;
		line-height: 100px;
		margin:0 auto;
		color:#b0b0b0;
	}
	.mainMenu li a {
	    padding: 0 10px 0 10px;
	}
	.mainMenu li a:hover {
		color: red;
		cursor: pointer;
	}
	.bar-earch{
		height: 50px;
	    line-height: 50px;
	    position: absolute;
	    right: 0;
	    border: 1px solid #ccc;
	}
	.bar-earch input {
		float: left;
	    width: 240px;
	    height: 48px;
	    border: 0;
	    outline: none;
	}
	.seachBtn img {
		width: 20px;
	    height: 20px;
	    display: block;
	    margin-top: 15px;
	    margin-left: 15px;
	}
	.bar-earch label {
	 	display: block;
	    float: right;
	    width: 50px;
	    height: 100%;
	    border-left: 1px solid #e0e0e0;
	    cursor: pointer;
	}
	.on-input {
	 	position: absolute;
	    font-size: 10px;
	    right: 50px;
	}
	.on-input li {
	 	float: right;
    	margin-right: 5px;
	}
	.on-input li a {
	 	background: #eee;
    	padding: 2px 4px;
	}
	.borderRed { 
		border: 1px solid red;
	}
	.borderLeftred{
	 	border-left: 1px solid red !important;
	}
	.searchUl {
	 	position: absolute;
	    width: 240px;
	    border: 1px solid red;
	    top: 50px;
	    font-size: 12px;
	    z-index: 9998;
	    background: #fff;
	}
	.searchUl li{
	 	overflow: hidden;
	 	height: 20px;
    	line-height: 20px;
    	padding: 5px 7px;
    	cursor: pointer;
	}
	.search-name {
	 	float:left;
	}
	.search-count {
	 	float:right;
	 	color: #757575
	}
	.fadein-transition {
	  transition: all .5s ease;
	  opacity: 1;
	}
	.fadein-enter, .fadein-leave {
	  opacity: 0;
	}
	.hfadein-transition {
	  transition: all .5s ease;
	  height: 220px;
      overflow: hidden;
	}
	.hfadein-enter, .hfadein-leave {
	  height: 0;
	}
	.main_menuInfo{
		position: absolute;
		width: 100%;
		background: #fff;
		box-shadow: 1px 1px 1px 1px #eee;
		z-index: 99999;
	}
	.main_menuInfo ul {
		overflow: hidden;
		width: 1226px;
    	margin: 25px auto;
	}
	.main_menuInfo ul li {
		float: left;
		margin-right: 20px
	}
	.main_menuInfo ul li img{
		width: 160px;
    	height: 110px;
    	padding: 0 10px;
	}
	.main_menuInfo ul li a {
		display: block;
		border-right: 1px solid #eee
	}
	.main_menuInfo ul li:last-child a{
		border-right: 0
	}
	.main_menuInfo .infoName {
		text-align: center;
    	font-size: 13px;
    	margin-top: 10px
	}
	.main_menuInfo .infoPrice {
		text-align: center;
    	font-size: 10px;
    	color: red;
    	margin-top: 10px
	}
</style>
