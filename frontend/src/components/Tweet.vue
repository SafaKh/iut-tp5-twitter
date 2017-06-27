<template>
  <div class="tweet">
    <div >
     {{ tweet.auteur.nom}} {{ tweet.auteur.prenom}} @{{ tweet.auteur.handle}}
    </div>
    <div>
      {{ tweet.contenu }}
    </div>
   </div>
</template>

<script>
export default {
  name: 'tweet',
  props: ['tweet']
}
</script>
