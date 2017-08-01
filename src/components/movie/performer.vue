<template>
  <div class="content-wrapper">
    <!--优化后，通过改变传入的url改变后台接口就能同一组件重用-->
    <div class="performer_con">
      <h4>{{performer.name}} <small>({{performer.name_en}})</small></h4>
      <div class="pic">
        <img :src="performer.avatars.medium" alt="">
        <p>性别：{{performer.gender}}</p>
        <p>出生地: {{performer.born_place}}</p>
        <a :href="performer.mobile_url" title="">更多资料</a>
      </div>

      <h4 style="margin-top: 20px;">作品</h4>
      <ul >
        <li v-for="work in performer.works">
          <router-link :to="'/movie/subject/'+work.subject.id" >
            <img :src="work.subject.images.small" alt="">
            <h4>{{work.subject.title}}</h4>
            <p>{{work.subject.title}}</p>
            <p>评分：{{work.subject.rating.average}}</p>
          </router-link>
        </li>
        <li>
          <a href="" title="">查看全部作品</a>
        </li>
      </ul>
    </div>

    <navtype></navtype>3
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
        performer: '',
        id: ''
      }
    },
    mounted: function () {
      this.$http.jsonp('https://api.douban.com/v2/movie/celebrity/' + this.id, {}, {
        headers: {},
        emulateJSON: true
      }).then(function (response) {
        this.performer = response.data
        console.log(this.performer)
      })
    },
    created() {
      this.id = this.$route.params.id
    },
    components: {
      navtype,
      download
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
.performer_con {padding: 0 1.12rem;}
.performer_con h4 {margin: 10px 0;}
.pic {overflow: hidden;}
.pic img {float: left;margin-right: 10px;}
.performer_con ul {padding: 0;}
.performer_con ul li {list-style: none;overflow: hidden;margin-bottom: 10px;background: #EBEBEB;padding: 10px;}
.performer_con ul li img {float: left;margin-right: 10px;}
.performer_con ul li a {text-decoration: none;}
.performer_con ul li h4 {color:#333;}
.performer_con ul li p {margin: 0;line-height: 1.6em;color: #666;}
</style>
