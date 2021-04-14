<template>
  <div @click="emitLetter(letter)">{{letter}}</div>
</template>

<script>
export default {
  name: "Letters",
  props: ["letter"],
  data(){
    return {
      clickedLetter : null
    }
  },
  methods: {
    //Emit a button press, receive it and show the appropriate class.
    emitLetter(letter){
      this.$emit('letterEvent', {letter: letter})
    }
  }
};
</script>

<style scoped>
.letter-container {
  display: inline-block;
}
</style>