<template>
  <div>
  Connected User :{{this.handle}}
    <select @change="onChange($event.target.value)">
     <option>Choisissez un utilisateur ...</option>
     <option v-for="utilisateur in utilisateurs" :value="utilisateur.handle">
       {{ utilisateur.prenom }} {{ utilisateur.nom }} - {{utilisateur.handle}}
     </option>
    </select>
  </div>
</template>

<script>
import Vue from 'vue'
import Resource from 'vue-resource'
import moment from 'moment'

Vue.use(Resource)

export default {
  name: 'timeline',
  data () {
    return {
      utilisateurs: [''],
      handle: undefined
    }
  },
  created () {
    this.getUtilisateurs()
  },
  methods: {
    momentf: function (date) {
      return moment(date)
    },
    getUtilisateurs: function () {
      // GET /someUrl
      this.$http.get('http://localhost:8080/utilisateurs').then(response => {
        this.utilisateurs = response.body
      }, response => {
          // error callback
      })
    },
    onChange: function (handle) {
      this.$emit('changed', handle)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
