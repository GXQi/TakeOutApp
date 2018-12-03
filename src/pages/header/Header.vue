<template>
  <div class="header">
    <div class="header-wrapper">
      <div class="header-avatar">
        <img class="header-img" :src="seller.avatar">
      </div>
      <div class="header-content">
        <div class="header-title">
          <span class="brand"></span>
          <span class="name">{{ seller.name }}</span>
        </div>
      </div>
      <div class="header-desc">
        {{ seller.description }}/{{ seller.deliveryTime }}分钟送达
      </div>
      <div class="header-discounts"
            v-if="seller.supports"
      >
        {{ seller.supports[0].description }}
      </div>
    </div>
    <div class="header-wrapper">11111111</div>
  </div>
</template>

<script>
export default {
  name: 'Header',
  props: {
    seller: Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
  .header
    color: #FFF
    background: black
    .header-wrapper
      padding: .48rem .24rem .36rem .24rem
      .header-avatar
        display: inline-block
    .header-img
      width: 1.28rem
      height: 1.28rem
      border-radius: .04rem
</style>
