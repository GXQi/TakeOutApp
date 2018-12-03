<template>
  <div class="tab">
    <router-link to="/goods" class="tab-item border-bottom">
      <div>商品</div>
    </router-link>
    <router-link to="/ratings" class="tab-item border-bottom">
      <div>评论</div>
    </router-link>
    <router-link to="/seller" class="tab-item border-bottom">
      <div>商家</div>
    </router-link>
  </div>
</template>

<script>
export default {
  name: 'Tab'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
  .border-bottom
    &:before
      border-color: rgba(7, 17, 27, .1)
  .tab
    display: flex
    width: 100%
    height: .8rem
    line-height: .8rem
    font-size: .28rem
    .tab-item
      flex: 1
      text-align: center
      color: rgb(77, 85, 93)
    .router-link-active
      color: rgb(240, 20, 20)
</style>
