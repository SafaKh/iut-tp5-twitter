<template>
  <div class="timeline">
        <utilisateurs @changed="userChanged"></utilisateurs>
        <feed :tweets="tweets" :loading="loading" :userConnected="handle" @retweeted="retweet"></feed>
   </div>
</template>

<script>
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)
import Feed from './Feed'
import Utilisateurs from './Utilisateurs'
export default {

  name: 'timeline',
  components: {Feed, Utilisateurs},
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
    },
    userChanged: function (handle) {
      this.handle = handle
    }
  },
  data () {
    return {
      tweets: [],
      loading: true,
      handle: ''
    }
  },
  created () {
    this.fetchTweets()
  }
}
</script>

