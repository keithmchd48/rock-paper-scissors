<template>
  <div id="app">
    <div class="main-container">
      <div class="legend-div">
        <Legend></Legend>
      </div>
      <div class="match">
        <Selections :clickHandler="clickHandler"></Selections>
        <Results :userWins="userWins"
                 :computerWins="computerWins"
                 :matchArray="matchArray">
        </Results>
      </div>
    </div>
  </div>
</template>

<script>
import Selections from "@/components/Selections";
import Results from "@/components/Results";
import Legend from "@/components/Legend";
const SELECTIONS = [
  {
    name: 'rock',
    emoji: '✊',
    beats: ['scissors', 'lizard']
  },
  {
    name: 'paper',
    emoji: '📄',
    beats: ['rock', 'spock']
  },
  {
    name: 'scissors',
    emoji: '✂️',
    beats: ['paper', 'lizard']
  },
  {
    name: 'lizard',
    emoji: '🦎',
    beats: ['spock', 'paper']
  },
  {
    name: 'spock',
    emoji: '🖖',
    beats: ['scissors', 'rock']
  },
]
export default {
  name: 'App',
  components: {Legend, Results, Selections},
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
      if (player1.beats.includes(player2.name)) {
        return 1
      }
      if (player2.beats.includes(player1.name)) {
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
    background-color: mintcream;
  }
  .main-container {
    display: grid;
    grid-template-columns: 30% 70%;
    justify-items: center;
  }
@media only screen and (max-width: 860px) {
  .main-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    justify-items: center;
  }
  .legend-div {
    margin-bottom: 3rem;
  }
}
</style>
