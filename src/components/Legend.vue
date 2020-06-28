<template>
  <div class="legend-container">
    <div>Rock(✊) smashes Scissors(✂️)</div>
    <div>Rock(✊) crushes Lizard(🦎)</div>
    <div>Paper(✋) covers Rock(✊)</div>
    <div>Paper(✋) disproves Spock(🖖)</div>
    <div>Scissors(✌) cuts Paper(📄)</div>
    <div>Scissors(✌) decapitates Lizard(🦎)</div>
    <div>Lizard(🦎) poisons Spock(🖖)</div>
    <div>Lizard(🦎) eats Paper(📄)</div>
    <div>Spock(🖖) smashes Scissors(✂️)</div>
    <div>Spock(🖖) vaporizes Rock(✊)</div>
  </div>
</template>

<script>
  export default {
    name: "Legend"
  }
</script>

<style scoped>
  .legend-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
</style>
