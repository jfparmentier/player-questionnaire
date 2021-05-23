<template>
  <div :class="[!selectable && correct ? 'bouton-vert' : (!selectable && selectedByUser ? 'bouton-orange' : 'bouton-reponse'), 'u-full-width']"
       @click="clickReponse"
       :style="{cursor: selectable ? 'pointer' : 'not-allowed' }"
       v-html="reponse">
  </div>
</template>

<script>
export default {
  name: "boutonReponse",
  props: {
    reponse: String,
    correct: Boolean,
    selectable: Boolean,
    selectedByUser: Boolean
  },
  methods: {
    clickReponse: function () {
      if(this.selectable) {
        this.$emit('reponse-cliquee');
      }
    }
  },
  emits : ['reponse-cliquee']
}
</script>

<style scoped>

</style>