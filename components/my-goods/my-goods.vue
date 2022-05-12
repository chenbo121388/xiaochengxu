<template>
	<view>
		<view class="good-item">
			<view class="good-item-left">
				<image :src="good.goods_small_logo" class="goods-pic"></image>
			</view>
			<view class="good-item-right">
				<view class="good-name">{{good.goods_name}}</view>
				<view class="good-info-box">
					<view class="goods-price">￥{{good.goods_price | tofixed}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"my-goods",
		props:{
			good:{
				type:Object,
			}
		},
		data() {
			return {
				
			};
		},
		filters:{
			tofixed(num){
				return Number(num).toFixed(2)
			}
		}
	}
</script>

<style lang="scss">
.good-item{
	display: flex;
	padding: 10px 5px;
	border-bottom: 1px solid #f0f0f0;
	.good-item-left{
		margin-right: 5px;
		.goods-pic{
			width: 100px;
			height: 100px;
			display: block;
		}
	}
	.good-item-right{
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		.good-name{
			font-size: 13px;
		}
		.goods-price{
			font-size: 16px;
			color: #c00000;
		}
	}
}
</style>