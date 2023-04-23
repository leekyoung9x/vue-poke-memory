<template>
  <div class="screen">
    <h1>POKE MEMORIES</h1>
    <p>SELECT MODE TO START GAME</p>
    <div class="modes">
      <button @click="onStart(16)">
        <span> 4x4 </span>
        <span>Easy</span>
      </button>
      <button @click="onStart(36)">
        <span> 6x6 </span>
        <span>Normal</span>
      </button>
      <button @click="onStart(64)">
        <span> 8x8 </span>
        <span>Hard</span>
      </button>
      <button @click="onStart(100)">
        <span> 10x10 </span>
        <span>Super Hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", { totalOfBlocks });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/style/globall.scss";

.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-color: $dark-color;
  color: $light-color;
  h1 {
    font-size: 4.5rem;
    text-transform: uppercase;
  }
  p {
    font-size: 2rem;
  }
}
.modes {
  display: flex;
  margin-top: 2rem;

  button {
    font: var(--font);
    width: 150px;
    height: 150px;
    background: transparent;
    box-shadow: none;
    border: 1px solid $light-color;
    color: $light-color;
    display: flex;
    flex-direction: column;
    border-radius: 1rem;
    margin: 0 1rem;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: background 0.3s ease-in-out;

    &:hover {
      background-color: $light-color;
      color: $dark-color;
    }

    span {
      &:first-child {
        font-size: 2rem;
      }

      &:last-child {
        display: block;
        font-size: 1.25rem;
        margin-top: 0.5rem;
      }
    }
  }
}
</style>
