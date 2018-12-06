<template>
  <div class="header">
    <div class="header-wrapper">
      <div class="header-avatar">
        <img class="header-img" src="./avatar.png">
      </div>
      <div class="header-content">
        <div class="header-title">
          <span class="brand"></span>
          <span class="name">{{ seller.name }}</span>
        </div>
        <div class="header-desc">
          {{ seller.description }}/{{ seller.deliveryTime }}分钟送达
        </div>
        <div class="header-discounts"
              v-if="seller.supports"
        >
          <span class="minus" :class="minusIcon"></span>
          <span class="text">{{ seller.supports[0].description }}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="minus-count"  @click="handleBulletinClick">
        <span class="count">{{ seller.supports.length }}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="handleBulletinClick">
      <span class="bulletin-title"></span><span class="bulletin-text">{{ seller.bulletin }}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="header-background">
      <img src="./avatar.png" width="100%" height="100%" />
    </div>
    <fade-animation>
      <header-curtain v-show="showCurtain" :seller="seller" @close="handleCurtainClose"></header-curtain>
    </fade-animation>
  </div>
</template>

<script>
import HeaderCurtain from './curtain/Curtain'
import FadeAnimation from '@/common/fade/FadeAnimation'
export default {
  name: 'Header',
  data () {
    return {
      showCurtain: false,
      classes: []
    }
  },
  props: {
    seller: Object
  },
  components: {
    HeaderCurtain,
    FadeAnimation
  },
  methods: {
    handleBulletinClick () {
      this.showCurtain = true
    },
    handleCurtainClose () {
      this.showCurtain = false
    }
  },
  computed: {
    minusIcon () {
      return this.classMap[this.seller.supports[0].type]
    }
  },
  created () {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
@import '~@/common/stylus/mixin.styl'
@import '~@/common/stylus/base.styl'
  .header
    position: relative
    overflow: hidden
    color: #FFF
    background: rgba(7, 17, 27, .5)
    .header-wrapper
      position: relative
      padding: .48rem .24rem .36rem .24rem
      font-size: 0
      .header-avatar
        display: inline-block
        vertical-align: top
        .header-img
          width: 1.28rem
          height: 1.28rem
          border-radius: .04rem
      .header-content
        display: inline-block
        padding-left: .32rem
        .header-title
          margin: .04rem 0 .16rem 0
          .brand
            display: inline-block
            width: .6rem
            height: .36rem
            bgImg('brand');
            vertical-align: top
            background-size: .6rem .36rem;
            background-repeat: no-repeat;
          .name
            margin-left: .12rem
            font-size: .32rem
            font-weight: blod
            line-height: .36rem
        .header-desc
          margin-bottom: .2rem
          font-weight: $fontWeight
          font-size: .24rem
          line-height: .24rem
        .header-discounts
          .minus
            display: inline-block
            width: .24rem
            height: .24rem
            margin-right: .08rem
            vertical-align: top
            background-size: .24rem .24rem
            background-repeat: no-repeat
            &.decrease
              bgImg('decrease_1')
            &.discount
              bgImg('discount_1')
            &.guarantee
              bgImg('guarantee_1')
            &.invoice
              bgImg('invoice_1')
            &.special
              bgImg('special_1')
          .text
            font-size: .2rem
            font-weight: $fontWeight
            line-height: .24rem
      .minus-count
        z-index: 2
        position: absolute
        right: .24rem
        bottom: .28rem
        height: .48rem
        padding: 0 .16rem
        background: rgba(0, 0, 0, .2)
        line-height: .48rem
        border-radius: .28rem
        text-align: center
        .count
          font-size: .2rem
          vertical-align: top
        .icon-keyboard_arrow_right
          margin-left: .04rem
          font-size: .2rem
          line-height: .48rem
    .bulletin-wrapper
      position: relative
      height: .56rem
      padding: 0 .44rem 0 .24rem
      line-height: .56rem
      ellipsis()
      background: rgba(7, 17, 27, .2)
      .bulletin-title
        display: inline-block
        vertical-align: top
        margin-top: .16rem
        width: .44rem
        height: .24rem
        bgImg('bulletin')
        background-size: .44rem .24rem
        background-repeat: no-repeat
      .bulletin-text
        vertical-align: top
        margin: 0 .08rem
        font-size: .2rem
      .icon-keyboard_arrow_right
        position: absolute
        top: .16rem
        right: .24rem
        font-size: .2rem
    .header-background
      position: absolute
      top: 0
      left: 0
      width: 100%
      height: 100%
      filter: blur(.2rem)
      z-index: -1
</style>
