<template>
  <div>
    <div class='friends'>
        <img src='@/assets/friends-logo-cover-958x575.png' :width='700' >
    </div>
    <h1 class="title">T R I V I A</h1>
    <button @click="hideAll" class="flat-button">HIDE ALL</button>
    <div class="difficulty-options">
      <difficulty-options
        :difficulty="selectedDifficulty"
        @difficulty-change="handleDifficultyChange"
      />
    </div>
    <div class="questions">
      <div v-for="card in displayedTrivia" :key="card.id">
        <flash-card :card="card" @toggle="handleToggle" />
      </div>
    </div>
  </div>
</template>

<script>
import trivia from "../trivia";
import DifficultyOptions from "./DifficultyOptions.vue";
import FlashCard from "./FlashCard";
export default {
  components: { FlashCard, DifficultyOptions },
  data() {
    return {
      trivia: [...trivia],
      selectedDifficulty: "all"
    };
  },
  methods: {
    handleToggle(card) {
      card.answerShown = !card.answerShown;
    },
    handleDifficultyChange(difficulty) {
      this.selectedDifficulty = difficulty;
    },
    hideAll() {
      this.trivia.forEach(t => (t.answerShown = false));
    }
  },
  computed: {
    displayedTrivia() {
      if (this.selectedDifficulty === "all") {
        return this.trivia;
      }
      return this.trivia.filter(t => t.difficulty === this.selectedDifficulty);
    }
  }
};
</script>

<style scoped>
.friends {
    margin-top: 60px;
}
.title {
    color: white;
    margin-top: -5px;
    margin-bottom: 50px;
}
.questions {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
}
.flat-button {
  background: transparent;
  border: none;
  cursor: pointer;
  margin-bottom: 10px;
  font-size: 20px;
  color: rgb(32, 137, 218);
}
</style>