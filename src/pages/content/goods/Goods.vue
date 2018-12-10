<template>
  <div class="goods">
    <goods-menu
      :goods="goods"
      :scrollY="scrollY"
      :listheight="listheight"
      @menuindex="getMenuIndex"
    >
    </goods-menu>
    <goods-foods
      :goods="goods"
      @indexchange="handleFoodsChange"
      @listheight="listHeightPara"
      :menuindex="menuindex"
    >
    </goods-foods>
  </div>
</template>

<script>
import GoodsMenu from './components/Menu'
import GoodsFoods from './components/Foods'
export default {
  name: 'Goods',
  components: {
    GoodsMenu,
    GoodsFoods
  },
  props: {
    seller: {
      Object
    }
  },
  data () {
    return {
      goods: [],
      scrollY: 0,
      listheight: [],
      menuindex: 0
    }
  },
  methods: {
    handleFoodsChange (y) {
      this.scrollY = y
    },
    listHeightPara (list) {
      this.listheight = list
    },
    getMenuIndex (index) {
      this.menuindex = index
    }
  },
  created () {
    this.$http.get('/api/goods').then((res) => {
      res = res.body
      if (res.errno === 0) {
        this.goods = res.data
      }
    }, function () {
      console.log('请求失败处理')
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
  .goods
    display: flex
    position: absolute
    top: 3.48rem
    bottom: .92rem
    overflow: hidden
</style>
