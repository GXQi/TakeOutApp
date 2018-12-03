<template>
  <div id="app">
    <home-header :seller="seller"></home-header>
    <home-tab></home-tab>
    <home-content>
      <router-view/>
    </home-content>
  </div>
</template>

<script>
import Header from '@/pages/header/Header'
import Tab from '@/pages/tab/Tab'
import Content from '@/pages/content/Content'
export default {
  name: 'App',
  data () {
    return {
      goods: {},
      ratings: {},
      seller: {}
    }
  },
  components: {
    'HomeHeader': Header,
    'HomeTab': Tab,
    'HomeContent': Content
  },
  methods: {
    get () {
      this.$http.get('/api/seller').then((res) => {
        res = res.body
        if (res.errno === 0) {
          this.seller = res.data
        }
      }, function () {
        console.log('请求失败处理')
      })
    }
  },
  created () {
    this.get()
  }
}
</script>

<style>
</style>
