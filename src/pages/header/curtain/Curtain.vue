<template>
  <div class="curtain">
    <div class="curtain-wrapper clearfix">
      <div class="curtain-content">
        <div class="curtain-title">{{ seller.name }}</div>
        <div class="curtain-star">
          <curtain-star :size="48" :score="seller.score"></curtain-star>
        </div>
        <div class="curtain-discount">
          <div class="info-title">
            <div class="title-line border-bottom"></div>
            <div class="curtain-titleMain">优惠信息</div>
            <div class="title-line border-bottom"></div>
          </div>
          <ul class="curtain-discountInfo" v-if="seller.supports">
            <li class="discount-item" v-for="(item, index) in seller.supports" :key="index">
              <span class="minus" :class="minusClass[item.type]"></span>
              <span class="text">{{ item.description }}</span>
            </li>
          </ul>
        </div>
        <div class="curtain-notice">
          <div class="info-title">
            <div class="title-line border-bottom"></div>
            <div class="curtain-titleMain">商家告示</div>
            <div class="title-line border-bottom"></div>
          </div>
          <div class="curtain-noticeInfo">{{ seller.bulletin }}</div>
        </div>
      </div>
    </div>
    <div class="curtain-close" @click="handleCurtainClick">
      <i class="icon-close"></i>
    </div>
  </div>
</template>

<script>
import CurtainStar from '@/common/star/Star'
export default {
  name: 'Curtain',
  components: {
    CurtainStar
  },
  data () {
    return {
      minusClass: ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    }
  },
  props: {
    seller: Object
  },
  methods: {
    handleCurtainClick () {
      this.$emit('close')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
@import '~@/common/stylus/base.styl'
@import '~@/common/stylus/mixin.styl'
  .border-bottom
    &:before
      border-color: rgba(255, 255, 255, .2)
  .info-title
    display: flex
    width: 100%
    margin: .56rem auto .48rem auto
    .title-line
      flex: 1
      position: relative
      top: -.12rem
    .curtain-titleMain
      padding: 0 .24rem
      font-size: .28rem
      font-weight: 700
      line-height: .28rem
  .curtain
    overflow: auto
    position: fixed
    z-index: 100
    top: 0
    left: 0
    width: 100%
    height: 100%
    background: rgba(7, 17, 27, .8)
    .curtain-wrapper
      width: 100%
      min-height: 100%
      .curtain-content
        margin-top: 1.28rem
        margin-left: .72rem
        margin-right: .72rem
        padding-bottom: 1.28rem
        .curtain-title
          text-align: center
          line-height: .32rem
          font-size: .32rem
          font-weight: 700
        .curtain-star
          margin-top: .32rem
          text-align: center
        .curtain-discount
          .curtain-discountInfo
            margin: 0 .24rem
            .discount-item
              margin-bottom: .24rem
              font-size: 0
              &:last-child
                margin-bottom: 0
              .minus
                display: inline-block
                width: .32rem
                height: .32rem
                vertical-align: top
                margin-right: .12rem
                background-size: .32rem .32rem
                background-repeat: no-repeat
                font-size: .2rem
                &.decrease
                  bgImg('decrease_2')
                &.discount
                  bgImg('discount_2')
                &.guarantee
                  bgImg('guarantee_2')
                &.invoice
                  bgImg('invoice_2')
                &.special
                  bgImg('special_2')
              .text
                line-height: .32rem
                font-size: .24rem
        .curtain-notice
          font-size: .24rem
          font-weight: $fontWeight
          line-height: .48rem
          .curtain-noticeInfo
            margin: 0 .24rem
            font-size: .24rem
            font-weight: $fontWeight
            line-height: .48rem
    .curtain-close
      position: relative
      width: .64rem
      height: 1.28rem
      margin: -1.28rem auto 0 auto
      margin-top: -1.28rem
      font-size: .64rem
      clear: both
</style>
