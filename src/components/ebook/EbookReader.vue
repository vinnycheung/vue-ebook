<template>
  <div class="ebook-reader">
    <div id="read"></div>
  </div>
</template>

<script>
  import {mapGetters} from 'vuex'
  import Epub from 'epubjs'
  global.ePub = Epub
  export default {
    name: 'EbookReader',
    computed: {
      ...mapGetters(['fileName'])
    },
    methods: {
      initEpub () {
        const url = 'http://localhost:8888/epub/' + this.fileName + '.epub'
        console.log(url)
        this.book = new Epub(url)
        this.book.renderTo('read', {
          width: window.innerWidth,
          height: window.innerHeight,
          method: 'default'
        }).display()
      }
    },
    mounted () {
      const fileName = this.$route.params.fileName.split('|').join('/')
      this.$store.dispatch('setFileName', fileName)
        .then(() => {
          this.initEpub()
        })
    }
  }
</script>

<style lang="scss" scoped>
  @import "@/assets/style/global.scss";

</style>
