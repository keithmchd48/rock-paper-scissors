<template>
  <div class="selections">
    <div class="selections__row">
      <button class="selections__row__cell" @click="clickHandler('rock')">✊</button>
      <button class="selections__row__cell" @click="clickHandler('paper')">📄</button>
      <button class="selections__row__cell" @click="clickHandler('scissors')">✂️</button>
      <button class="selections__row__cell" @click="clickHandler('lizard')">🦎</button>
      <button class="selections__row__cell" @click="clickHandler('spock')">🖖</button>
    </div>
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

<style scoped lang="scss">
  .selections {
    display: table;
    width: 100%;

    &__row {
      display: table-row;

      &__cell {
        background: none;
        border: none;
        outline: none;
        cursor: pointer;
        font-size: 4rem;
        transition: 100ms;
        display: table-cell;
        padding: 0;
        
        &:hover {
          transform: scale(1.2);
        }
      }
    }
  }

  @media only screen and (max-width: 375px) {
    .selections {
      &__row {
        &__cell {
          font-size: 3rem;
        }
      }
    }
  }

</style>
