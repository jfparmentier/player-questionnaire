<template>
<div style="margin-top: 20%">
  <h2 v-text="(score_pc < 50) ? 'C\'est un bon début.' : ( (score_pc < 100)? 'Bien joué' : 'Bravo !') "></h2>
  <p>Votre score est de <strong>{{score_pc}}%</strong>. Que voulez-vous faire ?</p>
  <button class="button-primary u-full-width" @click="$emit('restart');" >Recommencer</button>
</div>
</template>

<script>
export default {
  name: "pageBilan",
  props : {
    score_pc: Number
  }
}
</script>

<style scoped>

</style>