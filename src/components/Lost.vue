<template>
    <div class="endgame-container" id="loss">
        <div class="flex-container">
            <h1>😝 Unlucky 😝</h1>
            <h2>You Lost with the word : {{this.word}}</h2>
            <button @click="resetGame">Reset Game</button>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Lost',
  props: ['word'],
  methods: {
    //Reset game event, this causes the getWord function to be called, resetting all variables and making a call for a new word.
    resetGame() {
      this.$emit('gameResetEvent')
    },
  }
}
</script>

<style>

#loss {
  background: linear-gradient(60deg, rgb(245, 90, 78, 0.801), rgb(243, 44, 30, 0.801));
}

</style>