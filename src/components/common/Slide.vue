<template>
	<div class="banner"
  @mouseenter="clearSlide"
  @mouseleave="autoSlide">
		<span
			@click="slidePre"
			class="slide-pre slide-control">
			<i class="fa fa-chevron-left fa-2x fa-fw icon-chevron-left"></i>
		</span>
		<span
			@click="slideNext"
			class="slide-next slide-control">
			<i class="fa fa-chevron-right fa-2x fa-fw icon-chevron-right"></i>
		</span>
    <ul>
    <li
			class="slide"
			v-for="(item,index) in banners"
      :key="index">
			<transition name="fadeIn">
        <a v-show="index === curpage" 
        :href="item.sourceUrl" target="_blank">
				<img :src="item.imgUrl" alt="" />
			</a>
      </transition>
		</li>
    </ul>
		
	</div>
</template>

<script>
export default {
	data () {
		return {
			prevTid: '',
			curpage: 0,
			slideDirection: 1
		}
  },
  computed: {
  },
	props: {
		banners: {
			type: Array,
      required: true
		}
	},
	created () {
		this.autoSlide()
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
		slidePre () {
			const lastPage = this.banners.length - 1
			if (this.curpage > 0) {
				this.curpage -= 1
			} else {
				this.curpage = lastPage
			}
		},
		autoSlide () {
			// clearInterval(this.prevTid)
			this.prevTid = setInterval(() => {
				this.slideNext()
			}, 3000)
    },
    clearSlide () {
      clearInterval(this.prevTid)
    }
	}
}
</script>

<style lang="postcss" scoped>
.banner {
	position: relative;
	width: 1226px;
	height: 460px;
	z-index: 0;
}

.slide-control {
  display: block;
	position: absolute;
	/* left: 235px; */
	top: 50%;
	width: 40px;
	height: 70px;
	margin-top: -35px;
	z-index: 10;
	cursor: pointer;
	&:hover{
		background: rgba(0, 0, 0, 0.3);
	}
}
.slide-pre {
	left: 235px;
}

.slide-next {
	right: 0;
}

.slide {
	position: absolute;
	left: 0;
	top: 0;
	width: 1226px;
	height: 460px;
	transition: all 0.3s;
  & a {
    display: block;
  }
	& img {
		width: 100%;
		height: 100%;
	}
}

.icon-chevron-left, .icon-chevron-right {
	position: absolute;
	left: 50%;
	top: 50%;
	width: 30px;
	height: 30px;
	margin-left: -15px;
	margin-top: -15px;
	color: #ecf0f1;
}

/* 轮播图过渡动画 */
.fadeIn-enter-active,
.fadeIn-leave-active {
  transition: all .5s ease;
	opacity: 1;
}
.fadeIn-enter, .fadeIn-leave-to {
  opacity: 0;
}

</style>
