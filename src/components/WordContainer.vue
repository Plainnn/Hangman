<template>
  <div>
      <section class="word-to-guess">
          {{this.word}}
          {{this.wordStatus}}
      </section>
      <section class="letters-so-far">

      </section>
      <section class="word-so-far">

      </section>
      <section class="letter-container">
          <div v-for="(letter, index) in letters" :key="index" @click="letterPressed(letter)" class="letters">
              {{letter}}
          </div>
      </section>
      <section class="mistakes">
      </section>
  </div>
</template>

<script>
export default {
    name: 'WordContainer',
    props: ['word'],
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
    methods: {
        letterPressed(letters) {
            //Check if the letter is in the guessedLetters array, if not, add it
            this.guessedLetters.indexOf(letters) === -1 ? this.guessedLetters.push(letters) : null;
            //Split the word into an array
            let wordArray = this.word.split('');
            //Check if the letter is in the word
            if(wordArray.indexOf(letters) >= 0) {
                  //Update the word status if the letter is in the word, if it is display the letter, else show an underscore.
                  this.wordStatus = this.word.split('').map(letter => (this.guessedLetters.indexOf(letter) >= 0 ? letter : " _ ")).join('');
                  this.checkIfWon();
            } else {
                //Add a mistake to the count
                this.mistakesMade++;
                this.checkIfLost();
            }
        },
        checkIfLost() {
            if(this.mistakesMade === 6) {
                this.$emit('gameLostEvent', this.mistakesMade)
            } else {
                this.$emit('mistakeMade', this.mistakesMade)
            }
        },
        checkIfWon() {
            if(this.wordStatus === this.word) {
                this.$emit('gameWonEvent', this.word)
            }
        }
    },
}
</script>

<style>
.letters {
  display: inline-block;
  margin: 0.25em;
  background: red;
  padding: 10px;
  border-radius: 5px;
  text-transform: uppercase;

}
</style>