<template>
	<div class="header-wrap">
		<h2 class="title">{{title}}</h2>
		<a class="top-sub" v-if="rightSub.sourceUrl" :href="rightSub.sourceUrl" target="_blank">
      <span>
        查看全部
        <i class="sub-icon fa fa-fw fa-chevron-circle-right"></i>
      </span>
    </a>
	</div>
</template>

<script>
export default {
	data () {
		return {
		}
	},
	props: {
		title: {
			required: true,
			type: String
		},
		rightSub: {
			type: Object,
			required: true
		}
	}
}
</script>

<style lang='postcss' scoped>
.header-wrap {
	position: relative;
	& .title {
		margin: 0;
		font-size: 22px;
		font-weight: 200;
		line-height: 58px;
		color: #333;
	}
	& .top-sub {
	  position: absolute;
		right: 0;
		top: 0;
	  display: block;
	  font-size: 16px;
	  line-height: 58px;
	  color: #424242;
	  cursor: pointer;
	  & .sub-icon {
	    color: #b0b0b0;
	    font-size: 20px;
	  }
	  &:hover {
	    color: #ff6700;
	    & .sub-icon {
	      color: #ff6700;
	    }
	  }
	}
}

</style>
