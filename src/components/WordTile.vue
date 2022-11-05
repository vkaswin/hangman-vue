<script setup>
let pros = defineProps({
  wordToFind: {
    type: String,
    default: "",
  },
  guessedWord: {
    type: String,
    default: "",
  },
});
</script>

<template>
  <ul :class="styles.tile">
    <li v-for="(word, index) in wordToFind" :key="index">
      <span>
        {{ guessedWord.includes(word) ? word : "" }}
      </span>
    </li>
  </ul>
</template>

<style lang="scss" module="styles">
.tile {
  display: flex;
  justify-content: center;
  gap: 10px;
  height: 65px;
  margin-top: 20px;
  li {
    width: 50px;
    list-style: none;
    border-bottom: 4px solid black;
    position: relative;
    span {
      position: absolute;
      left: 50%;
      bottom: -10px;
      transform: translate(-50%);
      font-size: 42px;
      text-transform: uppercase;
    }
  }
}
</style>
