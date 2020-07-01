<template>
	<view class="category clearfix">
		<view class="nav fl">
			<template v-for="(item, index) in navList">
				<view @click="changeActive(item)" :class="['nav-item', { active: item.active }]" :key="index">{{ item.text }}</view>
			</template>
		</view>
		<view class="category-content fl">
			<view class="cc-top">
				<text class="division">
					今日优惠
				</text>
				<view class="cc-content">
					<view class="discount-item">
						<image src="../../static/images/index/activity_4.png" mode=""></image>
						<text>广东菜心</text>
						<text class="red">￥8.98</text>
					</view>
					<view class="discount-item">
						<image src="../../static/images/index/activity_4.png" mode=""></image>
						<text>广东菜心</text>
						<text class="red">￥8.98</text>
					</view>
					<view class="discount-item">
						<image src="../../static/images/index/activity_4.png" mode=""></image>
						<text>广东菜心</text>
						<text class="red">￥8.98</text>
					</view>
					<view class="discount-item">
						<image src="../../static/images/index/activity_4.png" mode=""></image>
						<text>广东菜心</text>
						<text class="red">￥8.98</text>
					</view>
					<view class="discount-item">
						<image src="../../static/images/index/activity_4.png" mode=""></image>
						<text>广东菜心</text>
						<text class="red">￥8.98</text>
					</view>
					<view class="discount-item">
						<image src="../../static/images/index/activity_4.png" mode=""></image>
						<text>广东菜心</text>
						<text class="red">￥8.98</text>
					</view>
				</view>
			</view>
			<view class="content-list">
				<!-- <view class="cl-item">
					<image src="../../assets/images/index/activity_4.png" mode=""></image>
					
				</view> -->
				<scroll-view :scroll-top="scrollTop" scroll-y="true" class="scroll-Y" @scrolltoupper="upper" @scrolltolower="lower"
				                @scroll="scroll">
					<view class="scroll-view-item uni-bg-red cl-item clearfix">
						<image class="cli-left" src="../../static/images/index/activity_4.png" mode=""></image>
						<view class="cli-right">
							<text>青脆李 约500g/份</text>
							<text class="secondary">清脆爽口、汁多肉厚、香甜美味</text>
							<view class="label">
								<text>今日优惠</text>
								<text>62袋</text>
							</view>
							<view class="unit-price">
								<text class="red">￥8.98</text>
								<text> / 份</text>
							</view>
						</view>
					</view>
					<view class="scroll-view-item uni-bg-red cl-item clearfix">
						<image class="cli-left" src="../../static/images/index/activity_4.png" mode=""></image>
						<view class="cli-right">
							<text>青脆李 约500g/份</text>
							<text class="secondary">清脆爽口、汁多肉厚、香甜美味</text>
							<view class="label">
								<text>今日优惠</text>
								<text>62袋</text>
							</view>
							<view class="unit-price">
								<text class="red">￥8.98</text>
								<text> / 份</text>
							</view>
						</view>
					</view>
					<view class="scroll-view-item uni-bg-red cl-item clearfix">
						<image class="cli-left" src="../../static/images/index/activity_4.png" mode=""></image>
						<view class="cli-right">
							<text>青脆李 约500g/份</text>
							<text class="secondary">清脆爽口、汁多肉厚、香甜美味</text>
							<view class="label">
								<text>今日优惠</text>
								<text>62袋</text>
							</view>
							<view class="unit-price">
								<text class="red">￥8.98</text>
								<text> / 份</text>
							</view>
						</view>
					</view>
					<view class="scroll-view-item uni-bg-red cl-item clearfix">
						<image class="cli-left" src="../../static/images/index/activity_4.png" mode=""></image>
						<view class="cli-right">
							<text>青脆李 约500g/份</text>
							<text class="secondary">清脆爽口、汁多肉厚、香甜美味</text>
							<view class="label">
								<text>今日优惠</text>
								<text>62袋</text>
							</view>
							<view class="unit-price">
								<text class="red">￥8.98</text>
								<text> / 份</text>
							</view>
						</view>
					</view>
				</scroll-view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				 scrollTop: 0,
				navList: [
					{
						text: '超值精选',
						active: true
					},
					{
						text: '田园素菜',
						active: false
					},
					{
						text: '禽畜肉类',
						active: false
					},
					{
						text: '水产海产',
						active: false
					}
				]
			}
		},
		methods: {
			upper: function(e) {
				console.log(e)
			},
			lower: function(e) {
				console.log(e)
			},
			scroll: function(e) {
				console.log(e)
				// this.old.scrollTop = e.detail.scrollTop
			},
			changeActive(obj) {
				this.navList.forEach((item) => {
					if (item.text === obj.text) {
						item.active = true
					} else {
						item.active = false
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	* {
		box-sizing: border-box;
	}
	
	.fl {
		float: left;
	}
	
	.fr {
		float: right;
	}
	
	.violet {
		color: #7397ff;
	}
	
	.orange {
		color: #ffcb5e;
	}
	
	.mt5 {
		margin-top: 5px !important;
	}
	
	.clearfix {
		&::after {
			content: "";
			display: block;
			height: 0;
			line-height: 0;
			visibility: hidden;
			clear: both;
		}
	}
	
	.red {
		color: #ff766b !important;
	}
	
	.secondary {
		color: #979797;
	}
	
	text {
		display: block;
	}
	
	.category {
		font-size: 14px;
		background-color: #f9faf9;
		

		.nav {
			width: 25%;
			height: 100%;
			background-color: #fff;
			
			.nav-item {
				padding: 14px;
				font-size: 12px;
				
				&.active {
					color: #fdd25e;
					background-color: #f9faf9;
				}
			}
		}

		.category-content {
			width: 75%;

			.cc-top {
				text-align: center;

				.division {
					font-size: 14px;
					position: relative;
					display: inline-block;
					
					&::before{
						top: 50%;
						left: -5px;
						content: "";
						width: 50px;
						height: 1px;
						display: block;
						position: absolute;
						background-color: #ff7160;
						transform: translate(-100%, -50%);
					}
					
					&::after {
						top: 50%;
						right: -5px;
						content: "";
						width: 50px;
						height: 1px;
						display: block;
						position: absolute;
						background-color: #ff7160;
						transform: translate(100%, -50%);
					}
				}
			
				.cc-content {
					.discount-item {
						width: 30%;
						float: left;
						
						image {
							width: 100%;
							height: 46px;
						}
					}
				}
			}
		
			.content-list {
				.cl-item {
					border-bottom: 1px solid #eee;
					
					.cli-left {
						float: left;
						width: 120px;
						height: 80px;
					}
					
					.cli-right {
						.label {
							text {
								font-size: 12px;
								padding: 2px;
								border: 1px solid #ff766b;
								border-radius: 5px;
								display: inline-block;
							}
						}
						
						.unit-price {
							text {
								font-size: 12px;
								display: inline-block;
							}
						}
					}
				}
			}
		}
	}
</style>
