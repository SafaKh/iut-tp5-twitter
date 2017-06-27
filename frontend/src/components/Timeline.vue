<template>
  <div class="timeline">
      <feed :tweets="tweets" :loading="loading"/></li>
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

