<template>
  <div class="foods" ref="wrapper">
    <ul>
      <li v-for="(titleItem, index) of goods" :key="index" class="food-item">
        <h1 class="food-title">{{ titleItem.name }}</h1>
        <ul class="food-ul">
          <li v-for="(foodItem, index) of titleItem.foods" :key="index" class="foodList-item border-bottom">
            <div class="food-img">
              <img width="57" height="57" :src="foodItem.icon" />
            </div>
            <div class="food-info">
              <h2 class="food-name">{{ foodItem.name }}</h2>
              <p class="food-desc">{{ foodItem.description }}</p>
              <div class="food-extra">
                <span>月售{{ foodItem.sellCount }}</span><span>好评率{{ foodItem.rating }}%</span>
              </div>
              <div class="food-price">
                <span>￥</span>
                <span>{{ foodItem.price }}</span>
                <span v-if="foodItem.oldPrice">￥{{ foodItem.oldPrice }}</span>
              </div>
            </div>
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
import BetterScroll from 'better-scroll'
export default {
  name: 'GoodsFoods',
  props: {
    goods: {
      Object,
      required: true
    }
  },
  mounted () {
    this.scroll = new BetterScroll(this.$refs.wrapper, {
      click: true
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
@import '~@/common/stylus/base.styl'
@import '~@/common/stylus/mixin.styl'
  .border-bottom
    &:before
      border-color: rgba(7, 17, 27, .2)
  .foods
    flex: 1
    .food-item
      .food-title
        height: .52rem
        line-height: .52rem
        padding-left: .28rem
        font-size: .24rem
        color: rgb(147, 153, 159)
        background: #F3F5F7
        border-left: 2px solid #d9dde1
      .food-ul
        padding: 0 .36rem
      .foodList-item
        display: flex
        padding: .36rem 0
        &:last-child
          border-none()
        .food-img
          flex: 0 0 1.14rem
          margin-right: .2rem
        .food-info
          flex: 1
          .food-name
            margin-top: .04rem
            line-height: .28rem
            font-size: .28rem
            color: rgb(7, 17, 27)
          .food-desc, .food-extra
            margin-top: .16rem
            font-size: .2rem
            color: rgb(147, 153, 159)
            line-height: .25rem
          .food-desc
            line-height: .24rem
          .food-extra
            span
              &:first-child
                padding-right: .24rem
          .food-price
            margin-top: .16rem
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
</style>
