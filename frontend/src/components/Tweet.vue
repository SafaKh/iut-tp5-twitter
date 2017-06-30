<template>
  <div class="tweet">
    <div >
     <strong>{{ tweet.auteur.nom}} {{ tweet.auteur.prenom}}</strong> <span class="handle">@{{ tweet.auteur.handle}} -{{moment(tweet.date).fromNow()}}</span>
    </div>
    <div>
      {{ tweet.contenu }}
    </div>
    <div>
      <ul ><li class="button"><icon name="reply"/></li>
      <li class="button"><a @click="retweet()"> <icon name="retweet"/>{{ nbretweet() }}</a></li>
      <li class="button"><icon name="heart"/></li>
      <li class="button"><icon name="envelope"/></li></ul>
    </div>
   </div>
</template>

<script>
import 'vue-awesome/icons'
import moment from 'moment'
import Icon from 'vue-awesome/components/Icon'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)
export default {
  name: 'tweet',
  components: {Icon},
  props: ['tweet'],
  methods: {
    moment: function (date) {
      return moment(date)
    },
    nbretweet: function () {
      return this.tweet.retweeters.length
    },
    retweet: function () {
      this.$http.get('http://localhost:8080/retweet', {params: {utilisateur: 'johndoe', tweet: this.tweet.id}, responseType: 'text'}).then(response => {
        this.tweets = response.body
        this.$emit('retweeted', this.tweet.id)
      }, response => {
        console.log('error')
      })
    }
  },
  created () {
    moment.locale('fr')
  }
}
</script>
<style scoped>
li.button {
 display: inline-block;
}
ul {
  list-style-type: none;
  padding: 0;
}

a {
 color: #42b983;
}

span.handle {
 color: gray;
}
</style>
