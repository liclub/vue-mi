<template>
	<div class="content">
		<div class="bannerMenu" @mouseleave="bannerMenuLeave">
			<ul class="bannerMenuUl">
				<li v-for="menu in sideItems" @mouseenter="bannerMenuEnter(menu.type)" >
					<a>{{menu.content}}</a>
				</li>
			</ul>
			<div class="bannerMenuInfo" v-show="isShowInfo">
				<ul  v-for="items in currentInfo">
					<li v-for="item in items">
						<a class="bannerMenuInfoA" :href="item.sourceUrl">
							<img :src="item.imgUrl">
							<div class="productName">{{item.name}}</div>
						</a>
						<div class="buybtn" v-show="item.buyStatus == true">
							<a :href="item.buyUrl" class="buyhref">购买</a>
						</div>
						
					</li>
				</ul>
			</div>
		</div>
		<banner-slide :banners="banners"></banner-slide>
	</div>
</template>

<script>
import slide from './common/slide.vue'
export default {
	data () {
		return {
			sideItems: [
				{type: 'phones', content: '手机 电话卡'},
				{type: 'computer', content: '笔记本 平板'},
				{type: 'box', content: '电视 盒子'},
				{type: 'router', content: '路由器 智能硬件'},
				{type: 'power', content: '移动电源 电池 插线板'},
				{type: 'headset', content: '耳机 音响'},
				{type: 'foil', content: '保护套 贴膜'},
				{type: 'line', content: '线材 支架 存储卡'},
				{type: 'bags', content: '箱包 服饰'},
				{type: 'rabbit', content: '兔米 生活周边'}],
			banners: [
				{sourceUrl: '//item.mi.com/buyphone/mi5', imgUrl: 'https://i1.mifile.cn/a4/xmad_1504686766558_dhASO.jpg'},
				{sourceUrl: '//item.mi.com/buyphone/hongmi3s', imgUrl: 'https://i1.mifile.cn/a4/xmad_15045977666042_AFXHR.jpg'},
				{sourceUrl: '//item.mi.com/buyphone/mimax', imgUrl: 'https://i1.mifile.cn/a4/xmad_15045782791781_VzwBk.jpg'},
				{sourceUrl: '//item.mi.com/buyphone/note3', imgUrl: 'https://i1.mifile.cn/a4/xmad_15045220219659_nXwdK.jpg'},
				{sourceUrl: '//item.mi.com/buymitv/48', imgUrl: 'https://i1.mifile.cn/a4/xmad_15045196417602_uBKlq.jpg'},
				{sourceUrl: '//item.mi.com/buymitv/48', imgUrl: 'https://i1.mifile.cn/a4/xmad_15046615492359_RaMfH.jpg'}
			],
			phones: [
				{sourceUrl: '//www.mi.com/mi5/', buyUrl: '//item.mi.com/buyphone/mi5', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/list/mi5bar80.jpg?width=40&height=40', name: '小米手机5', buyStatus: true},
				{sourceUrl: '//www.mi.com/mimax/', buyUrl: '//item.mi.com/buyphone/mimax', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/maxbar80.jpg?width=40&height=40', name: '小米Max', buyStatus: true},
				{sourceUrl: '//www.mi.com/note3/pro/', buyUrl: '//item.mi.com/buyphone/note3', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/note3.jpg?width=40&height=40', name: '小米Note3', buyStatus: true},
				{sourceUrl: '//www.mi.com/hongmi3s/', buyUrl: '//item.mi.com/buyphone/hongmi3s', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/video/hm3s80x80.jpg?width=40&height=40', name: '红米手机3S', buyStatus: true},
				{sourceUrl: '//www.mi.com/redmipro/', buyUrl: '//item.mi.com/buyphone/redmipro/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/hongmi3.jpg?width=40&height=40', name: '红米Pro', buyStatus: true},
				{sourceUrl: '//www.mi.com/hongmi3/', buyUrl: '//item.mi.com/buyphone/hongmi3/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/list/mi5bar80.jpg?width=40&height=40', name: '红米手机3', buyStatus: true},
				{sourceUrl: '//www.mi.com/hongmi3x/', buyUrl: '//item.mi.com/buyphone/hongmi3x', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/video/3X80.jpg?width=40&height=40', name: '红米手机3X', buyStatus: true},
				{sourceUrl: '//heyue.mi.com/', buyUrl: '//item.mi.com/buyphone/mi5', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/heyue.jpg?width=40&height=40', name: '合约机', buyStatus: false},
				{sourceUrl: '//www.mi.com/compare/', buyUrl: '//item.mi.com/buyphone/mi5', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/compare.jpg?width=40&height=40', name: '对比手机', buyStatus: false},
				{sourceUrl: '//www.mi.com/mimobile/', buyUrl: '//item.mi.com/buyphone/mi5', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/mimobile.jpg?width=40&height=40', name: '小米移动 电话卡', buyStatus: false}
			],
			computer: [
				{sourceUrl: '//www.mi.com/mibookair/', buyUrl: '//item.mi.com/buymibook/air', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/bijiben80.jpg?width=40&height=40', name: '小米笔记本Air', buyStatus: true},
				{sourceUrl: '//www.mi.com/mipad2/', buyUrl: '//item.mi.com/static/buymipad', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/pad2.png?width=40&height=40', name: '小米平板2', buyStatus: true},
				{sourceUrl: '//item.mi.com/1163000011.html', buyUrl: '//item.mi.com/buyphone/mi5', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/usbzjqggg80.jpg?width=40&height=40', name: 'USB-C转接器', buyStatus: false},
				{sourceUrl: '//item.mi.com/1163100001.html', buyUrl: '//item.mi.com/buyphone/mi5', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/neidanbao80.jpg?width=40&height=40', name: '小米笔记本内胆包', buyStatus: false}
			],
			box: [
				{sourceUrl: '//www.mi.com/mitv3s/43/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/4380side.jpg?width=40&height=40', name: '小米电视 43英寸', buyStatus: false},
				{sourceUrl: '//www.mi.com/mitv3s/48/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/mitv3s48.jpg?width=40&height=40', name: '小米电视 48英寸', buyStatus: false},
				{sourceUrl: '//www.mi.com/mitv3/55/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/tv3-55.jpg?width=40&height=40', name: '小米电视 55英寸', buyStatus: false},
				{sourceUrl: '//www.mi.com/mitv3/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/tv60.jpg?width=40&height=40', name: '小米电视 60英寸', buyStatus: false},
				{sourceUrl: '//www.mi.com/mitv3s/65/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/6580side.jpg?width=40&height=40', name: '小米电视 65英寸', buyStatus: false},
				{sourceUrl: '//www.mi.com/mitv3/70/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/tv70.png?width=40&height=40', name: '小米电视 70英寸', buyStatus: false},
				{sourceUrl: '//www.mi.com/tvzj/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/tvzj.jpg?width=40&height=40', name: '小米电视主机', buyStatus: false},
				{sourceUrl: '//www.mi.com/hezi3s/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/hezizengqiangban80side.jpg?width=40&height=40', name: '小米盒子3 增强版', buyStatus: false},
				{sourceUrl: '//www.mi.com/hezi3/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/hezis.jpg?width=40&height=40', name: '小米盒子3', buyStatus: false},
				{sourceUrl: '//www.mi.com/hezimini/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/hezimini.jpg?width=40&height=40', name: '小米盒子 mini', buyStatus: false},
				{sourceUrl: '//item.mi.com/1154100018.html', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/diyinpao.jpg?width=40&height=40', name: '小米低音炮', buyStatus: false},
				{sourceUrl: '//www.mi.com/shb/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/shb.jpg?width=40&height=40', name: '蓝牙手柄', buyStatus: false},
				{sourceUrl: '//list.mi.com/accessories/tag?id=yinxiang', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/zuheyinxiang80side.jpg?width=40&height=40', name: '家庭音响', buyStatus: false},
				{sourceUrl: '//list.mi.com/tvboxpj', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/dianshipeijian.jpg?width=40&height=40', name: '电视盒子配件', buyStatus: false}
			],
			router: [
				{sourceUrl: '//www.mi.com/mivr1c/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/vr8080.jpg?width=40&height=40', name: '小米VR眼镜玩具版', buyStatus: false},
				{sourceUrl: '//www.mi.com/miuav/', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/video/wurenji80.jpg?width=40&height=40', name: '小米无人机', buyStatus: false},
				{sourceUrl: '//www.mi.com/miwifi3/', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/luyouqi-80.jpg?width=40&height=40', name: '小米路由器', buyStatus: false},
				{sourceUrl: '//www.mi.com/scooter/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/list/scooter.jpg?width=40&height=40', name: '九号平衡车', buyStatus: false},
				{sourceUrl: '//www.mi.com/dianfanbao/', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/dianfanbao-80.jpg?width=40&height=40', name: '米家压力IH电饭煲', buyStatus: false},
				{sourceUrl: '//www.mi.com/kettle/', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/video/shuihu80.jpg?width=40&height=40', name: '米家恒温电水壶', buyStatus: false},
				{sourceUrl: '//www.mi.com/mibicycle/', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/zxc80-80.jpg?width=40&height=40', name: '电助力折叠自行车', buyStatus: false},
				{sourceUrl: '//list.mi.com/accessories/tag?id=shexiangji', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/xiaobai80.jpg?width=40&height=40', name: '摄像机', buyStatus: false},
				{sourceUrl: '//list.mi.com/accessories/tag?id=jinghuaqilvxin', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/video/jinghuaqilvxin80.jpg?width=40&height=40', name: '净化器及滤芯', buyStatus: false},
				{sourceUrl: '//list.mi.com/accessories/tag?id=water', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/jingshuiqiandlvxin-80.jpg?width=40&height=40', name: '净水器及滤芯', buyStatus: false},
				{sourceUrl: '//list.mi.com/accessories/tag?id=xueyaji', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/xueyaji-80.jpg?width=40&height=40', name: '血压计', buyStatus: false},
				{sourceUrl: '//list.mi.com/accessories/tag?id=smartlamp', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/zhinengdeng-80.jpg?width=40&height=40', name: '智能灯', buyStatus: false},
				{sourceUrl: '//www.mi.com/mitu/', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/gushiji80.jpg?width=40&height=40', name: '米兔智能故事机', buyStatus: false},
				{sourceUrl: '//list.mi.com/accessories/smartsuit', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/zhinengjiatingtaozhuang-80.jpg?width=40&height=40', name: '智能家庭组合', buyStatus: false},
				{sourceUrl: '//list.mi.com/accessories/shouhuan', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/video/shouhuan280.jpg?width=40&height=40', name: '手环及配件', buyStatus: false},
				{sourceUrl: '//www.mi.com/scale/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/scale.jpg?width=40&height=40', name: '体重秤', buyStatus: false},
				{sourceUrl: '//www.mi.com/mituwatch/', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/shoubiao3-80.jpg?width=40&height=40', name: '米兔儿童电话手表', buyStatus: false},
				{sourceUrl: '//list.mi.com/26?cfrom=search', imgUrl: 'http://c1.mifile.cn/f/i/g/doodle/znyjdaohang.jpg?width=40&height=40', name: '全部智能硬件', buyStatus: false}
			],
			power: [
				{sourceUrl: '//www.mi.com/dianyuan/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/dianyuan.jpg?width=40&height=40', name: '小米移动电源', buyStatus: false},
				{sourceUrl: '//list.mi.com/accessories/tag?id=powerstrip', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/powerscript.jpg?width=40&height=40', name: '小米插线板', buyStatus: false},
				{sourceUrl: '//list.mi.com/13', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/yidongdianyuan.jpg?width=40&height=40', name: '品牌移动电源', buyStatus: false},
				{sourceUrl: '//list.mi.com/dyfj', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/dianyuanfujian.jpg?width=40&height=40', name: '移动电源附件', buyStatus: false},
				{sourceUrl: '//list.mi.com/14', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/video/charger80.jpg?width=40&height=40', name: '电池', buyStatus: false},
				{sourceUrl: '//list.mi.com/15', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/chongdianqi-80.jpg?width=40&height=40', name: '充电器', buyStatus: false},
				{sourceUrl: '//item.mi.com/1154300033.html', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/5Battery1.jpg?width=40&height=40', name: '彩虹5号电池', buyStatus: false},
				{sourceUrl: '//item.mi.com/1155000010.html', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/7Battery1.jpg?width=40&height=40', name: '彩虹7号电池', buyStatus: false}
			],
			headset: [
				{sourceUrl: '//www.mi.com/headphone/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/headphone.jpg?width=40&height=40', name: '小米头戴式耳机', buyStatus: false},
				{sourceUrl: '//www.mi.com/quantie/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/quantie.jpg?width=40&height=40', name: '小米圈铁耳机', buyStatus: false},
				{sourceUrl: '//www.mi.com/capsuleearphone/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/jiaonang80.jpg?width=40&height=40', name: '小米胶囊耳机', buyStatus: false},
				{sourceUrl: '//www.mi.com/huosai2/', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/jichuban-80.jpg?width=40&height=40', name: '小米活塞耳机 基础版', buyStatus: false},
				{sourceUrl: '//www.mi.com/bluetooth-headset/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/bluetoothheadset.jpg?width=40&height=40', name: '小米蓝牙耳机', buyStatus: false},
				{sourceUrl: '//list.mi.com/18', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/video/pinpai80.jpg?width=40&height=40', name: '品牌耳机', buyStatus: false},
				{sourceUrl: '//www.mi.com/pocketaudio/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/pocketaudio.png?width=40&height=40', name: '小米蓝牙音箱', buyStatus: false},
				{sourceUrl: '//www.mi.com/littleaudio/', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/suishen-80.jpg?width=40&height=40', name: '小米随身蓝牙音箱', buyStatus: false},
				{sourceUrl: '//www.mi.com/yinxiang/', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/xiaogangpao2-hei-80.jpg?width=40&height=40', name: '小钢炮音箱 2', buyStatus: false},
				{sourceUrl: '//www.mi.com/speaker/', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/qignchungangpao-80.jpg?width=40&height=40', name: '小钢炮音箱 青春版', buyStatus: false},
				{sourceUrl: '//item.mi.com/1154400010.html', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/fanghezi.jpg?width=40&height=40', name: '小米方盒子音箱', buyStatus: false},
				{sourceUrl: '//item.mi.com/1163100008.html', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/mituyinx80.jpg?width=40&height=40', name: '小米米兔音箱', buyStatus: false},
				{sourceUrl: '//www.mi.com/radio/', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/radio80side.jpg?width=40&height=40', name: '网络收音机', buyStatus: false},
				{sourceUrl: '//list.mi.com/accessories/soundbox', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/pinpaiyinxiang.jpg?width=40&height=40', name: '品牌音箱', buyStatus: false}
			],
			foil: [
				{sourceUrl: '//list.mi.com/9', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/tiemo.jpg?width=40&height=40', name: '贴膜', buyStatus: false},
				{sourceUrl: '//list.mi.com/8', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/baohu.jpg?width=40&height=40', name: '保护套/保护壳', buyStatus: false},
				{sourceUrl: '//list.mi.com/2', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/hougai.jpg?width=40&height=40', name: '后盖', buyStatus: false},
				{sourceUrl: '//list.mi.com/3', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/video/tiezhi80.jpg?width=40&height=40', name: '背贴', buyStatus: false}
			],
			line: [
				{sourceUrl: '//list.mi.com/16', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/xiancai.jpg?width=40&height=40', name: '线材', buyStatus: false},
				{sourceUrl: '//search.mi.com/search_%E8%87%AA%E6%8B%8D%E6%9D%86', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/zipaigan.jpg?width=40&height=40', name: '自拍杆', buyStatus: false},
				{sourceUrl: '//list.mi.com/5', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/zhijia.jpg?width=40&height=40', name: '手机支架', buyStatus: false},
				{sourceUrl: '//list.mi.com/27', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/cunchu.jpg?width=40&height=40', name: '存储卡', buyStatus: false}
			],
			bags: [
				{sourceUrl: '//list.mi.com/23', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/xiangbao-80.jpg?width=40&height=40', name: '箱包', buyStatus: false},
				{sourceUrl: '//search.mi.com/search_%E6%97%85%E8%A1%8C%E7%AE%B1', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/lvxingxiang.jpg?width=40&height=40', name: '90分旅行箱', buyStatus: false},
				{sourceUrl: '//list.mi.com/22', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/fuzhuang-80.jpg?width=40&height=40', name: '服饰', buyStatus: false}
			],
			rabbit: [
				{sourceUrl: 'http://mitu.mi.com/', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/mitu-80.jpg?width=40&height=40', name: '米兔玩偶', buyStatus: false},
				{sourceUrl: '//list.mi.com/59', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/shubiaodian-80.jpg?width=40&height=40', name: '鼠标垫', buyStatus: false},
				{sourceUrl: '//list.mi.com/24', imgUrl: 'http://c1.mifile.cn/f/i/15/goods/sidebar/zhoubian1.jpg?width=40&height=40', name: '生活周边', buyStatus: false},
				{sourceUrl: '//www.mi.com/zazhi/index.html', imgUrl: 'http://c1.mifile.cn/f/i/g/2015/cn-index/zazhi-80-80.jpg?width=40&height=40', name: '《小米》杂志', buyStatus: false}
			],
			showInfo: [],
			isShowInfo: false,
			showTimer: ''
		}
	},
	methods: {
		bannerMenuEnter (type) {
			if (type) {
				this.showInfo = this[type]
			}
			clearInterval(this.showTimer)
			this.isShowInfo = true
		},
		bannerMenuLeave () {
			this.isShowInfo = false
		}
	},
	computed: {
		currentInfo: function () {
			let showList = [ [], [], [], [], [] ]
			this.showInfo.forEach(function (item, idx) {
				let goodsIdx = Math.floor(idx / 6)
				showList[goodsIdx].push(item)
			})
			return showList
		}
	},
	components: {
		'banner-slide': slide
	}
}
</script>

<style scoped>
	.content{
		width: 1226px;
		position: relative;
		height: auto;
		margin:0 auto;
	}
	.bannerMenu{
		width: 235px;
	    background: black;
	    z-index: 9999;
	    position: relative;
	    background: rgba(0,0,0,0.6);
	}
	.bannerMenu .bannerMenuUl {
		padding-bottom: 30px;
		padding-top: 30px;
    	text-align: center;
	}
	.bannerMenu .bannerMenuUl li {
		height: 40px;
   		line-height: 40px;
	}
   	.bannerMenu .bannerMenuUl li a {
   		width: 100%;
	    height: 100%;
	    display: block;
		color:#fff;
		font-size: 14px;
		cursor: pointer
   	}
	.bannerMenu .bannerMenuUl li:hover{
		background: #ff6700;
	}
	.bannerMenuInfo {
		position: absolute;
	    left: 235px;
	    height: 100%;
	    top: 0;
	    background: #fff;
	    overflow: hidden;
	    display: flex;
		flex-flow: row nowrap;
		justify-content: flex-start;
	}
	.bannerMenuInfo ul {
		padding-bottom: 0px;
		padding-top: 0px;
		height: 100%;
		float: left;
	}
	.bannerMenuInfo ul li {
		width: 240px;
		padding: 20px 25px 10px 10px;
	}
	.bannerMenuInfo ul li .bannerMenuInfoA {
		color: black;
		width: 80%;
	    height: 100%;
	    display: inline-block;
		font-size: 14px;
		cursor: pointer;
		overflow: hidden;
	}
	.bannerMenuInfo ul li img {
		float:left;
	}
	.bannerMenuInfo ul li .productName{
		height: 40px;
	    line-height: 40px;
	    margin-left: 16px;
	    float: left;
	}
	.bannerMenuInfo .buybtn {
		display: block;
	    float: right;
	    height: 40px;
	    line-height: 40px;
	}
	.bannerMenuInfo .buyhref {
		padding: 2px 10px;
		border: 1px solid #ff6700;
		color: #ff6700;
		font-size: 13px;
	}
	.bannerMenuInfo .buyhref:hover {
		background: #ff6700;
		color: #fff
	}
</style>
