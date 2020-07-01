<template>
	<view class="shoppingCart">
		<view class="shop" v-for="(item, index) in shop" :key="index">
			<view class="shop-top clearfix">
				<checkbox class="va-top checkbox" @click="allSelect(item)" :value="item.id" :checked="item.checked" />
				<view class="st-title display-ib">
					<image class="shop-icon fl" src="../../static/images/shops/shops.png" mode="widthFix"></image>
					<text class="fl">{{ item.name }}</text>
					<image class="icon-right fl" src="../../static/images/shops/right-icon.png" mode="widthFix"></image>
				</view>
				<!-- <icon @click="deleteSingle(item)" class="fr" type="cancel" size="20"/> -->
			</view>
			<template v-for="(ite, inde) in item.list">
				<view class="shop-content clearfix" :key="inde">
					<checkbox class="fl checkbox" @click="selectSingle(ite)" :value="ite.id" :checked="ite.checked" />
					<image class="commodity fl" src="../../static/images/index/activity_1.png" mode="widthFix"></image>
					<view class="sc-right fr clearfix">
						<text class="scr-title">{{ ite.title }}</text>
						<text class="secondary display-ib">{{ ite.secondary }}</text>
						<view class="clearfix">
							<text class="fl red">￥{{ ite.price }}</text>
							<view class="number clearfix fr">
								<text @click="deleteNumber(ite)">-</text>
								<text class="text" @click="changeNumber(ite)">{{ ite.number }}</text>
								<text @click="addNumber(ite)">+</text>
							</view>
						</view>
					</view>
				</view>
			</template>
		</view>
		<view class="settlement">
			<checkbox @click="allShopSelect(allShopChecked)" class="va-top checkbox" value="all" :checked="allShopChecked" />
			<view class="settlement-right fr">
				<text>合计：</text>
				<text class="red">￥{{ settlement }}</text>
				<button type="warn" size="mini">结算（{{ number }}）</button>
			</view>
			<text v-show="number" class="clear" @click="clickDelete">删除</text>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'shoppingCart',
		data() {
			return {
				shop: [
					{
						name: '红鑫羽生鲜专营店',
						id: '1',
						checked: false,
						list: [
							{
								title: '芒果新鲜水果 进口玉芒带箱10斤装优选精品果 鲜果直发 热带水果 新鲜青芒 苏宁生鲜',
								secondary: '果粒饱满多汁 甜蜜爆炸',
								price: 40,
								maxNumber: 5,
								id: '1-1',
								number: 1,
								checked: false
							},
							{
								title: '芒果新鲜水果 进口玉芒带箱10斤装优选精品果 鲜果直发 热带水果 新鲜青芒 苏宁生鲜',
								secondary: '果粒饱满多汁 甜蜜爆炸',
								price: 40,
								maxNumber: 200,
								id: '1-2',
								number: 1,
								checked: false
							}
						]
					},
					{
						name: '红鑫羽生鲜专营店',
						id: '2',
						checked: true,
						list: [
							{
								title: '芒果新鲜水果 进口玉芒带箱10斤装优选精品果 鲜果直发 热带水果 新鲜青芒 苏宁生鲜',
								secondary: '果粒饱满多汁 甜蜜爆炸',
								price: 40,
								maxNumber: 200,
								id: '2-1',
								number: 1,
								checked: true
							}
						]
					},
					{
						name: '红鑫羽生鲜专营店',
						id: '3',
						checked: false,
						list: [
							{
								title: '芒果新鲜水果 进口玉芒带箱10斤装优选精品果 鲜果直发 热带水果 新鲜青芒 苏宁生鲜',
								secondary: '果粒饱满多汁 甜蜜爆炸',
								price: 40,
								maxNumber: 200,
								id: '3-1',
								number: 1,
								checked: false
							}
						]
					}
				],
				settlement: 0,
				number: 0,
				allShopChecked: false
			}
		},
		created() {
			this.changeNumber()
		},
		methods: {
			// 改变数量时-计算金额
			changeNumber() {
				let settlement = 0
				let number = 0
				let isAll = true
				this.shop.forEach((item, index) => {
					// 针对店铺
					let temp = 0
					let end = item.list.length

					item.list.forEach((ite, inde) => {
						if (ite.checked) {
							settlement += ite.price * ite.number
							number += 1
							temp++
						} else {
							isAll = false
						}
					})
					
					// 针对店铺-全选的复选框
					if (temp === end) {
						item.checked = true
					} else {
						item.checked = false
					}
				})
				
				if (isAll) {
					this.allShopChecked = true
				} else {
					this.allShopChecked = false
				}
				
				this.settlement = settlement
				this.number = number
			},
			// 添加商品数量
			addNumber(ite) {
				if (ite.number >= ite.maxNumber) {
					return false
				}
				ite.number++
				this.changeNumber()
			},
			// 减少商品数量
			deleteNumber(ite) {
				if (ite.number <= 1) {
					return false
				}
				ite.number--
				this.changeNumber()
			},
			// 全选 || 全不选 - 针对店铺
			allSelect(item) {
				console.log(1)
				const checked = item.checked
				item.list.forEach((ite, inde) => {
					if (checked) {
						ite.checked = false
					} else {
						ite.checked = true
					}
				})
				item.checked = !item.checked
				this.changeNumber()
			},
			// 全选 || 全不选 - 针对所有商品
			allShopSelect(checked) {
				this.shop.forEach((item, index) => {
					if (checked) {
						item.checked = false
					} else {
						item.checked = true
					}
					item.list.forEach((ite, inde) => {
						if (checked) {
							ite.checked = false
						} else {
							ite.checked = true
						}
					})
				})
				
				this.allShopChecked = !this.allShopChecked
				this.changeNumber()
			},
			// 单选
			selectSingle(item) {
				item.checked = !item.checked
				this.changeNumber()
			},
			// 点击选中删除商品
			clickDelete() {
				uni.showModal({
				    title: '提示',
				    content: `是否确认删除这${this.number}件商品`,
				    success: (res) => {
				        if (res.confirm) {
				            this.deleteShops()
							this.changeNumber()
				        } else if (res.cancel) {
				            console.log('用户点击取消')
				        }
				    }
				})
			},
			// 删除选中商品
			deleteShops() {
				const shop = this.shop.filter((item, index) => {
					let obj = {}
					if (item.checked) {
					} else {
						let arr = item.list.filter((ite, inde) => {
							if (!ite.checked) {
								return ite
							}
						})
						
						if (arr.length > 0) {
							item.list = arr
							return item
						}
					}
				})
				this.shop = shop
			},
			
		}
	}
