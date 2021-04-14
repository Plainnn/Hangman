<template>
  <div id="app">
    <Title />
    <div v-if="gameLostCheck">
      <Lost :word="randomWord"  @gameResetEvent="updateGameReset"/>
    </div>
    <div v-else-if="gameWonCheck">
      <Won :word="randomWord" @gameResetEvent="updateGameReset"/>
    </div>
    <div v-else-if="loading">
      <h5>Searching for a word...</h5>
    </div>
     <div v-if="randomWord">
      <HangmanDrawing :mistakesMade="mistakesMade"/>
      <WordContainer :word="randomWord" @mistakeMade="updateDrawing" @gameLostEvent="updateGameLost" @gameWonEvent="updateGameWon" />
    </div>
    <WinLossCounter :gamesWon="gamesWon" :gamesLost="gamesLost"/>
  </div>
</template>

<script>
import axios from 'axios';
import Title from "./components/Title";
import HangmanDrawing from "./components/HangmanDrawing";
import WordContainer from "./components/WordContainer";
import Won from "./components/Won";
import Lost from "./components/Lost";
import WinLossCounter from "./components/WinLossCounter";

export default {
  name: "App",
  components: { Title, HangmanDrawing,WordContainer, Won, Lost, WinLossCounter },
  data() {
    return {
      gamesWon: 0,
      gamesLost: 0,
      words: ['celery', 'room', 'headphones', 'bottle'],
      wordToGuess: null,
      mistakesMade: 0,
      data: null,
      gameLostCheck: false,
      gameWonCheck: false,
      loading: true
    };
  },
async created() {
    this.getWord()
  },
  computed: {
    randomWord() {
      //If this.data exists, return the word.
      return this.data ? this.data.word : null;
    }
  },
  methods: {
    //Update the drawing, using a switch statement in HangmanDrawing to determine which step.
    updateDrawing(mistakesMade) {
      this.mistakesMade = mistakesMade;
    },
    //Show the Lost component
    updateGameLost() {
      this.gamesLost++;
      this.gameLostCheck = true;
    },
    //Show the Won component
    updateGameWon() {
      this.gamesWon++;
      this.gameWonCheck = true;
    },
    updateGameReset() {
      this.getWord();  
    },
    getWord() {
      //Reset all the game variables
       this.gameLostCheck = false;
       this.gameWonCheck = false;
       this.data = null;
       this.loading = true;   
       var options = {
        method: 'GET',
        url: 'https://wordsapiv1.p.rapidapi.com/words/',
        params: {random: 'true', lettersMax: '8', lettersMinimum: '5', },
        headers: {
          'x-rapidapi-key': 'a75432b58bmsh83ec6f966b32c26p1135c6jsn63dc0597d05b',
          'x-rapidapi-host': 'wordsapiv1.p.rapidapi.com'
        }
      };
      //Get a word
      axios.request(options).then((response) => {
        //If the response contains spaces, hypens etc get another word
        if(!response.data.word.match(/^[a-z]+$/)) {
          this.getWord();
        } else {
          this.data = response.data;
          this.loading = false;
        }
      }).catch(function (error) {
          //If an error occours, try again
          this.getWord();
          console.error(error);
      });
  }
}}

</script>

<style>

#app {
  font-family: 'Alegreya', serif;
  -webkit-font-smoothing: antialiased;
  text-transform: uppercase;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #181818;

}

body {
  margin: 0;
  background: #F6F8F8;
}

#won, #loss {
  z-index: 999;
}

.endgame-container {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  align-items: center;
  justify-content: center;
  display: flex;
  color: #fff;
}

button {
    background: #11998e;  /* fallback for old browsers */
    background: -webkit-linear-gradient(350deg, #38ef7d, #11998e);  /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(350deg , #38ef7d, #11998e); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
    border:0;
    padding:10px;
    color: 181818;
    border-radius: 10px;
    transition: all ease-in-out .5s;
    box-shadow: 0 0 15px 0px rgb(0 0 0 / 30%);
        border-bottom: 4px solid #11998e;
}

button:hover {
    background: #11998e;  /* fallback for old browsers */
    background: -webkit-linear-gradient(-350deg, #38ef7d, #11998e);  /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(-350deg , #38ef7d, #11998e); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}

</style>
