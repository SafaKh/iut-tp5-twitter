<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <ul>
      <li><router-link to="/timeline">Timeline</router-link></li>
     </ul>
   </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Bienvenue sur Twitter'
    }
  }
}
</script>
