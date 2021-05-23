<template>
<div>
  <h2>Bravo !</h2>
  <p>Votre score est de <strong>{{score_pc}}%</strong>. Que voulez-vous faire ?</p>
  <button class="button u-full-width" @click="$emit('restart');" >Recommencer</button>
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