<template>
  <div id="app">
    <Selections :clickHandler="clickHandler"></Selections>
    <Results :userWins="userWins"
             :computerWins="computerWins"
             :matchArray="matchArray">
    </Results>
  </div>
</template>

<script>
import Selections from "@/components/Selections";
import Results from "@/components/Results";
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
  components: {Results, Selections},
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
</style>
