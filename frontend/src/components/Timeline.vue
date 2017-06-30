<template>
  <div class="timeline">
      <feed :tweets="tweets" @retweeted="retweet" :loading="loading"/>
   </div>
</template>

<script>
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)
import Feed from './Feed'
export default {

  name: 'timeline',
  components: {Feed},
  methods: {
    fetchTweets: function () {
      this.$http.get('http://localhost:8080/list').then(response => {
        this.tweets = response.body
        this.loading = false
      }, response => {
        console.log('error')
      })
    },
    retweet: function (id) {
      var tweet = this.tweets.find(e => e.id === id)
      var handle = this.tweets.find(e => e.handle === handle)
      tweet.retweeters.push({handle: handle})
    }
  },
  data () {
    return {
      tweets: [],
      loading: true
    }
  },
  created () {
    this.fetchTweets()
  }
}
</script>

