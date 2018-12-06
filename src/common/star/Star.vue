<template>
  <div class="star" :class="starType">
    <span v-for="(item, index) in itemClass" :class="item" class="star-item" :key="index"></span>
  </div>
</template>

<script>
export default {
  name: 'Star',
  props: {
    size: Number,
    score: Number
  },
  computed: {
    starType () {
      return 'star-' + this.size
    },
    itemClass () {
      const LENGTH = 5
      const ON = 'on'
      const HALF = 'half'
      const OFF = 'off'
      const result = []
      let score = Math.floor(this.score * 2) / 2
      let hasDecimal = score % 1 !== 0
      let integer = Math.floor(score)
      for (let i = 0; i < integer; i++) {
        result.push(ON)
      }
      if (hasDecimal) {
        result.push(HALF)
      }
      while (result.length < LENGTH) {
        result.push(OFF)
      }
      return result
    }
  },
  created () {
    console.log(this.score)
  }
}
</script>

<style scoped lang="stylus">
@import '~@/common/stylus/mixin.styl'
  .star
    .star-item
      display: inline-block
      background-repeat: no-repeat
    &.star-48
      .star-item
        width: .4rem
        height: .4rem
        margin-right: .44rem
        background-size: .4rem .4rem
        &:last-child
          margin-right: 0
        &.on
          bgImg('star48_on')
        &.half
          bgImg('star48_half')
        &.off
          bgImg('star48_off')
    &.star-36
      .star-item
        width: .3rem
        height: .3rem
        margin-right: .12rem
        background-size: .3rem .3rem
        &:last-child
          margin-right: 0
        &.on
          bgImg('star36_on')
        &.half
          bgImg('star36_half')
        &.off
          bgImg('star36_off')
    &.star-24
      .star-item
        width: .2rem
        height: .2rem
        margin-right: .03rem
        background-size: .2rem .2rem
        &:last-child
          margin-right: 0
        &.on
          bgImg('star24_on')
        &.half
          bgImg('star24_half')
        &.off
          bgImg('star24_off')
</style>
