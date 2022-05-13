<template>
	<view>
		<view class="goods_list">
			<view v-for="(good,i) in goodsList" :key="i">
				<my-goods :good="good"></my-goods>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				queryObj: {
					query: '',
					cid: '',
					pagenum: 1,
					pagesize: 10
				},
				goodsList: [],
				total: 0,
				isloading:false
			};
		},
		onLoad(options) {
			this.queryObj.query = options.query || '',
				this.queryObj.cid = options.cid || '',
				this.getGoodsList()
		},
		methods: {
			async getGoodsList(cb) {
				this.isloading = true
				const {
					data: res
				} = await uni.$http.get('/api/public/v1/goods/search', this.queryObj)
				if (res.meta.status !== 200) return uni.$showMsg()
				this.goodsList = [...this.goodsList,...res.message.goods]
				this.total = res.message.total
				this.isloading = false
				cb && cb()
			}
			// gotoDetail(item){
			// 	uni.navigateTo({
			// 		url:'/subpkg/goods_detail/goods_detail?goods_id=' + item.goods_id
			// 	})
			// }
		},
		onReachBottom(){
			if(this.queryObj.pagenum * this.queryObj.pagesize >= this.total) return uni.$showMsg('数据加载完毕！')
			if(this.isloading) return
			this.queryObj.pagenum += 1
			this.getGoodsList()
		},
		onPullDownRefresh() {
			this.queryObj.pagenum = 1
			this.total = 0
			this.isloading = false
			this.goodsList = []
			this.getGoodsList(()=>uni.stopPullDownRefresh())
		}
	}
</script>

<style lang="scss">

</style>
