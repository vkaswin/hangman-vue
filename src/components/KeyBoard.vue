<script setup>
import keyboard from "@/data/keyboard.json";

defineProps({
  onClick: { type: Function, default: () => {} },
  guessedWord: { type: String, default: "" },
  wordToFind: { type: String, default: "" },
});
</script>

<template>
  <div :class="styles.container">
    <div v-for="(list, index) in keyboard" :key="index" :class="styles.wrapper">
      <button
        v-for="(word, index) in list"
        :class="styles.tile"
        :key="index"
        :disabled="guessedWord.includes(word)"
        :state="
          wordToFind.includes(word) && guessedWord.includes(word)
            ? 'correct'
            : guessedWord.includes(word)
            ? 'disable'
            : ''
        "
        @click="onClick(word)"
      >
        {{ word }}
      </button>
    </div>
  </div>
</template>

<style lang="scss" module="styles">
.container {
  display: flex;
  flex-direction: column;
  gap: 10px;
  max-width: 750px;
  width: 100%;
  margin: 40px auto 0px auto;
  .wrapper {
    display: flex;
    justify-content: center;
    gap: 10px;
    .tile {
      width: 50px;
      height: 50px;
      border-radius: 4px;
      font-size: 20px;
      text-transform: uppercase;
      background-color: #d3d6da;
      color: #000;
      border: none;
      cursor: pointer;
      &:disabled {
        cursor: not-allowed;
      }
    }
    .tile[state="correct"] {
      background-color: #6aaa64;
      color: white;
    }
    .tile[state="wrong"] {
      background-color: red;
      color: white;
    }
    .tile[state="disable"] {
      opacity: 0.5;
    }
  }
}
</style>
