<template>
	<span class="pull-left" @click="slideNext">
		<img class="pointImg" src='../../assets/img/chevron-left.png'>
	</span>
	<span class="pull-right" @click="slidpre">
		<img class="pointImg" src='../../assets/img/chevron-right.png'>
	</span>
	<div class="banner" v-for="banner in banners" 
		 v-show="$index === curpage" transition="fadein">
		<a :href="banner.sourceUrl">
			<img :src="banner.imgUrl">
		</a>
	</div>
</template>

<script>
export default {
	data () {
		return {
			bannerTimer: '',
			curpage: 0
		}
	},
	props: {
		banners: {
			type: Array,
			required: true
		}
	},
	ready () {
		this.autoPlay()
	},
	methods: {
		slideNext () {
			const lastPage = this.banners.length - 1
			if (this.curpage < lastPage) {
				this.curpage += 1
			} else {
				this.curpage = 0
			}
		},
		slidpre () {
			const lastPage = this.banners.length - 1
			if (this.curpage > 0) {
				this.curpage -= 1
			} else {
				this.curpage = lastPage
			}
		},
		autoPlay () {
			clearInterval(this.bannerTimer)
			this.bannerTimer = setInterval(() => {
				this.slideNext()
			}, 5000)
		}
	}
}
</script>

<style scoped>
/* 轮播图 点击下一张的时候获取图片的张数，判断当前的index是否大于图片的张数，如果大于调到第一张如果小于调到下一张  
点击上一张 判断当前idx是否大于0 大于0 的话 当前页数减去1  小于0 的话 就置为最后一张 */
	.banner {
		right: 0;
		top: 0;
		position: absolute;
		height: 100%;
	}
	.banner img {
		width: 100%;
		height: 100%
	}
	.pull-left {
		position: absolute;
		z-index: 999;
		display: block;
    	height: 70px;
    	left: 235px;
    	top:200px;
	}
	.pull-right {
		position: absolute;
		z-index: 999;
		display: block;
    	height: 70px;
    	left: 1185px;
    	top:200px;
	}
	.pointImg {
		height: 40px;
		width: 40px;
		margin-top: 15px
	}
	.fadein-transition {
	  transition: all .5s ease;
	  opacity: 1
	}
	.fadein-enter, .fadein-leave {
	  opacity:0;
	}
	.pull-right:hover,.pull-left:hover {
		background: #757575
	}
</style>
