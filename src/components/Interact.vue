<template>
  <h1>Interact running ....</h1>
  <CardPokemon
    v-for="(card, index) in cardsContext"
    :key="index"
    :imgBackFaceUrl="`images/${card}.png`"
    :card="card"
    @onFlip="checkRule($event)"
  />
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
  data: () => {
    return {
      rules: []
    }
  },
  components: {
    CardPokemon
  },
  methods: {
    checkRule (card) {
      console.log(card)
    }
  }
}
</script>
