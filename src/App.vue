<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforStart($event)"
  />
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
    @onFinish="onGetResult()"
  />
  <result-screen
    v-if="statusMatch === 'result'"
    :timer="timer"
    @startAgain="statusMatch = 'default'"
  />
  <coppy-right />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
import { shuffed } from "./untils/array.js";
import CoppyRight from "./components/CoppyRightScreen.vue";
export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
    CoppyRight,
  },
  data() {
    return {
      settings: {
        totalOfBlock: 0,
        cardsContext: [],
        startedAt: null,
        timer: 0,
      },
      statusMatch: "default",
    };
  },
  methods: {
    onHandleBeforStart(config) {
      this.settings.totalOfBlock = config.totalOfBlock;

      const firstCards = Array.from(
        { length: this.settings.totalOfBlock / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const card = [...firstCards, ...secondCards];
      this.settings.cardsContext = shuffed(shuffed(shuffed(shuffed(card))));
      this.settings.startedAt = new Date().getTime();

      this.statusMatch = "match";
    },
    onGetResult() {
      this.timer = new Date().getTime() - this.settings.startedAt;

      console.log(this.timer);
      this.statusMatch = "result";
    },
  },
};
</script>
