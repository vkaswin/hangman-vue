<script setup>
import { useCssModule } from "vue";
defineProps({ incorrectLetters: { type: Number } });

const styles = useCssModule("styles");
let hangMan = [
  `<div  class=${styles.head} />`,
  `<div class=${styles.body}></div>`,
  `<div class=${styles.hand} position='left'></div>`,
  `<div class=${styles.hand} position='right'></div>`,
  `<div class=${styles.foot} position='left'></div>`,
  `<div class=${styles.foot} position='right'></div>`,
];
</script>

<template>
  <div :class="styles.container">
    <template v-for="n in incorrectLetters" :key="n">
      <div v-html="hangMan[n - 1]"></div>
    </template>
    <div :class="styles.bottom_bar"></div>
    <div :class="styles.side_bar"></div>
    <div :class="styles.top_bar"></div>
  </div>
</template>

<style lang="scss" module="styles">
.container {
  position: relative;
  min-height: 300px;
  .bottom_bar {
    position: absolute;
    bottom: 0px;
    left: 25%;
    border-bottom: 4px solid black;
    width: 50%;
  }
  .side_bar {
    position: absolute;
    bottom: 0px;
    left: 35%;
    height: 100%;
    border-left: 4px solid black;
  }
  .top_bar {
    position: absolute;
    top: 0px;
    left: 35%;
    border-bottom: 4px solid black;
    width: 114px;
    &::after {
      content: "";
      position: absolute;
      right: 0px;
      height: 54px;
      border-left: 4px solid black;
    }
  }
  .head {
    position: absolute;
    left: 50%;
    top: 50px;
    transform: translateX(-50%);
    border: 4px solid black;
    width: 50px;
    height: 50px;
    border-radius: 50%;
  }
  .body {
    position: absolute;
    top: 104px;
    left: 50%;
    transform: translateX(-50%);
    height: 100px;
    border: 2px solid black;
  }
  .hand {
    position: absolute;
    top: 125px;
    height: 50px;
    border: 2px solid black;
  }
  .hand[position="left"] {
    left: 47.5%;
    transform: translateX(-50%) rotate(135deg);
  }
  .hand[position="right"] {
    left: 52.5%;
    transform: translateX(-50%) rotate(45deg);
  }
  .foot {
    position: absolute;
    top: 199px;
    height: 50px;
    border: 2px solid black;
  }
  .foot[position="left"] {
    left: 47.5%;
    transform: translateX(-50%) rotate(45deg);
  }
  .foot[position="right"] {
    left: 52.5%;
    transform: translateX(-50%) rotate(-45deg);
  }
}

@media only screen and (max-width: 768px) {
  .container {
    .bottom_bar {
      left: 0px;
      width: 100%;
    }
    .side_bar {
      left: 25%;
    }
    .top_bar {
      left: 25%;
      width: 120px;
    }
    .head {
      left: calc(25% + 120px);
    }
    .body {
      left: calc(25% + 120px);
    }
    .hand {
      position: absolute;
      top: 125px;
      height: 50px;
      border: 2px solid black;
    }
    .hand[position="left"] {
      left: calc(25% + 102px);
      transform: translateX(-50%) rotate(135deg);
    }
    .hand[position="right"] {
      left: calc(25% + 138px);
      transform: translateX(-50%) rotate(45deg);
    }
    .foot {
      position: absolute;
      top: 199px;
      height: 50px;
      border: 2px solid black;
    }
    .foot[position="left"] {
      left: calc(25% + 102px);
      transform: translateX(-50%) rotate(45deg);
    }
    .foot[position="right"] {
      left: calc(25% + 138px);
      transform: translateX(-50%) rotate(-45deg);
    }
  }
}
</style>
