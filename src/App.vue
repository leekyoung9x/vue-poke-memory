<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  ></main-screen>
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardContext="settings.cardContext"
    @onFinish="onGetResult"
  ></interact-screen>
  <result-screen
    v-if="statusMatch === 'result'"
    :timer="settings.timer"
    @onStartAgain="statusMatch = 'default'"
  ></result-screen>
  <copy-right-screen></copy-right-screen>
</template>

<script>
import CopyRightScreen from "./components/CopyRightScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import MainScreen from "./components/MainScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";

import { shuffled } from "./utils/array";

export default {
  name: "App",
  components: { CopyRightScreen, MainScreen, InteractScreen, ResultScreen },
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardContext: [],
        startedAt: null,
        timer: 0,
      },
      statusMatch: "default",
    };
  },
  methods: {
    onHandleBeforeStart(config) {
      this.settings.totalOfBlocks = config.totalOfBlocks;

      const firstCard = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );

      const secondCard = [...firstCard];

      const card = [...firstCard, ...secondCard];

      this.settings.cardContext = shuffled(shuffled(shuffled(shuffled(card))));

      this.settings.startedAt = new Date().getTime();

      // data ready
      this.statusMatch = "match";
    },

    onGetResult() {
      // Get timer
      this.settings.timer = new Date().getTime() - this.settings.startedAt;
      // Switch to result
      this.statusMatch = "result";
      console.log(this.settings.timer);
    },
  },
};
</script>

<style lang="scss"></style>
