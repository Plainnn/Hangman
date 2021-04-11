<template>
  <div>
    {{wordToGuess}}
      <div v-for="(letters, index) in wordToGuess" :key="index" class="letters">
        _
      </div>
      <div v-for="(guesses, index) in previousLetters" :key="index + 10">
        {{guesses}}
      </div>
  </div>
</template>

<script>
export default {
  name: "WordToGuess",
  props: ["words", 'guessedLetter'],
  data() {
      return {
        wordToGuess: null,
        previousLetters: [],
        newWord: null,
        
      }
  },
  mounted() {
      this.$on('guessedLetter', this.guessedLetter)
  },
  methods: {
      randomWord() {
          this.wordToGuess = this.words[Math.floor(Math.random() * this.words.length)];
      },
      guessedLetters(letter) {
        console.log(letter);
      },
      fillInWordWithLetter(letter, word) {
        console.log(letter)
        console.log(word)
        this.newWord = word.toLowerCase().split('').map(l =>  {
          if (l === letter.toLowerCase()) {
            return l.toUpperCase()
          }
          return '_'
        }).join(' ')
      }
  },
  watch: {
  guessedLetter: {
    immediate: true, 
    handler () {
      this.previousLetters.push(this.guessedLetter);
      this.fillInWordWithLetter(this.previousLetters[this.previousLetters.length - 1].letter, this.wordToGuess);
    }
  }
}
};
</script>

<style>
.letters {
  display: inline-block;
  margin: 1em;
}
</style>