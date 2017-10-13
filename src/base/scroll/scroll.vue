<template>
  <div ref="wrapper">
    <slot></slot>
  </div>
</template>

<script type="text/ecmascript-6">
  import BSscroll from 'better-scroll'

  export default {
    props: {
      probeType: {
        type: Number,
        default: 1
      },
      click: {
        type: Boolean,
        default: true
      },
      //要不要监听滚动时间
      listenScroll: {
        type: Boolean,
        default: false
      },
      //初始化data  解决有可能数据变动以后页面滑动不了的情况
      data: {
        type: Array,
        default: null
      },
      refreshDelay: {
        type: Number,
        default: 20
      }
    },
    mounted() {
      setTimeout(() => {
        this._initScroll();
      }, 20)
    },
    methods: {
      _initScroll() {
        if (!this.$refs.wrapper) {
          return;
        }
        this.scroll = new BSscroll(this.$refs.wrapper, {
          probeType: this.probeType,
          click: this.click
        });
        if (this.listenScroll) {
          let that = this;
          this.scroll.on('scroll',(pos)=>{
            that.$emit('scroll',pos);
          })
        }
      },
      enable() {
        this.scroll && this.scroll.enable();
      },
      disable() {
        this.scroll && this.scroll.disable();
      },
      refresh() {
        this.scroll && this.scroll.refresh();
      },
      scrollTo() {
        this.scroll && this.scroll.scrollTo.apply(this.scroll, arguments);
      },
      scrollToElement() {
        this.scroll && this.scroll.scrollToElement.apply(this.scroll, arguments);
      }


    },
    watch: {
      data() {
        setTimeout(() => {
          this.refresh();
        }, this.refreshDelay);
      }
    }
  }
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">

</style>
