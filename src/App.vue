<template>
  <div id="app">
    <header>
      <h1>
        <span class="number">10</span> questions de culture générale
      </h1>
    </header>
    <div class="container">
      <div>
        <Questions
          v-for="(item, index) in items"
          :key="index"
          :post="item"
          v-on:addSolution="onAddSolution"
        />
      </div>
      <div class="container__app-reponses">
        <Reponses :post="solutions" class="app-reponses" />
      </div>
    </div>
    <div class="progress" :style="{ width: progress + '%'}"></div>
  </div>
</template>

<script>
import Questions from "./components/Questions.vue";
import Reponses from "./components/Reponses.vue";

export default {
  name: "app",
  components: {
    Questions,
    Reponses
  },
  data() {
    return {
      items: [
        {
          question: "Quelle est la couleur du cheval blanc d'henri iv ?",
          reponses: ["Bleu", "Blanche", "Noir"],
          solution: "Blanche"
        },
        {
          question: "Combien de dieu trône a l’Olympe ?",
          reponses: ["8", "10", "12"],
          solution: "12"
        },
        {
          question: "Quelle est la voiture dans Retour vers le futur ?",
          reponses: ["Doloréanne", "Jacquette", "Annette"],
          solution: "Doloréanne"
        },
        {
          question: "Qui a écrit les misérables ?",
          reponses: ["Victor Hugo", "Albert Camus", "Voltaire"],
          solution: "Victor Hugo"
        },
        {
          question: "Quel est le symbole chimique de l’azote ?",
          reponses: ["Y", "B", "N"],
          solution: "N"
        },
        {
          question: "Quel est le 2ème nom de l’hippocampe ?",
          reponses: ["Le cheval de mer", "La truie", "Le dromadaire de mer"],
          solution: "Le cheval de mer"
        },
        {
          question: "En quelle année fut posé le premier pas sur la lune ?",
          reponses: ["1955", "1969", "1985"],
          solution: "1969"
        },
        {
          question: "Qui est le patron des totally spies ?",
          reponses: ["Popeye", "Freddy", "Jerry"],
          solution: "Jerry"
        },
        {
          question:
            "Quelle pièce est absolument à protéger dans un jeu d’échec ?",
          reponses: ["Le roi", "La dame", "Le pion"],
          solution: "Le roi"
        },
        {
          question: "Combien il y a-t-il de joueurs dans un onze au foot ?",
          reponses: ["42", "69", "11"],
          solution: "11"
        }
      ],
      solutions: [],
      progress: 0,
      stageProgressBar: 0,
      include: false
    };
  },
  created() {
    this.stageProgressBar = 100 / this.items.length;
    this.items.forEach(element => {
      this.solutions.push({
        question: element.question,
        reponse: "",
        solution: element.solution
      });
    });
  },
  methods: {
    onAddSolution(value) {
      this.solutions.forEach(element => {
        if (element.question == value.question) {
          if (element.reponses != value.reponse) {
            this.solutions[this.solutions.indexOf(element)].reponse =
              value.reponse;
          }
          this.include = true;
        }
      });
      if (!this.include) {
        this.solutions.push(value);
        this.progress += this.stageProgressBar;
      }
      this.include = false;
    }
  }
};
</script>

<!-- Add "lang='scss'" attribute to use SCSS to this component only -->
<style lang="scss">
#app {
  font-family: "Roboto", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
header {
  text-align: center;
  margin-bottom: 2rem;
  text-transform: uppercase;
  font-weight: 700;
}
h1 {
  letter-spacing: 0.05rem;
}
.number {
  color: rgb(20, 137, 221);
}
.container {
  display: flex;
  height: 100%;
  width: 80vw;
  margin: auto;

  &__app-reponses {
    position: fixed;
    right: 7.5vw;
    top: 50%;
    margin-top: -350px;
  }
}
.progress {
  position: fixed;
  width: 0%;
  height: 5px;
  top: 0;
  background-color: orange;
  transition: width 0.5s ease-out;
}

@media screen and (max-width: 1800px) {
  .container__app-reponses {
    display: none;
  }
}
@media screen and (max-width: 1024px) {
  .container {
    width: 90vw;
    text-align: center;

    div {
      margin: auto;
    }
  }
}
</style>
