<template>
  <div class="home">
    <div id="read"></div>
  </div>
</template>

<script>
  import Epub from 'epubjs'
  import { mapGetters } from 'vuex'

  global.ePub = Epub
  export default {
    name: 'home',
    computed: {
      ...mapGetters(['test'])
    },
    mounted () {
      this.$store.dispatch('setTest', 4).then(() => {
        console.log(this.test)
      })
      this.book = new Epub('/yxz.epub')
      this.book.renderTo('read', {
        width: window.innerWidth,
        height: window.innerHeight
      }).display()
    }
  }
</script>
<style lang="scss" scoped>
  @import "@/assets/style/global.scss";

</style>
