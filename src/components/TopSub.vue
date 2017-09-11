<template>
	<div class="sub_content">
		<div class="sub_area">
			<div class="sub-iconArea" v-for="icon in iconList">
				<a href="icon.toUrl" target="_blank">
					<i v-bind:class="icon.icontype" class="fa fa-fw sub-icon"></i>
				    <div class="sub-fontname" v-bind:class="{paddBottom : $index == '3' ||  $index == '4' ||  $index == '5' }">{{icon.name}}</div>
				</a>
				<template v-if="$index == '0' || $index == '1' || $index == '2' ">
					<div class="rowline"></div>
				</template>
				<template v-if="$index == '0' || $index == '1' || $index == '3' || $index == '4' ">
					<div class="colline"></div>
				</template>
			</div>
		</div>
		<div class="subimg_area" v-for="img in imgList">
			<a href="{{img.linkUrl}}" target="_blank">
				<img src="{{img.imgUrl}}">
			</a>
		</div>
	</div>
</template>

<script>
export default {
	data () {
		return {
			iconList: [
				{icontype: 'fa-mobile', name: '选购手机', toUrl: 'http://www.mi.com/compare/'},
				{icontype: 'fa-gift', name: '企业团购', toUrl: 'http://qiye.mi.com/'},
				{icontype: 'fa-refresh', name: '官翻产品', toUrl: 'http://item.mi.com/re'},
				{icontype: 'fa-credit-card', name: '小米移动', toUrl: 'http://huanxin.mi.com/product/list'},
				{icontype: 'fa-recycle', name: '以旧换新', toUrl: 'http://huanxin.mi.com/product/list'},
				{icontype: 'fa-credit-card-alt', name: '话费充值', toUrl: 'http://recharge.10046.mi.com/'}
			],
			imgList: [
				{imgUrl: 'http://i3.mifile.cn/a4/1327d707-4f67-4c36-8ae5-3d7704c989eb', linkUrl: 'http://hd.mi.com/y/08191p/index.html'},
				{imgUrl: 'http://i3.mifile.cn/a4/c202123c-4197-4666-9793-2f1e156ab23a', linkUrl: 'https://www.mi.com/index.html'},
				{imgUrl: 'http://i3.mifile.cn/a4/216f7f38-66ee-4c1b-8409-8d77cb64d386', linkUrl: 'http://item.mi.com/buy/mipad2'}
			]
		}
	}
}
</script>

<style scoped>
	.sub_content {
		width: 1226px;
		height: auto;
		margin: 15px auto;
		display: flex;
		flex-wrap: wrap;
		justify-content: flex-start;
		align-items: center;
	}
	.sub_area{
		width: 235px;
		height:100%;
		margin: 0 20px 0 20px;
		display: flex;
		flex-wrap: wrap;
		justify-content: flex-start;
		align-items: center;
		background:#5f5750;
	}
	.sub-iconArea {
		width: 58px;
    	text-align: center;
    	margin:9px;
    	margin-top:15px;
    	position: relative;
	}
	.sub-iconArea a{
		color: #cdcac8;
		color: #cdcac8;
	}
	.sub-icon {
		font-size: 20px;
    	padding-top: 5px;
	}
	.sub-fontname {
		font-size: 12px;
	    margin-top: 7px;
	    padding-bottom: 5px;
	}
	.sub_area:first-child {
		margin-left: 0
	}
	.rowline{
		height: 1px;
		width: 50px;
		margin-left: 5px;
		margin-top: 20px;
		background: rgba(255,255,255,0.1);
	}
	.colline {
		height: 65px;
	    width: 1px;
	    position: absolute;
	    left: 68px;
	    top: -10px;
		background: rgba(255,255,255,0.1);
	}
	.sub-iconArea a:hover {
		color:#fff
	}
	.paddBottom{
		padding-bottom: 10px
	}
	.subimg_area{
		width: 310px;
		height: 176px;
		margin-right: 20px
	}
	.subimg_area img{
		width: 100%;
		height: 100%;
	}
	.subimg_area img:hover{
		box-shadow: 0 5px 30px #ccc;
	}
	.subimg_area:last-child {
		margin-right: 0
	}
</style>