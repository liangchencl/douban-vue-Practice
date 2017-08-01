<template>
  <div class="content-wrapper">
    <!--优化后，通过改变传入的url改变后台接口就能同一组件重用-->
    <ul class="movie_more">
      <li class="item" v-for="(movie, movieindex) in movies">
          <router-link :to="'/movie/subject/'+movie.id">
            <a href="javascript:;">
              <div class="item-img"><img :src="movie.images.medium" style="width: 100px; height: 148px" alt=""></div>
              <span class="item-title">{{movie.title}}</span>
              <div class="rating">
                <span class="rating-average">评分：{{movie.rating.average}}</span>
              </div>
            </a>
          </router-link>
        </li>
    </ul>
    <navtype></navtype>
    <download></download>
  </div>
</template>

<script type="text/ecmascript-6">
  import navtype from '../common/navtype/navtype.vue'
  import download from '../common/download/download'
  export default {
    name: 'movie',
    data() {
      return {
        movies: ''
      }
    },
    mounted: function () {
      this.$http.jsonp('https://api.douban.com/v2/movie/' + this.$route.query.id, {}, {
        headers: {},
        emulateJSON: true
      }).then(function (response) {
        // this.articles = response.data.subjects
        this.movies = response.data.subjects
        console.log(this.movies)
      })
    },
    components: {
      navtype,
      download
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
ul.movie_more {overflow: hidden;margin-bottom: 20px;}
ul.movie_more li {float: left;width: 33.33%;text-align: center;font-size: 12px;margin-top: 15px;}
ul.movie_more li img {margin-bottom: 6px;}
ul.movie_more li .item-title {height:12px;overflow: hidden;display: inline-block;}
ul.movie_more li .rating {margin-top:3px;}
</style>
