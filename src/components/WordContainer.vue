<template>
  <div>
      <section class="word-to-guess">
          <h1 class="word">{{wordStatus}}</h1>
      </section>
      <section class="mistakes-made">
        <h2 v-if="mistakesMadeComputed == 0">👇 Welcome, click a letter to start! 👇</h2>
        <h2 v-else>🛑 You have made {{mistakesMade}} / 6 wrong moves 🛑</h2>
      </section>
      <section class="letter-container">
          <div v-for="(letter, index) in letters" :key="index" @click="letterPressed(letter, $event);" class="letters">
              {{letter}}
          </div>
      </section>
  </div>
</template> 

<script>
export default {
    name: 'WordContainer',
    props: ['word'],
    mounted() {
        //Replace all the letters with underscores by checking the word against the guessedLetter array
        this.wordStatus = this.word.split('').map(letter => (this.guessedLetters.indexOf(letter) >= 0 ? letter : " _ ")).join('');
    },
    data() {
        return {
            guessedLetters: [],
            wordStatus: null,
            mistakesMade: 0,
            letters: [
                        "a",
                        "b",
                        "c",
                        "d",
                        "e",
                        "f",
                        "g",
                        "h",
                        "i",
                        "j",
                        "k",
                        "l",
                        "m",
                        "n",
                        "o",
                        "p",
                        "q",
                        "r",
                        "s",
                        "t",
                        "u",
                        "v",
                        "w",
                        "x",
                        "y",
                        "z"
            ],
        }
    },
    computed: {
        //If mistakes made is greater than or equal to 0, return it, else, return null.
        mistakesMadeComputed() {
            return this.mistakesMade >= 0 ? this.mistakesMade : null
        }
    },
    methods: {
        letterPressed(letters, element) {
            //Check if the letter is in the guessedLetters array, if not, add it
            this.guessedLetters.indexOf(letters) === -1 ? this.guessedLetters.push(letters) : null;
            //Split the word into an array
            let wordArray = this.word.split('');
            //Check if the letter is in the word
            if(wordArray.indexOf(letters) >= 0) {
                  //Update the word status if the letter is in the word, if it is display the letter, else show an underscore.
                  this.wordStatus = this.word.split('').map(letter => (this.guessedLetters.indexOf(letter) >= 0 ? letter : " _ ")).join('');
                  this.checkIfWon();
                  this.highlightGuessedLetter(element, true);
            } else {
                //Add a mistake to the count
                this.mistakesMade++;
                this.checkIfLost();
                this.highlightGuessedLetter(element, false);
            }
        },
        checkIfLost() {
            //Emit a mistake made event, this is how I draw the hangman.
            this.$emit('mistakeMade', this.mistakesMade)
            //Emit a gameLost event on 6 incorrrect guesses.
            if(this.mistakesMade === 6) {
                this.$emit('gameLostEvent', this.mistakesMade)
            } 
        },
        checkIfWon() {
            //If the wordStatus is equal too the word, emit a gameWon event (shows Won.vue)
            this.wordStatus == this.word ? this.$emit('gameWonEvent', this.word) : null
        },
        //Add a class to the letter pressed.
        highlightGuessedLetter(element, wasCorrect){
            if(wasCorrect) {
                element.target.classList.toggle('correct');
            } else {
                element.target.classList.toggle('incorrect');
            }
        }
    },
}
</script>

<style>

.letter-container, .mistake-container {
    display: flex;
    align-items: center;
    display: flex;
    padding-top:10px;
    justify-content:space-evenly;
    width: 40%;
    flex-direction: row;
    margin: 0 auto;
    align-items: center;
    flex-wrap: wrap;
    z-index: 0;
}

.mistakes-made{
    padding-top: 1em;
    text-transform:initial;
}

.letters {
    background: #11998e;  /* fallback for old browsers */
    background: -webkit-linear-gradient(350deg, #38ef7d, #11998e);  /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(350deg , #38ef7d, #11998e); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
    border-radius: 5px;
    text-transform: uppercase;
    box-shadow: 0 0 15px 0px rgb(0 0 0 / 30%);
    transition: all ease-in-out .5s;
    font-family: 'Alegreya', serif;
    font-size: 1.75rem;
    width:40px;
    height:40px;
    align-items: center;
    line-height: 40px;
    display: inline-block;
    position: relative;
    margin: .25em;
    border-bottom: 4px solid #11998e;
}

.letters:hover {
    margin-top: -15px;
}

.correct::before, .incorrect::before {
    font-family: "Font Awesome 5 Free";
    font-weight: 900;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 60%);
    border-bottom: 4px solid transparent;
    border-radius: 5px;
    margin-top: 2px;
}

.correct::before {
    content: "✔️";
    color: #18ce40;
    border-bottom-color: #18ce40;
}

.incorrect::before{
    content: "❌";
    color: #f10909;
    border-bottom-color: #f10909;
}

.word {
    margin-top: 20px;
    letter-spacing: 10px;
    margin-bottom: 0;
}

@media screen and (max-width: 39.9375em) {
  .letter-container {
      width: 90%;
  }

  .mistakes-made {
      font-size:.75em;
  }
}
</style>