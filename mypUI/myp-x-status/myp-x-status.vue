<template>
	<view :class="['myp-bg-'+bgType]" :style="xBarStyle"></view>
</template>

<script>
	import windowMixin from '../myp-mixin/windowMixin.js'
	
	export default {
		mixins: [windowMixin],
		props: {
			bgType: {
				type: String,
				default: ''
			},
			boxStyle: {
				type: String,
				default: ''
			}
		},
		computed: {
			xBarStyle() {
				const h = this.mypGetStatusBarHeight()
				return `height: ${h}px;` + this.boxStyle
			}
		}
	}
</script>

<style lang="scss" scoped>
</style>
