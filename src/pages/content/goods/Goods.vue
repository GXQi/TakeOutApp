<template>
  <div class="goods">
    <goods-menu :goods="goods"></goods-menu>
    <goods-foods></goods-foods>
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
      goods: []
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
    overflow: hidden
</style>
