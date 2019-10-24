<template>
  <div class="bloc">
    <div class="carre carre__1"></div>
    <div class="carre carre__2"></div>
    <div class="card card__1">
      <h2 class="titre">Résumé de vos réponses</h2>
      <div class="list" v-for="(item, index) in post" :key="index">
        <h5 class="question">{{ item.question }}</h5>
        <ul>
          <li :class="{ reponse__true : isCorrect(index) }">{{ item.reponse }}</li>
        </ul>
      </div>
      <button v-on:click="correction" v-if="active">Valider</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Reponses",
  props: ["post"],
  data() {
    return {
      select: [],
      nbReponses: 0,
      active: false
    };
  },
  updated() {
    this.nbReponses = 0;
    this.post.forEach(element => {
      if (element.reponse != "") {
        this.nbReponses = this.nbReponses + 1;
      }
    });
    if (this.nbReponses >= 10) {
      this.active = true;
    }
  },
  methods: {
    correction() {
      for (const value in this.select) {
        this.select[value] = false;
      }
      this.post.forEach(element => {
        if (element.reponse === element.solution) {
          this.$set(
            this.select,
            this.post.indexOf(element),
            !this.select[this.post.indexOf(element)]
          );
        }
      });
    },
    isCorrect(index) {
      return this.select[index];
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.card {
  background: #ffffff;
  padding: 1rem 2rem;
  position: relative;
  z-index: 10;
  &__1 {
    box-shadow: 0 2px 1px -1px rgba(0, 0, 0, 0.2),
      0 1px 1px 0 rgba(0, 0, 0, 0.14), 0 1px 3px 0 rgba(0, 0, 0, 0.12);
  }
}
.titre {
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 0.1rem;
  margin-bottom: 2rem;
}
.question {
  text-transform: uppercase;
  letter-spacing: 0.15rem;
  margin: 0;
}
button {
  position: absolute;
  z-index: 15;
  font-size: 1rem;
  right: 10px;
  bottom: 10px;
  background-color: #4caf50;
  border: none;
  color: white;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  cursor: pointer;

  &:hover {
    box-shadow: 0 3px 5px -1px rgba(0, 0, 0, 0.2),
      0 5px 8px 0 rgba(0, 0, 0, 0.14), 0 1px 14px 0 rgba(0, 0, 0, 0.12);
  }
}
.reponse__true {
  color: #4caf50;
}
.reponse__false {
  color: rgb(204, 85, 56);
}
ul {
  list-style: none; /* Remove default bullets */
}
ul li::before {
  content: "\2022"; /* Add content: \2022 is the CSS Code/unicode for a bullet */
  color: black; /* Change the color */
  font-weight: bold; /* If you want it to be bold */
  display: inline-block; /* Needed to add space between the bullet and the text */
  width: 1em; /* Also needed for space (tweak if needed) */
  margin-left: -1em; /* Also needed for space (tweak if needed) */
}
.carre {
  width: 100px;
  height: 100px;
  background: rgba(20, 137, 221, 0.7);
  position: absolute;
  z-index: 1;
  &__1 {
    top: -20px;
    left: -20px;
  }
  &__2 {
    bottom: -20px;
    right: -20px;
  }
}
</style>