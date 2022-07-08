<template>
  <MainScreen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeMatch($event)"
  />
  <InteractScreen v-if="statusMatch === 'match'" />
  <CopyRight />
</template>

<script lang="js">
import MainScreen from './components/Main.vue'
import InteractScreen from './components/Interact.vue'
import CopyRight from './components/Footer.vue'
export default {
  name: 'App',
  data: () => {
    return {
      statusMatch: 'default'
    }
  },
  methods: {
    onHandleBeforeMatch (config) {
      console.log(config)
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
