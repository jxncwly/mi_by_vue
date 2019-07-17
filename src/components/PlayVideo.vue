<template>
	<div class="video-mask" v-show="maskStatus">
    <transition name="slideIn">
		<div class="video-content"
			v-show="videoStatus">
			<div class="video-header clearfix">
				<h3 class="title-txt">{{playConfig.title}}</h3>
				<div class="cancel-link"
					@click="evtCancel">
					<i class="cancel-btn fa fa-times"></i>
				</div>
			</div>
			<div class="video">
				<iframe :src="playConfig.videoUrl" frameborder="0" allowfullscreen=""></iframe>
			</div>
		</div>
    </transition>
	</div>
</template>

<script>
import eventHub from '../eventHub'
export default {
  data () {
    return {
      maskStatus: false
    }
  },
  computed: {
    videoStatus () {
      return this.playConfig.status
    }
  },
  watch: {
    videoStatus (newVal, oldVal) {
      let that = this
      if (!newVal) {
        setTimeout(function () {
          that.maskStatus = that.videoStatus
        }, 500)
      } else {
        that.maskStatus = that.videoStatus
      }
    }
  },
	methods: {
		evtCancel () {
			let config = {
				status: false,
				title: this.playConfig.title
			}
			eventHub.$emit('cancelPlay', config)
		}
	},
	props: {
		playConfig: {
			required: true,
			type: Object
		}
	}
}
</script>

<style lang="postcss" scoped>
.video-mask {
	position: fixed;
	left: 0;
	top: 0;
	width: 100%;
	height: 100%;
	background: rgba(0, 0, 0, 0.5);
	z-index: 120;
}

.video-content {
	position: absolute;
	left: 0;
  right: 0;
	margin: 0 auto;
	width: 880px;
	/* height: 500px; */
	background: #fff;
}

.video-header {
	padding: 0px 20px;
	background: #f5f5f5;
  text-align: center;
  position: relative;
	& .title-txt {
		margin: 0;
		font-size: 18px;
		font-weight: 400;
		line-height: 32px;
		color: #424242;
	}
	& .cancel-link {
		display: block;
		position: absolute;
		top: 0;
    bottom: 0;
    margin: auto 0;
		right: 20px;
		width: 30px;
		height: 30px;
		line-height: 30px;
		text-align: center;
		border-radius: 30px;
		font-size: 24px;
		color: #757575;
		transition: all .2s;
		cursor: pointer;
		&:hover {
			color: #fff;
			background: #e53935;
		}
	}
}

.video {
	/* width: 100%; */
	height: 536px;
  & iframe {
    width: 100%;
    height: 100%;
  }
}

.slideIn-enter-active, .slideIn-leave-active {
  transition: all .3s linear;
	transform: translateY(0);
}

.slideIn-enter, .slideIn-leave-to {
	transform: translateY(-100%);
}
</style>
