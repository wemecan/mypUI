<template>
	<myp-popup-always :show="show" pos="bottom" height="600rpx" @overlayClicked="toCancel">
		<slot name="header">
			<view :class="['myp-picker-header', 'myp-bg-'+headerBgType, 'myp-border-'+headerBorder, 'myp-radius-'+headerRadius]" :style="headerStyle">
				<text :class="['myp-color-'+cancelType, 'myp-size-'+cancelSize]" :style="cancelStyle" @tap="toCancel">{{cancelText}}</text>
				<text :class="['myp-picker-header-title', 'myp-color-'+titleType, 'myp-size-'+titleSize]" :style="titleStyle">{{title}}</text>
				<text :class="['myp-color-'+confirmType, 'myp-size-'+confirmSize]" :style="confirmStyle" @tap="toConfirm">{{confirmText}}</text>
			</view>
		</slot>
		<myp-picker-content :mode="mode" :selections="selections" :labelProps="labelProps" :value="value" :useCurrent="useCurrent" :start="start" :end="end" :includeBefore="includeBefore" :includeAfter="includeAfter" :rangeIndicator="rangeIndicator" :bgType="bgType" :type="type" :size="size" :height="height" :itemHeight="itemHeight" :boxStyle="boxStyle" :itemStyle="itemStyle" :itemTextStyle="itemTextStyle" :indicatorStyle="indicatorStyle" :rangeType="rangeType" :rangeSize="rangeSize" :rangeStyle="rangeStyle" @inited="pickerInited" @change="pickerChanged"></myp-picker-content>
	</myp-popup-always>
</template>

<script>
	export default {
		props: {
			show: {
				type: Boolean,
				default: false
			},
			mode: {
				type: String,
				default: 'date'
			},
			cancelText: {
				type: String,
				default: '取消'
			},
			confirmText: {
				type: String,
				default: '确认'
			},
			title: {
				type: String,
				default: ''
			},
			cancelType: {
				type: String,
				default: 'third'
			},
			cancelSize: {
				type: String,
				default: 'base'
			},
			cancelStyle: {
				type: String,
				default: ''
			},
			confirmType: {
				type: String,
				default: 'primary'
			},
			confirmSize: {
				type: String,
				default: 'base'
			},
			confirmStyle: {
				type: String,
				default: ''
			},
			titleType: {
				type: String,
				default: 'text'
			},
			titleSize: {
				type: String,
				default: 'base'
			},
			titleStyle: {
				type: String,
				default: ''
			},
			headerBorder: {
				type: String,
				default: 'bottom'
			},
			headerRadius: {
				type: String,
				default: 'top-base'
			},
			headerBgType: {
				type: String,
				default: 'inverse'
			},
			headerStyle: {
				type: String,
				default: ''
			},
			// content about
			// value, not index of column
			value: {
				type: Array,
				default: ()=>{
					return [0,0,0,0,0,0,0]
				}
			},
			useCurrent: {
				type: Boolean,
				default: false
			},
			// 表示年份year的开始或者小时hour的开始
			start: {
				type: String,
				default: "1970"
			},
			end: {
				type: String,
				default: new Date().getFullYear() + ''
			},
			// 仅仅只是用在带年份选择的mode上
			includeBefore: {
				type: Boolean,
				default: true
			},
			includeAfter: {
				type: Boolean,
				default: true
			},
			rangeIndicator: {
				type: String,
				default: '-'
			},
			// styles
			bgType: {
				type: String,
				default: 'inverse'
			},
			type: {
				type: String,
				default: 'text'
			},
			size: {
				type: String,
				default: 'base'
			},
			height: {
				type: String,
				default: '500rpx'
			},
			itemHeight: {
				type: String,
				default: '100rpx'
			},
			boxStyle: {
				type: String,
				default: ''
			},
			itemStyle: {
				type: String,
				default: ''
			},
			itemTextStyle: {
				type: String,
				default: ''
			},
			indicatorStyle: {
				type: String,
				default: ''
			},
			rangeType: {
				type: String,
				default: 'text'
			},
			rangeSize: {
				type: String,
				default: 'base'
			},
			rangeStyle: {
				type: String,
				default: ''
			},
			// for s1/s2/s3
			selections: {
				type: Array,
				default: () => {
					return []
				}
			},
			// for s1/s2/s3 to get right prop value
			labelProps: {
				type: Object,
				default: () => {
					return {
						s1: {
							label: 'name',
							value: 'id'
						},
						s2: {
							label: 'name',
							value: 'id',
							// the tag is for to get s2 selections in s1
							tag: "c"
						},
						s3: {
							label: 'name',
							value: 'id',
							// the tag is for to get get s3 in selections in s2
							tag: "a"
						}
					}
				}
			}
		},
		data() {
			return {
				result: null
			}
		},
		methods: {
			toConfirm() {
				this.$emit("confirm", this.result)
			},
			toCancel() {
				this.$emit("cancel")
			},
			pickerInited(val) {
				// console.log(val)
				this.result = JSON.parse(JSON.stringify(val))
			},
			pickerChanged(val) {
				// console.log(val)
				this.result = JSON.parse(JSON.stringify(val))
			}
		}
	}
</script>

<style lang="scss" scoped>
	.myp-picker {
		&-header {
			flex-direction: row;
			align-items: center;
			justify-content: center;
			height: 100rpx;
			width: 750rpx;
			padding-left: 32rpx;
			padding-right: 32rpx;
			
			&-title {
				flex: 1;
			}
		}
	}
</style>
