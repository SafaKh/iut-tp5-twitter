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
      <li class="button"> <icon name="retweet"/>{{ nbretweet() }}</li>
      <li class="button"><icon name="heart"/></li>
      <li class="button"><icon name="envelope"/></li></ul>
    </div>
   </div>
</template>

<script>
import 'vue-awesome/icons'
import moment from 'moment'
import Icon from 'vue-awesome/components/Icon'
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
