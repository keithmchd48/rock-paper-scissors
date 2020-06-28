<template>
  <div class="results">
    <div>
      You
      <span class="result-score">{{userWins}}</span>
    </div>
    <div>
      Computer
      <span class="result-score">{{computerWins}}</span>
    </div>
    <div v-for="(arr, key) in matchArray"
         :key="key"
         class="result-selection"
         :class="[{'winner': arr.winner}]">
      {{arr.emoji}}
    </div>
  </div>
</template>

<script>
  export default {
    name: "Results",
    props: {
      userWins: {
        type: Number,
        default: 0
      },
      computerWins: {
        type: Number,
        default: 0
      },
      matchArray: {
        type: Array
      }
    }
  }
</script>

<style scoped>
  .results {
    margin-top: 1rem;
    font-size: 2rem;
    display: grid;
    justify-content: center;
    grid-template-columns: repeat(2, 1fr);
    justify-items: center;
    align-items: center;
  }
  .result-score {
    margin-left: .1rem;
    font-size: 1.2rem;
    color: #333;
  }
  .result-selection {
    opacity: .5;
  }
  .result-selection.winner {
    opacity: 1;
    font-size: 2.4rem;
  }
</style>
