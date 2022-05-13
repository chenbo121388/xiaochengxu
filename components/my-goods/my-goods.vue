<template>
	<view class="container">
		<radio :checked="good.goods_state" color="#c00000" v-if="showRadio" @click="radioClickHandler" class="ra">
		</radio>
		<view class="good-item" @click="gotoDetail(good)">
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
		<uni-number-box :min="1" :value="good.goods_count" v-if="showNum" @change="numberChangeHandler"
			@blur="numberChangeHandler" class="num">
		</uni-number-box>
	</view>
</template>

<script>
	export default {
		name: "my-goods",
		props: {
			good: {
				type: Object,
			},
			showRadio: {
				type: Boolean,
				default: false
			},
			showNum: {
				type: Boolean,
				default: false
			}
		},
		data() {
			return {

			};
		},
		filters: {
			tofixed(num) {
				return Number(num).toFixed(2)
			}
		},
		methods: {
			radioClickHandler() {
				this.$emit('radio-change', {
					goods_id: this.good.goods_id,
					goods_state: !this.good.goods_state
				})
			},
			numberChangeHandler(val) {
				if (isNaN(val)) {
					this.$emit('num-change', {
						goods_id: this.good.goods_id,
						goods_count: 1
					})
					return
				}
				this.$emit('num-change', {
					goods_id: this.good.goods_id,
					goods_count: +val
				})
			},
			gotoDetail(item) {
				uni.navigateTo({
					url: '/subpkg/goods_detail/goods_detail?goods_id=' + item.goods_id
				})
			}
		}
	}
</script>

<style lang="scss">
	.container{
		height: 120px;
		clear: both;
	}
	.ra {
		float: left;
		position: relative;
		top: 45px;
		clear: both;
	}
	.num{
		float: right;
		display: inline-block;
		position: relative;
		right: 5px;
		bottom: 40px;
	}
	.good-item {
		display: flex;
		padding: 10px 5px;
		border-bottom: 1px solid #f0f0f0;

		.good-item-left {
			margin-right: 5px;
			display: flex;
			justify-content: space-between;
			align-items: center;

			.goods-pic {
				width: 100px;
				height: 100px;
				display: block;
			}
		}

		.good-item-right {
			display: flex;
			flex-direction: column;
			justify-content: space-between;

			.good-name {
				font-size: 13px;
			}

			.good-info-box {
				display: flex;
				align-items: center;
				justify-content: space-between;

				.goods-price {
					font-size: 16px;
					color: #c00000;
				}
			}
		}
	}
</style>
