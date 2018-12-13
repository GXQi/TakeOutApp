<template>
  <transition>
    <slot></slot>
  </transition>
</template>

<script>
export default {
  name: 'FadeScroll'
}
</script>

<style scoped lang="stylus">
  .v-enter, .v-leave-to
    opacity: 0
    transform: translate3D(.48rem, 0, 0)
  .v-enter-active, .v-leave-active
    transition: all .4s linear
</style>
