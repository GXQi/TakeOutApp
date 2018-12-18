<template>
<fade-right>
  <div class="detail" v-show="showFlag" ref="detail">
    <div class="detail-content border-bottom">
      <div class="image-header">
        <img :src="food.image" />
        <div class="back" @click="hide">
          <i class="icon-arrow_lift"></i>
        </div>
      </div>
      <div class="detail-info">
        <h2 class="info-name">{{ food.name }}</h2>
        <div class="info-extra">
          <span>月售{{ food.sellCount }}</span><span>好评率{{ food.rating }}%</span>
        </div>
        <div class="info-price">
          <span>￥</span>
          <span>{{ food.price }}</span>
          <span v-if="food.oldPrice">￥{{ food.oldPrice }}</span>
        </div>
        <div class="add-shoppingcart">
          <span>加入购物车</span>
        </div>
      </div>
      <div class="desc-content border-topbottom">
        <h2 class="desc-name">商品介绍</h2>
        <p class="desc-info">{{ food.info }}</p>
        <p class="desc-info">{{ food.info }}</p>
      </div>
      <div class="rating-content">
        <h2 class="rating-name">商品评价</h2>
      </div>
    </div>
  </div>
</fade-right>
</template>

<script>
import BetterScroll from 'better-scroll'
import FadeRight from '@/common/fade/FadeRight'
export default {
  name: 'Detail',
  data () {
    return {
      showFlag: false
    }
  },
  components: {
    FadeRight
  },
  props: {
    food: {
      type: Object
    }
  },
  methods: {
    show () {
      this.showFlag = true
      this.$nextTick(() => {
        if (!this.scroll) {
          this.scroll = new BetterScroll(this.$refs.detail, {
            click: true,
            bounce: false
          })
          console.log(this.scroll)
        } else {
          this.scroll.refresh()
        }
      })
    },
    hide () {
      this.showFlag = false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
  .border-bottom
    &:before
      border-color: rgba(7, 17, 27, .1)
  .border-topbottom
    &:before
      border-color: rgba(7, 17, 27, .1)
  .detail
    position: fixed
    left: 0
    top: 0
    bottom: .96rem
    z-index: 30
    width: 100%
    .detail-content
      background: #F3F5F7
      overflow: hidden
      .image-header
        position: relative
        width: 100%
        height: 0
        padding-bottom: 100%
        img
          position: absolute
          top: 0
          left: 0
          height: 100%
        .back
          position: absolute
          top: .2rem
          left: 0
          .icon-arrow_lift
            display: block
            padding: .20rem
            font-size: .32rem
            color: #FFF
      .detail-info
        position: relative
        font-size: 0
        padding: .36rem
        background: #FFF
        .info-name
          line-height: .28rem
          font-size: .28rem
          font-weight: 700
          color: rgb(7, 17, 27)
        .info-extra
          margin-top: .16rem
          font-size: .2rem
          line-height: .2rem
          color: rgb(147, 153, 159)
          span
            &:first-child
              padding-right: .24rem
        .info-price
          margin-top: .36rem
          font-size: 0
          span
            font-size: .28rem
            font-weight: 700
            color: rgb(240, 20, 20)
            &:first-child
              font-size: .2rem
              font-weight: normal
            &:nth-child(2)
              padding-right: .16rem
            &:nth-child(3)
              text-decoration: line-through
              font-size: .2rem
              color: rgb(147, 153, 159)
        .add-shoppingcart
          position: absolute
          bottom: .24rem
          right: .36rem
          width: 1.48rem
          height: .48rem
          padding-top: .12rem
          font-size: .2rem
          line-height: .24rem
          background: rgb(0, 160, 220)
          box-sizing: border-box
          text-align: center
          border-radius: .24rem
          color: rgb(255, 255, 255)
      .desc-content
        padding: .36rem
        margin-top: .32rem
        background: #FFF
        .desc-name
          font-size: .28rem
          padding-bottom: .12rem
        .desc-info
          font-size: .24rem
          line-height: .48rem
          padding: 0 .16rem
          font-weight: 200
          color: rgb(77, 85, 93)
      .rating-content
        padding: .36rem
        margin-top: .32rem
        background: #FFF
        .rating-name
          font-size: .28rem
          padding-bottom: .12rem
</style>
