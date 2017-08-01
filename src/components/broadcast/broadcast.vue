<template>
	<section class="commingsoon">
		<div class="content-wrapper">
		  	<div class="moviesui" id="moviesUl" el="moviesUl">
		  		<ul class="items">
		  			<li class="item" v-for="article in articles">
              <router-link :to="'/movie/subject/'+article.subject.id">
  		  				<img :src="article.subject.images.medium" alt="">
  		  				<p>{{article.subject.title}}</p>
              </router-link>
		  			</li>
		  		</ul>
		  	</div>
		</div>
  	<navtype></navtype>
  	<download></download>
	</section>
</template>

<script type="text/ecmascript-6">
  import BScroll from 'better-scroll'
  import navtype from '../common/navtype/navtype.vue'
  import download from '../common/download/download'
  export default {
    name: 'books',
    data() {
      return {
       articles: []
      }
    },
    methods: {
      // 看网上说用 this.$els.moviesUl 但是不知道为什么不行，会报错 然后就用下面的 document.getElementById('moviesUl')
      // 注意这里只是写在了事件里面，并不会执行，只有在下面加载json文件在成功之后调用执行才行
      // _initScroll () {
      //   this.moviesScroll = new BScroll(this.$els.moviesUl, {
      //     scrollX: true,
      //     click: true
      //   })
      //   console.log(this.$els.moviesUl)
      // }
      _initScroll() {
        this.moviesScroll = new BScroll(document.getElementById('moviesUl'), {
          scrollX: true,
          click: true
        })
        console.log(document.getElementById('moviesUl'))
      }
    },
    mounted: function () {
      this.$http.jsonp('https://api.douban.com/v2/movie/us_box', {}, {
        headers: {},
        emulateJSON: true
      }).then(function (response) {
        this.articles = response.data.subjects
        console.log(response.data.subjects)
        this._initScroll()
      })
    },
    components: {
      navtype,
      download
    }
   }
</script>

<style lang="stylus" rel="stylesheet/stylus">
.commingsoon {overflow: hidden;}
.moviesui ul {height: 170px;width:1320px;overflow: hidden;}
.moviesui ul li {float: left;width: 120px;text-align: center;list-style: none;}
.moviesui ul li p {font-size: 12px;margin-top: 5px;}
</style>
