<template>
  <div>
    <h1>Friends Trivia</h1>
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
  color: goldenrod;
}
</style>