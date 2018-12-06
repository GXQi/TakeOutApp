<template>
  <div class="menu">
    <ul class="menu-ul">
      <li v-for="(item, index) of goods" :key="index" class="menu-item border-bottom">
        <span class="text">
          <span v-show="item.type > 0" class="minus" :class="minusClass[item.type]"></span>{{ item.name }}
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'GoodsMenu',
  props: {
    goods: {
      Object,
      required: true
    }
  },
  data () {
    return {
      minusClass: ['decrease', 'discount', 'special', 'invoice', 'guarantee']
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
      border-color: rgba(7, 17, 27, .1)
  .menu
    flex: 0 0 1.6rem
    width: 1.6rem
    background: #F3F5F7
    .menu-ul
      padding: 0 .24rem
      .menu-item
        display: table
        height: 1.08rem
        width: 1.12rem
        line-height: .28rem
        .text
          display: table-cell
          width: 1.12rem
          vertical-align: middle
          font-size: .24rem
          line-height: .28rem
          .minus
            display: inline-block
            width: .24rem
            height: .24rem
            margin-right: .04rem
            vertical-align: top
            background-size: .24rem .24rem
            background-repeat: no-repeat
            &.decrease
              bgImg('decrease_3')
            &.discount
              bgImg('discount_3')
            &.guarantee
              bgImg('guarantee_3')
            &.invoice
              bgImg('invoice_3')
            &.special
              bgImg('special_3')
</style>
