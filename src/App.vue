<template>
  <MainScreen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeMatch($event)"
  />
  <InteractScreen v-if="statusMatch === 'match'" :cardsContext="cardContext" />
  <CopyRight />
</template>

<script lang="js">
import MainScreen from './components/Main.vue'
import InteractScreen from './components/Interact.vue'
import CopyRight from './components/Footer.vue'
import { shuffled } from './utils/array'
export default {
  name: 'App',
  data: () => {
    return {
      settings: {
        totalOfBlocks: 0,
        cardContext: [],
        startedAt: null
      },
      statusMatch: 'default'
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
    }
  },
  components: {
    MainScreen,
    CopyRight,
    InteractScreen
  }
}
</script>

<style></style>
