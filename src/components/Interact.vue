<template>
  <div class="screen">
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((getVh() - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) /
            4 +
            16) *
          Math.sqrt(cardsContext.length)
        }px`
      }"
    >
      <CardPokemon
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        :cardsContext="cardsContext"
        @onFlip="checkRule($event)"
      />
    </div>
  </div>
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
      if (this.rules.length === 2) return false
      this.rules.push(card)

      if (this.rules.length === 2 && this.rules[0].value === this.rules[1].value) {
        // add class disable , reset rules
        this.$refs[`card-${this.rules[0].index}`][0].onEnabledDisableMode()
        this.$refs[`card-${this.rules[1].index}`][0].onEnabledDisableMode()

        this.rules = []
        const disableElements = document.querySelectorAll('.screen .card.card__disabled')
        if (disableElements && disableElements.length === this.cardsContext.length - 2) {
          setTimeout(() => {
            this.$emit('onFinish')
          }, 920)
        }
      } else if (this.rules.length === 2 && this.rules[0].value !== this.rules[1].value) {
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard()
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard()
          this.rules = []
        }, 800)
      } else return false
    },
    getVh () {
      return Math.max(document.documentElement.clientHeight || 0, window.innerHeight || 0)
    }
  }
}
</script>
<style lang="css" scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}
.screen__inner {
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
