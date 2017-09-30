<template>
	<div ref="wrapper">
		<slot></slot>
	</div>
</template>

<script type="text/ecmascript-6">
	import BSscroll from 'better-scroll'

	export default {
		props:{
			probeType:{
				type:Number,
				default:1
			},
			click:{
				type:Boolean,
				default:true
			},
			listenScroll:{
				type:Boolean,
				default:false
			},
			//初始化data  解决有可能数据变动以后页面滑动不了的情况
			data:{
				type:Array,
				default:null
			},
      refreshDelay : {
			  type:Number,
        default:20
      }
		},
		mounted(){
			setTimeout(()=>{
				this._initScroll();
			},20)
		},
		methods:{
			_initScroll () {
				if(!this.$refs.wrapper){
					return;
				}
				this.scroll = new BSscroll(this.$refs.wrapper,{
					probeType:this.probeType,
					click:this.click
				})
			},
			enable () {
				this.scroll && this.scroll.enable();
			},
			disable () {
				this.scroll && this.scroll.disable();
			},
			refresh () {
				this.scroll && this.scroll.refresh();
			}


		},
		watch:{
			data () {
				setTimeout(() => {
					this.refresh();
				},this.refresh)
			}
		}
	}
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">

</style>
