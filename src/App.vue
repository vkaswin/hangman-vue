<script setup>
import Keyboard from "@/components/KeyBoard.vue";
import HangMan from "@/components/HangMan.vue";
import WordTile from "@/components/WordTile.vue";
import wordList from "@/data/words.json";
import { onMounted, onUnmounted, ref, watch } from "vue";

let wordToFind = ref("");
let guessedWord = ref("");
let incorrectLetters = ref(0);
let message = ref("");

onMounted(() => {
  getRandomWord();
  document.addEventListener("keydown", handleKeyDown);
});

onUnmounted(() => {
  document.removeEventListener("keydown", handleKeyDown);
});

const getRandomWord = () => {
  wordToFind.value = wordList[Math.floor(Math.random() * wordList.length)];
};

const handleKeyDown = ({ key }) => {
  const regex = /^[a-z]$/;
  if (!regex.test(key)) return;
  addWordInTile(key);
};

watch(incorrectLetters, () => {
  if (incorrectLetters.value >= 6)
    return showToastMsg(
      `Lost the Game! Correct word is ${wordToFind.value}, Try Again`
    );
});

const showToastMsg = (msg) => {
  message.value = msg;
  setTimeout(() => {
    handleRestart();
  }, 2000);
};

const handleRestart = () => {
  getRandomWord();
  guessedWord.value = "";
  message.value = "";
  incorrectLetters.value = 0;
};

const addWordInTile = (word) => {
  guessedWord.value = guessedWord.value.concat(word);
  let isWin = [...wordToFind.value].every((word) => {
    return guessedWord.value.includes(word);
  });
  if (isWin) return showToastMsg("Won the Game! Find next word");
  if (!wordToFind.value.includes(word)) {
    incorrectLetters.value = incorrectLetters.value + 1;
  }
};
</script>

<template>
  <div :class="styles.container">
    <HangMan :incorrectLetters="incorrectLetters" />
    <WordTile :wordToFind="wordToFind" :guessedWord="guessedWord" />
    <Keyboard
      :onClick="addWordInTile"
      :guessedWord="guessedWord"
      :wordToFind="wordToFind"
    />
  </div>
  <div v-if="message.length > 0" :class="styles.toast">
    <span>{{ message }}</span>
  </div>
</template>

<style lang="scss" module="styles">
.container {
  max-width: 750px;
  margin: 0px auto;
  padding: 15px;
}
.toast {
  position: fixed;
  top: 20px;
  left: 50%;
  transform: translateX(-50%);
  min-width: 150px;
  padding: 7px 15px;
  background-color: #000;
  color: white;
  border-radius: 4px;
  span {
    display: block;
    text-align: center;
  }
}

@media only screen and (max-width: 600px) {
  .toast {
    width: 100%;
    max-width: 80%;
  }
}
</style>
