<template>
  <MainScreen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeMatch($event)"
  />
  <InteractScreen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardContext"
    @onFinish="onGetResult"
  />
  <Result
    v-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="statusMatch = 'default'"
  />
  <CopyRight />
</template>

<script lang="js">
import MainScreen from './components/Main.vue'
import InteractScreen from './components/Interact.vue'
import Result from './components/Result.vue'
import { shuffled } from './utils/array'
export default {
  name: 'App',
  components: {
    MainScreen,
    InteractScreen,
    Result
  },
  data: () => {
    return {
      settings: {
        totalOfBlocks: 0,
        cardContext: [],
        startedAt: null
      },
      statusMatch: 'default',
      timer: 0
    }
  },
  methods: {
    onHandleBeforeMatch (config) {
      this.settings.totalOfBlocks = config.totalOfBlocks
      const firstCards = Array.from({ length: this.settings.totalOfBlocks / 2 }, (_, i) => i + 1)
      const secondCards = [...firstCards]
      const cards = [...firstCards, ...secondCards]
      this.settings.cardContext = shuffled(shuffled(shuffled(shuffled(cards))))
      this.settings.startedAt = new Date().getTime()
      this.statusMatch = 'match'
    },
    onGetResult () {
      // get timer
      this.timer = new Date().getTime() - this.settings.startedAt
      // switch component
      this.statusMatch = 'result'
    }
  }
}
</script>

<style></style>
