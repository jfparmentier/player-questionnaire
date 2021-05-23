<template>
<div>
  <h5 style="text-align:center">Question {{numeroQuestion}} / {{ nombreQuestions }}</h5>
  <question :question="question"
            @choix-utilisateur="reponseChoisie"
            :questionRepondue="questionRepondue"
            :reponseUtilisateur="reponseUtilisateur"/>
  <p v-show="questionRepondue"><strong>Explication :</strong></p>
  <span v-show="questionRepondue" v-html="question.explication"></span>
  <button v-show="questionRepondue"
          @click="reponseSuivante"
          class="button-primary u-full-width"
          v-text="(numeroQuestion < nombreQuestions) ? 'Question suivante' : 'Terminer'">
  </button>
</div>
</template>

<script>
import question from "@/components/question";

export default {
  name: "pageQuestion",
  components: {
    question
  },
  props : {
    question: Object,
    nombreQuestions: Number,
    numeroQuestion: Number
  },
  data: function () {
    return {
      questionRepondue: false,
      reponseUtilisateur: 0
    }
  },
  updated() {
    // MAJ equations
    // MathJax.typeset();
    // revient en haut de la page
    window.scrollTo(0, 0);
  },
  methods: {
    reponseChoisie: function (index) {
      this.questionRepondue = true;
      this.reponseUtilisateur = index;
      if((index + 1) === this.question.bonneReponse) {
        this.$emit('bonne-reponse-choisie');
      }
    },
    reponseSuivante: function() {
      this.$emit('question-suivante');
      this.questionRepondue = false;
    }
  },
  emits: ['question-suivante','bonne-reponse-choisie']
}
</script>

<style scoped>

</style>