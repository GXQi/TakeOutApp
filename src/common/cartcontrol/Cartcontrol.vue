<template>
  <div class="cartcontrol">
    <fade-scroll>
      <div
        class="cart-decrease icon-remove_circle_outline"
        v-show="food.count"
        @click="decreaseCart"
      ></div>
    </fade-scroll>
    <div class="cart-count" v-show="food.count">{{ food.count }}</div>
    <div class="cart-add icon-add_circle" @click="addCart"></div>
  </div>
</template>

<script>
import FadeScroll from '../fade/FadeScroll'
export default {
  name: 'Cartcontrol',
  props: {
    food: {
      type: Object
    }
  },
  components: {
    FadeScroll
  },
  methods: {
    addCart () {
      if (!this.food.count) {
        this.food.count = 1
      } else {
        this.food.count++
      }
    },
    decreaseCart () {
      if (!this.food.count) {
        this.food.count = 0
      } else {
        this.food.count--
      }
    }
  },
  watch: {
    food () {
      console.log()
    }
  },
  created () {
    this.$set(this.food, 'count', 0)
  }
}
</script>

<style scoped lang="stylus">
  .cartcontrol
    .cart-decrease, .cart-add
      display: inline-block
      padding: .12rem
      font-size: .48rem
      line-height: .48rem
      color: rgb(0, 160, 220)
    .cart-count
      display: inline-block
      vertical-align: top
      width: .24rem
      padding-top: .12rem
      font-size: .20rem
      line-height: .48rem
      text-align: center
      color: rgb(147, 153, 159)
</style>
