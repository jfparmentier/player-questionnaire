<template>
  <div>
    <span v-html="question.enonce"></span>
    <div v-for="(reponse, index) in question.reponses" :key="index" >
      <boutonReponse :reponse="reponse"
                     :selectable="!questionRepondue"
                     :correct="(index+1) === question.bonneReponse"
                     :selectedByUser="reponseUtilisateur === index"
                     @reponse-cliquee="$emit('choix-utilisateur', index)"
      />
    </div>
  </div>
</template>

<script>
import boutonReponse from "@/components/boutonReponse";

export default {
  name: "question",
  components: {
    boutonReponse
  },
  props: {
    question: Object,
    questionRepondue: Boolean,
    reponseUtilisateur: Number
  },
  emits : ['choix-utilisateur']
}
</script>

<style scoped>

</style>