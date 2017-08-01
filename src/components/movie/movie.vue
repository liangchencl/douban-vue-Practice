<template>
  <div class="content-wrapper">
    <!--优化后，通过改变传入的url改变后台接口就能同一组件重用-->
    <movieItem :Title='Title[0]' :url='url+"in_theaters"' :Fenlei="fenlei[0]"></movieItem>
    <movieItem :Title='Title[1]' :url='url+"top250"' :Fenlei="fenlei[1]"></movieItem>
    <movieItem :Title='Title[2]' :url='url+"coming_soon"' :Fenlei="fenlei[2]"></movieItem>
    <navtype></navtype>
    <download></download>
  </div>
</template>

<script type="text/ecmascript-6">
  import movieItem from './movieItem'

  import navtype from '../common/navtype/navtype.vue'
  import download from '../common/download/download'
  export default {
    name: 'movie',
    data() {
      return {
        url: 'https://api.douban.com/v2/movie/',
        Title: ['影院热映', 'TOP250', '即将上映'],
        fenlei: ['in_theaters', 'top250', 'coming_soon']
      }
    },
    components: {
      movieItem,
      navtype,
      download
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">

</style>
