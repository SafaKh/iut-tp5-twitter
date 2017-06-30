<template>
  <div class="timeline">
        <utilisateurs @changed="userChanged"></utilisateurs>
        <br>
        <PostTweet :connectedUser="handle" @newTweet="postTweet"></PostTweet>
        <br>
        <feed :tweets="sortedTweets" :loading="loading" :userConnected="handle" @retweeted="retweet"></feed>
   </div>
</template>

<script>
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)
import Feed from './Feed'
import PostTweet from './PostTweet'
import Utilisateurs from './Utilisateurs'
export default {

  name: 'timeline',
  components: {Feed, Utilisateurs, PostTweet},
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
    },
    postTweet: async function (newTweet) {
      var data = new FormData()
      data.append('auteur', this.handle)
      data.append('contenu', newTweet)
      var postedTweet = await this.$http.post('http://localhost:8080/tweet', data)
      postedTweet.body.retweeters = []
      postedTweet.body.date = Date.now()
      // unshift() ajoute un ou plusieurs éléments au début d'un tableau et renvoie la nouvelle longueur du tableau
      this.tweets.unshift(postedTweet.body)
    }
  },
  data () {
    return {
      tweets: [],
      loading: true,
      handle: undefined,
      id: undefined
    }
  },
  computed: {
    sortedTweets: function () {
      return this.tweets.sort((a, b) => a.date < b.date)
    }
  },

  created () {
    setTimeout(function () {
      this.fetchTweets()
    }.bind(this), 2000)
  }
}
</script>

