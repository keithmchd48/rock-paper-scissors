<template>
  <div class="selections">
    <button class="selection" @click="clickHandler('rock')">✊</button>
    <button class="selection" @click="clickHandler('paper')">✋</button>
    <button class="selection" @click="clickHandler('scissors')">✌</button>
  </div>
</template>

<script>
  export default {
    name: "Selections",
    props: {
      clickHandler: {
        type: Function
      }
    }
  }
</script>

<style scoped>
  .selections {
    display: flex;
    justify-content: center;
  }
  .selection {
    background: none;
    border: none;
    outline: none;
    cursor: pointer;
    font-size: 4rem;
    transition: 100ms;
  }
  .selection:hover {
    transform: scale(1.2);
  }

</style>
