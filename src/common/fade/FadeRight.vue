<template>
  <transition>
    <slot></slot>
  </transition>
</template>

<script>
export default {
  name: 'FadeRight'
}
</script>

<style scoped lang="stylus">
  .v-enter, .v-leave-to
    transform: translate3D(100%, 0, 0)
  .v-enter-active, .v-leave-active
    transition: all .4s linear
</style>