</script>

<style>
	.checkbox >>> .uni-checkbox-input {
		width: 14px;
		height: 14px;
		border-radius: 50%;
		border-color: #01DC4F;
	}
	
	.checkbox >>> .uni-checkbox-input.uni-checkbox-input-checked:before {
		font-size: 14px;
		font-weight: bold;
		color: #01DC4F !important;
	}
	
	.checkbox:not([disabled]) >>> .uni-checkbox-input:hover {
		border-color: #01DC4F;
	}
</style>
<style lang="scss" scoped>
	$green: #01DC4F;

	.number {
		width: 60pt;
		height: 15pt;
		display: flex;
		color: $green;
		font-size: 12px;
		line-height: 15pt;
		text-align: center;
		border-radius:5px;
		margin-right: 24px;
		border: 1px solid $green;
		
		text {
			flex: 1;
		}
		
		.text {
			border-left: 1px solid $green;
			border-right: 1px solid $green;
		}
	}
	
	.shoppingCart {
		height: 1200px;
		padding: 20px;
		font-size: 14px;
		position: relative;
		background-color: #f5f6f8;

		.shop {
			border-radius: 5px;
			margin-bottom: 12px;
			background-color: #fff;
			padding: 12px 0 12px 12px;

			.shop-top {
				height: 26px;
				padding-right: 10px;
				line-height: 26px;

				.st-title {
					image {
						margin-top: 7px;
					}
					
					text {
						color: #333;
						margin: 0 10px 0 5px;
					}
					
					.shop-icon {
						width: 14px;
					}
					
					.icon-right {
						width: 6px;
					}
				}
			}
		
			.shop-content {
				margin-top: 10px;

				.commodity {
					width: 60pt;
				}
				
				.sc-right {
					width: 214px;
					
					.scr-title {
						display: -webkit-box;
						-webkit-line-clamp:2;
						overflow: hidden;
						line-height: 20px;
						-webkit-box-orient: vertical;
						text-overflow: ellipsis;
					}
					
					.secondary {
						color: #999;
						padding: 5px;
						margin: 5px 0;
						border-radius: 5px;
						background: rgba(249,249,249,1);
					}
				}
			}
		}
	
		.settlement {
			bottom: 50px;
			left: 0;
			width: 100%;
			height: 45px;
			padding: 0 15px 0 28px;
			position: fixed;
			line-height: 45px;
			background-color: #fff;
			
			button {
				margin-left: 10px;
				vertical-align: middle;
			}

			.clear {
				color: $green;
				font-size: 12px;
				padding: 0 5px;
				margin-left: 24px;
				border-radius: 5px;
				border: 1px solid $green;
			}
		}
	}
</style>
