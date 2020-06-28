<template>
  <div id="app">
    <div class="selections">
      <button class="selection" @click="clickHandler('rock')">✊</button>
      <button class="selection" @click="clickHandler('paper')">✋</button>
      <button class="selection" @click="clickHandler('scissors')">✌</button>
    </div>
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
  </div>
</template>

<script>
const SELECTIONS = [
  {
    name: 'rock',
    emoji: '✊',
    beats: 'scissors'
  },
  {
    name: 'paper',
    emoji: '✋',
    beats: 'rock'
  },
  {
    name: 'scissors',
    emoji: '✌',
    beats: 'paper'
  }
]
export default {
  name: 'App',
  data () {
    return {
      userWins: 0,
      computerWins: 0,
      matchArray: []
    }
  },
  methods: {
    clickHandler (chosen) {
      const userSelection = SELECTIONS.find(x => x.name === chosen)
      const computerSelection = this.computerSelection()
      const winner = this.determineWinner(userSelection, computerSelection)
      // if user wins
      if (winner === 1) {
        this.userWins++
        this.unshiftToMatchArray(
          computerSelection.emoji,
          userSelection.emoji,
          false,
          true
        )
      }
      // if computer wins
      if (winner === 2) {
        this.computerWins++
        this.unshiftToMatchArray(
          computerSelection.emoji,
          userSelection.emoji,
          true,
          false
        )
      }
      // if match is drawn
      if (winner === 0) {
        this.unshiftToMatchArray(
          computerSelection.emoji,
          userSelection.emoji,
          false,
          false
        )
      }
    },
    determineWinner (player1, player2) {
      if (player1.beats === player2.name) {
        return 1
      }
      if (player2.beats === player1.name) {
        return 2
      }
      return 0
    },
    computerSelection () {
      const random = Math.floor(Math.random() * SELECTIONS.length)
      return SELECTIONS[random]
    },
    unshiftToMatchArray (computerEmoji, userEmoji, computerWinner, userWinner) {
      this.matchArray.unshift({
        emoji: computerEmoji,
        winner: computerWinner
      })
      this.matchArray.unshift({
        emoji: userEmoji,
        winner: userWinner
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  /*-webkit-font-smoothing: antialiased;*/
  /*-moz-osx-font-smoothing: grayscale;*/
}
  body {
    background-color: #ccc;
  }
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
