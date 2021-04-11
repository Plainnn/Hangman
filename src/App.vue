<template>
  <div id="app">
    <Title />
    <div v-if="gameLost">
      <Lost />
    </div>
    <div v-if="gameWon">
      <Won />
    </div>
    <div v-if="randomWord">
      <HangmanDrawing :mistakesMade="mistakesMade"/>
        <WordContainer :word="randomWord" @mistakeMade="updateDrawing" @gameLostEvent="updateGameLost" @gameWonEvent="updateGameWon"/>
      </div>
  </div>
</template>

<script>
import axios from 'axios';
import Title from "./components/Title";
import HangmanDrawing from "./components/HangmanDrawing";
import WordContainer from "./components/WordContainer";
import Won from "./components/Won";
import Lost from "./components/Lost";


export default {
  name: "App",
  components: { Title, HangmanDrawing,WordContainer, Won, Lost },
  data() {
    return {
      words: ['celery', 'room', 'headphones', 'bottle'],
      wordToGuess: null,
      mistakesMade: 0,
      data: null,
      gameWon: false,
      gameLost: false
    };
  },
  created() {
    var options = {
    method: 'GET',
    url: 'https://wordsapiv1.p.rapidapi.com/words/',
    params: {random: 'true', lettersMax: '10', lettersMinimum: '3'},
    headers: {
      'x-rapidapi-key': 'd375c1fa52msh95d673120642a1bp16e2f4jsn32785359658b',
      'x-rapidapi-host': 'wordsapiv1.p.rapidapi.com'
    }
  };

  axios.request(options).then( (response) => {
    console.log(response)
    this.data = response.data;
    }).catch(function (error) {
      console.error(error);
  });

  },
  computed: {
    randomWord() {
      return this.data ? this.data.word : null;
    }
  },
  methods: {
    updateDrawing(mistakesMade) {
      this.mistakesMade = mistakesMade;
    },
    updateGameLost() {
      this.gameLostCheck = true;
    },
    updateGameWon() {
      this.gameLostCheck = true;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


</style>
