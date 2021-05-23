<template>
  <div id="app">
    <div class="container">
      <pageQuestion
          v-show="!questionnaireTermine"
          :question="questionnaire[numeroQuestion-1]"
          :nombreQuestions="nombreQuestions"
          :numeroQuestion="numeroQuestion"
          @question-suivante="questionSuivante"
          @bonne-reponse-choisie="score = score + 1"
      />
      <pageBilan
          v-show="questionnaireTermine"
          :score_pc="Math.round(score / nombreQuestions * 100)"
          @restart="recommenceQuestionnaire"
      />
    </div>
  </div>
</template>

<script>
import pageQuestion from "@/components/pageQuestion";
import pageBilan from "@/components/pageBilan";

export default {
  name: 'App',
  components: {
    pageQuestion,
    pageBilan
  },
  data: function() {
    return {
      numeroQuestion: 0,
      nombreQuestions: 0,
      questionnaire: [],
      questionnaireTermine: false,
      score: 0
    }
  },
  created() {
    this.questionnaire = [
      {"id":31,"enonce":"<p>Donnez la réponse la plus précise possible.</p><p>La suite $u$ définie pour tout entier $n$ par $u_n = (-1)^n$ est:</p>","explication":"<p>Cette suite est&nbsp;majorée part tout nombre supérieur ou égal à $1$ et&nbsp;minorée par tout nombre inférieur ou égal à $-1$. Elle est donc bornée.</p>","bonneReponse":3,"reponses":["majorée","minorée","bornée","aucun des trois"],"feedbacks":["<p>oui tout à fait mais elle est aussi minorée par tout nombre inférieur ou égal à $-1$</p>","<p>oui tout à fait mais elle est aussi majorée part tout nombre supérieur ou égal à $1$</p>","","<p>On peut commencer par remarquer que $\\forall n\\in\\mathbb{N},~u_n \\leq 1$, autrement dit $u_n$ est au moins majorée...</p>"],"aide":"<p>Je vous proposer de représenter graphiquement les 10 premiers termes de cette suite.</p>"},
      {"id":6,"enonce":"<p>En physique, on relie l'énergie au repose d'une particule, $E$, à sa masse $m$ par une relation de proportionalité</p><p>$$E=\\text{constante}\\times m$$</p><p>Quelle est l'unité de la constante ?</p>","explication":"<p>L'énergie s'exprime en Joule (J) et la masse en kg. Or, la constante s'écrit $\\text{constante}=E/m$, donc son unité est le J/kg ou J.kg$^{-1}$. Il se trouve que cette unité est la même que des m$^2$.s$^{-2}$, c'est-à-dire une vitesse au carré. En effet, on sait que cette constante est le carré de la vitesse de la lumière.</p>","bonneReponse":3,"reponses":["J","J.kg","J.kg$^{-1}$","sans unité","aucune des réponses précédentes n'est correcte"],"feedbacks":["<p>Le Joule (J) est une unité d'énergie.</p>","<p>Attention aux manipulations algébriques quand tu exprimes la constante en fonction de $E$ et de $m$ pour trouver sa dimension.</p>","","<p>Une constante peut avoir une dimension.</p>","<p>Attention si tu penses que l'unité est le carré d'une vitesse, donc m$^2$.s$^{-2}$, cette unité est la même qu'une des unités proposées plus haut.</p>"],"aide":""},
      {"id":23,"enonce":"<p>La loi du déplacement de Wien dit que</p><p>$$\\lambda_{\\text{max}}=\\frac{\\text{constante}}{T}$$&nbsp; </p><p><img src=\"https://jfparmentier.fr/question_pictures/3/3d8c847.png\" class=\"u-max-full-width\"></p><p>Quelle est l'unité de la constante ?</p>","explication":"<p>La constante s'écrit $\\text{constante}=\\lambda\\,T$, donc l'unité dans le système international est le mètre Kelvin, m.K.</p>","bonneReponse":2,"reponses":["m/K","m.K","K/m","Sans dimension."],"feedbacks":["<p>Commence par exprimer la constante en fonction de $\\lambda$ et $T$.</p>","","","<p>Une constante <strong>peut</strong> avoir une dimension.</p>"],"aide":"<p>Écris que l'équation doit être homogène.</p>"},
      {"id":1022,"enonce":"<p>Un moustique s'écrase sur la vitre d'un TGV. Que dire de la force exercée par la vitre sur le moustique, par rapport à la force exercée par le moustique sur la vitre ?</p>","explication":"","bonneReponse":2,"reponses":["la force exercée par la vitre est plus grande","elles sont égales en norme","la force exercée par le moustique est plus grande"],"feedbacks":["","",""],"aide":""},
      {"id":953,"enonce":"<p>Une grandeur $a$ est reliée à une grandeur $b$ par la relation&nbsp;</p><p>$$a(x)=\\int_{0}^{x}b(x)\\text{d}&nbsp;x$$</p><p>où $x$ représente une longueur. Que dire des dimensions de $a$ et $b$?</p>","explication":"","bonneReponse":3,"reponses":["$[a]=[b]$","$[a]=[b]=1$","$[a]=[b]L$","$[a]=[b]L^{-1}$"],"feedbacks":["","","",""],"aide":""},
      {"id":887,"enonce":"<p>On considère la fronde de la figure ci-dessous.</p><p><img src=\"https://jfparmentier.fr/question_pictures/3/31383edc7.png\" class=\"u-max-full-width\"></p><p>Le travail de la tension de la corde est</p>","explication":"<p>Le mouvement de la masse $m$ est circulaire. La tension de la corde est radiale, donc le déplacement est perpendiculaire à la tension, le travail élémentaire est donc nul. Ainsi, le travail est toujours nul, quelque soit l'angle balayé par la masse $m$.</p>","bonneReponse":3,"reponses":["positif","nul sur un tour complet et non nul sur un demi-tour","toujours nul","négatif"],"feedbacks":["","","",""],"aide":""}
    ];
    this.nombreQuestions = this.questionnaire.length;
    this.numeroQuestion = 1;
  },
  methods: {
    questionSuivante: function() {
      this.numeroQuestion = Math.min( this.numeroQuestion + 1, this.nombreQuestions);
      this.questionnaireTermine = (this.nombreQuestions === this.numeroQuestion);
    },
    recommenceQuestionnaire: function() {
      this.numeroQuestion = 1;
      this.questionnaireTermine = false;
      this.score = 0;
    }
  }

}
</script>

<style>
@import "assets/styles/normalize.css";
@import "assets/styles/skeleton.css";
@import "assets/styles/extensionBoutons.css";
@import "assets/styles/boutonsAdele.css";
</style>
