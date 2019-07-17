<template>
  <header class="top-container">
		<div class="top-bar clearfix">
			<div class="topbar-nav">
				<ul class="nav-wrap">
					<li v-for="(nav,index) in navs" class="nav clearfix" :key="index">
            <template v-if="nav.name === '小米商城'">
              	<a :href="nav.sourceUrl" class="nav-name">{{nav.name}}</a>
            </template>
            <template v-else>
              <a :href="nav.sourceUrl" class="nav-name" target="_blank">{{nav.name}}</a>
            </template>
						<span class="nav-separate" v-if="index !== 8">|</span>
					</li>
				</ul>
			</div>
			<div class="topbar-info">
				<a href="http://order.mi.com/site/login?redirectUrl=http://www.mi.com/index.html">登陆</a>
				<span class="nav-separate">|</span>
				<a href="https://account.xiaomi.com/pass/register">注册</a>
			</div>
			<div class="topbar-cart fa cart-arrow-down"
        @mouseenter="evtCartEnter"
        @mouseleave="evtCartOut">
				<div class="cart"
          :class="{'active': cartStatus}">
					<i class="iconfont">&#xe601;</i>
					<a href="http://static.mi.com/cart/">
						购物车(
						<span>0</span>
							)
					</a>
				</div>
        <transition name='topbarCart'>
          <div class="cart-list" v-show="cartStatus">
            购物车中还没有商品，赶快选购吧！
          </div>
        </transition>
			</div>

		</div>
  </header>
</template>

<script>
export default {
	data () {
		return {
			navs: [
				{name: '小米商城', sourceUrl: 'http://www.mi.com/index.html'},
				{name: 'MIUI', sourceUrl: 'http://www.miui.com/'},
				{name: '米聊', sourceUrl: 'http://www.miliao.com/'},
				{name: '游戏', sourceUrl: 'http://game.xiaomi.com/'},
				{name: '多看阅读', sourceUrl: 'http://www.duokan.com/'},
				{name: '云服务', sourceUrl: 'https://i.mi.com/'},
				{name: '小米网移动版', sourceUrl: 'http://www.mi.com/c/appdownload/'},
				{name: '问题反馈', sourceUrl: 'http://static.mi.com/feedback/'},
				{name: 'Select Region', sourceUrl: 'http://www.mi.com/index.html'}
			],
			timer: '',
			cartStatus: false
		}
	},
  ready () {
  },
	methods: {
		evtCartEnter: function () {
      this.cartStatus = true
      clearTimeout(this.timer)
		},
    evtCartOut: function () {
      let self = this
      this.timer = setTimeout(function () {
        self.cartStatus = false
      }, 200)
    }
	},
	components: {
	}
}
</script>

<style lang="postcss" scoped>

.top-container {
	width: 100%;
	height: 40px;
	background: #333;
}

.top-bar {
	position: relative;
	width: 1226px;
	margin: 0 auto;
	font-size: 12px;
  z-index: 11;
}

.topbar-nav {
	float: left;
	display: inline-block;
	height: 40px;
	line-height: 40px;
	overflow: hidden;
}

.nav-wrap {
	display: inline-block;
	margin: 0;
	padding: 0;
	list-style: none;
	& .nav {
		display: inline-block;
		font-size: 0;
		text-decoration: none;
		height: 40px;
		line-height: 40px;
		padding-left: 7px;
		& .nav-name {
			display: inline-block;
			font-size: 12px;
			color: #b0b0b0;
			text-decoration: none;
      &:hover {
			color: #fff;
		}
		}
		& .nav-separate {
			font-size: 12px;
			display: inline-block;
			color: #b0b0b0;
			margin-left: 7px;
		}
	}
}

.topbar-info {
	position: absolute;
	top: 0;
	right: 140px;
	height: 40px;
	line-height: 40px;
	& a {
		color: #b0b0b0;
		text-decoration: none;
    &:hover {
      color: #fff;
    }
	}
	& span {
		color: #b0b0b0;
	}
}

.topbar-cart {
	position: relative;
	float: right;
	width: 120px;
	background: #424242;
	height: 40px;
	line-height: 40px;
	cursor: pointer;
  &:hover {
    background: #fff;
    & i, & a {
      color: #ff6700;
    }
  }
	& a {
		display: block;
    width: 100%;
    height: 100%;
		padding-left: 40px;
		color: #b0b0b0;
		text-decoration: none;
    box-sizing: border-box;
	}
  & i {
		margin-right: 4px;
    font-size: 20px;
    line-height: 20px;
    position: absolute;
    left: 15px;
    top: 10px;
    color: #b0b0b0;
  }
}

.cart-list {
	position: absolute;
	right: 0;
	top: 39px;
  width: 316px;
  /* height: 96px; */
  line-height: 96px;
	text-align: center;
	color: #b0b0b0;
	background: #fff;
	box-shadow: 0 5px 5px #ccc;
  z-index: 15;
  /* overflow: hidden; */
}

.topbarCart-enter-active,
.topbarCart-leave-active {
  transition: all .5s ease;
  height: 96px;
}

.topbarCart-enter, .topbarCart-leave-to {
  height: 0;
}
</style>

