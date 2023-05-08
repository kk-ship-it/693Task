<template>
    <div class="wrapper" ref="wrapper">
        <div class="content">
            <slot></slot> <!-- 插槽就是将主页里<sroll>的内容替换过来 -->
        </div>
    </div>
</template>

<script>
// 原生的局部滚动是通过 overflow:hidden+固定的高度实现的
/*

*/ 
/*
  1.npm下载源码,如果官网中没有下载地址,可以去 GitHub 上最新代码分支上的 dist 文件夹中下载
  2.import 引用
  3.使用的时候要在 mounted 中使用,不能在 created 中,因为没有挂载不能使用
*/ 
import BScroll from 'better-scroll'
export default {
  name: 'Scroll',
  props: {
    probeType: {
      type: Number,
      default: 0
    },
    pullUpLoad: {
      type: Boolean,
      default: false
    },
    observeDOM: {
      type: Boolean,
      default: false,
    },
    observeImage: {
      type: Boolean,
      default:false
    },
    data: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
    return {
      scroll: null
    }
  },
  mounted () {
     /*
       1 这个probeType是监测的意思.有4个值,0-不监测;1-延迟监测;2- 手指滚动的过程中实时监测,手机离开就不监测了,3-还要滚动就会监测
       2 click 属性是一个开关,如果在BScroll中使用按钮默认是不会监听的,但是如果设置为 TRUE,会监听BScroll中的按钮
       3 pullUpLoad上拉加载数据的功能,可以在第二个参数里请求更多页数据,
       但是注意,如果数据请求完成,并且新的数据已经显示,需要调用 bscroll.pullingUp(),只有这样程序才明白上次加载已经完成,可以进行下次加载
        */ 
       /*
        1.尽量使用ref 的形式获取元素对象,不要用 document.querySelector('.wrapper'),这样的话在调试的时候,如果遇到重名的会分不清楚
        2.ref 既可以在组件中使用,这样 this.$refs.x就是组件对象
        3.ref 既可以在普通元素中使用,这样 this.$refs.x就是元素对象
        */ 
      // setTimeout(() => { 图片加载完成后再滚动就不用定时器了
        // 1.创建BScroll对象
        this.scroll = new BScroll(this.$refs.wrapper,{
          click: true, /* div等元素想要被点击，必须设置click */
          probeType: this.probeType,
          pullUpLoad: this.pullUpLoad,
          observeDOM: this.observeDOM,
          // 等页面图片加载完之后，刷新content高度
          observeImage: this.observeImage
        })
        // 2.监听滚动的位置
            /*
            on监听事件滚动的类型,现在是记录滚动相关的数据 
            但是默认是不进行监测的,如果想要监测需要在 new bscroll 中写第二个参数 probeType,
          */ 
        if(this.probeType===2 || this.probeType===3){
          this.scroll.on('scroll', position => {
          // console.log(position)
          this.$emit('scroll',position)
        })
        }
      // 3.监听scroll是否滚动到底部
      if(this.pullUpLoad){ // pullUpLoad为true时，到达底部，为false的组件不用监听此事件，提升效率
        this.scroll.on('pullingUp',()=>{
          // console.log('bottom'); 到达底部时才触发函数
          this.$emit('pullingUp')
      })
      }
      // },1000)
  },
  watch: {
    data () {
      setTimeout(this.refresh,30)
    }
  },
  methods: {
    // 回到顶部的方法
    scrollTo(x,y,time=1000){
      this.scroll && this.scroll.scrollTo(x,y,time)
    },
    refresh () {
      console.log('----'); // 检测到刷新的次数
      this.scroll && this.scroll.refresh()
    },
    finishPullUp(){
       // 这个是当结束上拉更新的时候,必须调用当前方法才能执行下次的下拉更新
      this.scroll && this.scroll.finishPullUp()
    },
    getScrollY () {
      // 得到滚动的y轴的位置
      return this.scroll ? this.scroll.y : 0
    }
  }
}
</script>

<style>

</style>
