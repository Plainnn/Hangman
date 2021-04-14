<template>
    <div class="endgame-container" id="win">
        <div class="flex-container">
            <h1>🎊 Congratulations 🎊</h1>
            <h2>You won with the word : {{this.word}}</h2>
            <button @click="resetGame">Reset Game</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Win',
    props:['word'],
    methods: {
        //Reset game event, this causes the getWord function to be called, resetting all variables and making a call for a new word.
        resetGame() {
            this.$emit('gameResetEvent')
        },
    }
}
</script>

<style>

#win {
    background: linear-gradient(60deg, rgba(126, 177, 97, 0.801), rgba(101, 149, 74, 0.801));
    color: #fff;
    z-index: 999;
}

</style>