<template>
    <section class="win-loss-container">
        <h3> 🏆 Won : {{gamesWon}}</h3>
        <h3> 💩 Lost: {{gamesLost}}</h3>
    </section>
</template>

<script>
export default {
    name: 'WinLossCounter',
    props: ['gamesWon', 'gamesLost']
}
</script>

<style>
    .win-loss-container {
        display:flex;
        align-items: center;
        justify-content: center;
        text-transform: capitalize;;
    }

    .win-loss-container h3{
        padding:10px 10px 0 10px;

    }
</style>