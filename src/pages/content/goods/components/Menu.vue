<template>
  <div class="menu" ref="wrapper">
    <ul class="menu-ul">
      <li v-for="(item, index) of goods"
        :key="index" class="menu-item"
        :class="{'current':currentIndex===index}"
        @click="selectMenu(index, $event)"
      >
        <span class="text border-bottom">
          <span v-show="item.type > 0" class="minus" :class="minusClass[item.type]"></span>{{ item.name }}
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
import BetterScroll from 'better-scroll'
export default {
  name: 'GoodsMenu',
  props: {
    goods: {
      Object,
      required: true
    },
    scrollY: {
      Number
    },
    listheight: {
      Array
    }
  },
  data () {
    return {
      minusClass: ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    }
  },
  methods: {
    selectMenu (index, event) {
      this.$emit('menuindex', index)
    }
  },
  computed: {
    currentIndex () {
      for (let i = 0; i < this.listheight.length; i++) {
        let height1 = this.listheight[i]
        let height2 = this.listheight[i + 1]
        if (!height2 || (this.scrollY >= height1 && this.scrollY < height2)) {
          return i
        }
      }
      return 0
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
      border-color: rgba(7, 17, 27, .1)
  .menu
    flex: 0 0 1.6rem
    width: 1.6rem
    background: #F3F5F7
    .menu-ul
      .menu-item
        display: table
        height: 1.08rem
        width: 1.12rem
        padding: 0 .24rem
        line-height: .28rem
        &.current
          background: #FFF
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
