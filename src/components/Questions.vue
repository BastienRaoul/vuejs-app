<template>
  <div class="bloc">
    <h3 class="titre">{{ post.question }}</h3>
    <ul>
      <li v-for="(reponse, index) in post.reponses" :key="index">
        <div
          class="card card__1"
          :class="{ card__active: isActive(index) }"
          v-on:click="selected(reponse, index), $emit('addSolution', solution)"
        >
          <h4 class="reponses">{{ reponse }}</h4>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Question",
  props: ["post"],
  data() {
    return {
      solution: {
        question: "",
        reponse: ""
      },
      select: []
    };
  },
  methods: {
    selected(reponse, index) {
      this.solution.question = this.post.question;
      this.solution.reponse = reponse;

      // Change la selection de l'item
      for (const value in this.select) {
        this.select[value] = false;
      }
      this.$set(this.select, index, !this.select[index]);
    },
    isActive(index) {
      return this.select[index];
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.bloc {
  margin-bottom: 30px;
}
.titre {
  text-transform: uppercase;
  letter-spacing: 0.2rem;
}
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
.reponses {
  text-transform: uppercase;
  letter-spacing: 0.1rem;
}
.card {
  background: #ffffff;
  margin: 0.5rem;
  display: inline-block;
  padding: 0.2rem 0 0.2rem 0;
  width: 25vw;
  text-align: center;
  border-radius: 2rem;
  cursor: pointer;

  &__1 {
    box-shadow: 0 2px 1px -1px rgba(0, 0, 0, 0.2),
      0 1px 1px 0 rgba(0, 0, 0, 0.14), 0 1px 3px 0 rgba(0, 0, 0, 0.12);
    transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);

    &:hover {
      box-shadow: 0 3px 5px -1px rgba(0, 0, 0, 0.2),
        0 5px 8px 0 rgba(0, 0, 0, 0.14), 0 1px 14px 0 rgba(0, 0, 0, 0.12);
    }
  }

  &__active {
    box-shadow: 0 3px 5px -1px rgba(0, 0, 0, 0.2),
      0 5px 8px 0 rgba(0, 0, 0, 0.14), 0 1px 14px 0 rgba(0, 0, 0, 0.12);
  }
}
</style>