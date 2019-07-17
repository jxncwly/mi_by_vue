<template>
	<div class="goods-container">
		<goods-top-box></goods-top-box>
		<goods-collocation></goods-collocation>
		<goods-accessories></goods-accessories>
		<goods-around></goods-around>
		<recommend></recommend>
		<hot-product></hot-product>
		<goods-content></goods-content>
		<prod-video></prod-video>
	</div>
</template>

<script>
import GoodsTopBox from './GoodsTopBox'
import GoodsCollocation from './GoodsCollocation'
import GoodsAccessories from './GoodsAccessories'
import GoodsAround from './GoodsAround'
import Recommend from './Recommend'
import HotProduct from './HotProduct'
import GoodsContent from './GoodsContent'
import prodVideo from './prodVideo'

export default {
	components: {
		'goods-top-box': GoodsTopBox,
		'goods-collocation': GoodsCollocation,
		'goods-accessories': GoodsAccessories,
		'goods-around': GoodsAround,
		'recommend': Recommend,
		'hot-product': HotProduct,
		'goods-content': GoodsContent,
		'prod-video': prodVideo
	}
}
</script>

<style lang="postcss" scoped>
.goods-container {
	width: 100%;
	height: auto;
	background: #f5f5f5;
	padding-bottom: 40px;
}
</style>
