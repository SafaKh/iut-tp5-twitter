<template>
  <div class="timeline">
    <ul >
      <li v-for="tweet in tweets"><tweet :tweet="tweet"/></li>
    </ul>
   </div>
</template>

<script>
var tweet1 = {auteur: 'Safa', contenu: 'Salut'}
var tweet2 = {auteur: 'test2', contenu: 'Salut'}
var tweet3 = {auteur: 'test3', contenu: 'Salut'}
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)
import Tweet from './Tweet'
export default {

  name: 'timeline',
  components: {Tweet},
  methods: {
    fetchTweets: function () {
      this.$http.get('http://localhost:8080/list').then(response => {
        this.tweets = response.body
      }, response => {
        console.log('error')
      })
    }
  },
  data () {
    return {
      tweets: [tweet1, tweet2, tweet3]
    }
  },
  created () {
    this.fetchTweets()
  }
}
</script>
<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: block;
  margin: 0 10px;
}
</style>
