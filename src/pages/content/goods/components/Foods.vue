<template>
  <div class="foods" ref="wrapper">
    <ul>
      <li v-for="(titleItem, index) of goods" :key="index" class="food-item food-item-hook">
        <h1 class="food-title">{{ titleItem.name }}</h1>
        <ul class="food-ul">
          <li
            v-for="(foodItem, index) of titleItem.foods"
            :key="index"
            class="foodList-item border-bottom"
            @click="selectFood(foodItem)"
          >
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
              <div class="cartcontrol-wrapper">
                <cart-control :food="foodItem"></cart-control>
              </div>
            </div>
          </li>
        </ul>
      </li>
    </ul>
    <food-detail
      :food="selectedFood"
      ref="food"
    ></food-detail>
  </div>
</template>

<script>
import BetterScroll from 'better-scroll'
import CartControl from '@/common/cartcontrol/Cartcontrol'
import FoodDetail from 'content/detail/Detail'
export default {
  name: 'GoodsFoods',
  data () {
    return {
      listHeight: [],
      scrollY: 0,
      currentIndex: 0,
      selectedFood: {}
    }
  },
  props: {
    goods: {
      Object
    },
    menuindex: {
      Number
    }
  },
  components: {
    CartControl,
    FoodDetail
  },
  methods: {
    calculateHeight () {
      let foodList = this.$refs.wrapper.getElementsByClassName('food-item-hook')
      let height = 0
      this.listHeight.push(height)
      for (let i = 0; i < foodList.length; i++) {
        let item = foodList[i]
        height += item.clientHeight
        this.listHeight.push(height)
      }
      this.$emit('listheight', [0, 1033, 1185, 1306, 1617, 1833, 2068, 2379, 2880, 3571])
    },
    selectFood (food) {
      this.selectedFood = food
      this.$refs.food.show()
    }
  },
  computed: {
    selectFoods () {
      let foods = []
      this.goods.forEach((good) => {
        console.log(good)
        good.foods.forEach((food) => {
          if (food.count) {
            foods.push(food)
          }
        })
      })
      this.$emit('foodsarray', foods)
      return foods
    }
  },
  watch: {
    menuindex () {
      let foodList = this.$refs.wrapper.getElementsByClassName('food-item-hook')
      let el = foodList[this.menuindex]
      this.scroll.scrollToElement(el, 500)
    },
    scrollY () {
      this.$emit('indexchange', this.scrollY)
    },
    goods () {
      let foods = []
      this.goods.forEach((good) => {
        console.log(good)
        good.foods.forEach((food) => {
          if (food.count) {
            foods.push(food)
          }
        })
      })
      this.$emit('select-foods', this.goods)
    }
  },
  mounted () {
    this.scroll = new BetterScroll(this.$refs.wrapper, {
      click: true,
      probeType: 3
    })
    this.scroll.on('scroll', (pos) => {
      this.scrollY = Math.abs(Math.round(pos.y))
    })
    this.calculateHeight()
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
                color: rgb(147, 153, 159)
          .cartcontrol-wrapper
            position: absolute
            right: 0
            bottom: .24rem
            font-size: 0
</style>
