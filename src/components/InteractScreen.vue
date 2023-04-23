<template>
  <div class="screen">
    <div class="screen__inner">
      <div v-for="n in maTran" :key="`row-card-${n}`" style="display: flex">
        <card-flip
          v-for="m in maTran"
          :key="(n - 1) * maTran + m - 1"
          :ref="`card-${(n - 1) * maTran + m - 1}`"
          :imgBackFaceUrl="`images/${
            cardContext[(n - 1) * maTran + m - 1]
          }.png`"
          :card="{
            index: (n - 1) * maTran + m - 1,
            value: cardContext[(n - 1) * maTran + m - 1],
          }"
          :maTran="maTran"
          @onFlipped="checkRule($event)"
        ></card-flip>
      </div>
    </div>
  </div>
</template>

<script>
import CardFlip from "./Card.vue";
export default {
  components: { CardFlip },
  data() {
    return {
      rules: [],
      maTran: 0,
      countRight: 0,
    };
  },

  props: {
    cardContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  beforeMount() {
    this.maTran = Math.sqrt(this.cardContext.length);
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) {
        return false;
      } else {
        this.rules.push(card);
      }

      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        // Close two card
        this.$refs[`card-${this.rules[0].index}`][0].onDisabledCard();
        this.$refs[`card-${this.rules[1].index}`][0].onDisabledCard();
        // Reset rules to []
        this.rules = [];

        // Remember count
        this.countRight += 2;

        if (this.countRight == this.cardContext.length) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 920);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        let cardFirst = this.$refs[`card-${this.rules[0].index}`][0],
          secondCard = this.$refs[`card-${this.rules[1].index}`][0];

        // Reset rules to []
        this.rules = [];

        setTimeout(() => {
          // Close two card
          cardFirst.onFlipBackCard();
          secondCard.onFlipBackCard();
        }, 800);
      } else {
        return false;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/style/globall.scss";

.screen {
  height: 100%;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: $dark-color;
  color: $light-color;
  display: flex;
  align-items: center;
  justify-content: center;
}

.screen__inner {
  margin: 2rem;
}
</style>
