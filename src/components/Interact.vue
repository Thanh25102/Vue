<template>
  <h1>Interact running ....</h1>
  <CardPokemon v-for="(card, index) in cardsContext" :key="index" />
</template>

<script lang="js">
import CardPokemon from './Card.vue'
export default {
  name: 'InteractScreen',
  props: {
    cardsContext: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  components: {
    CardPokemon
  }
}
</script>
