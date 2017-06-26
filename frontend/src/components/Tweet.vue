<template>
  <div>
    <div >
     {{ tweet.auteur }}
    </div>
    <div>
      {{ tweet.contenu }}
    </div>
   </div>
</template>

<script>
export default {
  name: 'tweet',
  props : [tweet]
}
</script>
