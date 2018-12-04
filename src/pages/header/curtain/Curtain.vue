<template>
  <div class="curtain">
    <div class="curtain-wrapper clearfix">
      <div class="curtain-content">
        <div class="curtain-header">
          <div class="curtain-title">{{ seller.name }}</div>
          <div class="curtain-star"></div>
        </div>
        <div class="curtain-discount" v-if="seller.supports">
          <div class="curtain-discountTitle">优惠信息</div>
          <div class="curtain-discountInfo">
            <ul>
              <li v-for="(item, index) in seller.supports" :key="index">
                <span class="minus"></span>
                <span class="text">{{ item.description }}</span>
              </li>
            </ul>
          </div>
        </div>
        <div class="curtain-notice" v-if="seller.bulletin">
          <div class="curtain-noticeTitle">商家公告</div>
          <div class="curtain-noticeInfo">{{ seller.bulletin }}</div>
          <div class="curtain-noticeInfo">{{ seller.bulletin }}</div>
          <div class="curtain-noticeInfo">{{ seller.bulletin }}</div>
          <div class="curtain-noticeInfo">{{ seller.bulletin }}</div>
          <div class="curtain-noticeInfo">{{ seller.bulletin }}</div>
          <div class="curtain-noticeInfo">{{ seller.bulletin }}</div>
          <div class="curtain-noticeInfo">{{ seller.bulletin }}</div>
          <div class="curtain-noticeInfo">{{ seller.bulletin }}</div>
        </div>
      </div>
    </div>
    <div class="curtain-close" @click="handleCurtainClick">
      <i class="icon-close"></i>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Curtain',
  props: {
    seller: Object
  },
  methods: {
    handleCurtainClick () {
      this.$emit('close')
    }
  },
  created () {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
@import '~@/common/stylus/base.styl'
  .curtain
    overflow: auto
    position: fixed
    z-index: 100
    top: 0
    left: 0
    width: 100%
    height: 100%
    background: rgba(7, 17, 27, .8)
    .curtain-wrapper
      min-height: 100%
      .curtain-content
        margin-top: 1.28rem
        margin-left: .72rem
        margin-right: .72rem
        padding-bottom: 1.28rem
    .curtain-close
      position: relative
      width: .64rem
      height: .64rem
      margin: -1.28rem auto 0 auto
      margin-top: -1.28rem
      font-size: .64rem
      clear: both
</style>
