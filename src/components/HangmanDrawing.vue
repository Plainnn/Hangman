<template>
  <div>
    {{mistakesMade}}
    <br>
    <canvas id="stickman" width="500" height="500">


    </canvas>
  </div>
</template>

<script>
export default {
  name: "HangmanDrawing",
  props:['mistakesMade'],
  mounted() {
      let canvas = document.getElementById("stickman");
      let context = canvas.getContext('2d');
      context.strokeStyle = "black";
      context.lineWidth = 5;

      //Bottom Frame Line
      context.beginPath();
      context.moveTo(0, 500);
      context.lineTo(500, 500);
      context.stroke();

      //Vertical Frame Line
      context.beginPath();
      context.moveTo(450, 150);
      context.lineTo(450, 500);
      context.stroke();

      //Horizontal Frame Line
      context.beginPath();
      context.moveTo(450, 150);
      context.lineTo(300, 150);
      context.stroke();

      //Noose
      context.beginPath();
      context.moveTo(300, 190);
      context.lineTo(300, 150);
      context.stroke();
  },
  watch: {
    mistakesMade() {
      let canvas = document.getElementById("stickman");
      let context = canvas.getContext('2d');
      context.fillStyle = "#181818";

        switch (this.mistakesMade) {
        case 1:
          //Head
          context.beginPath();
          context.arc(300, 210, 20, 0, 2 * Math.PI);
          context.stroke();
          break;
        case 2:
          //Body Line
          context.beginPath();
          context.moveTo(300, 230);
          context.lineTo(300, 350);
          context.stroke();
          break;
        case 3:
          //Left Arm
          context.beginPath();
          context.moveTo(300, 250);
          context.lineTo(250, 300);
          context.stroke();
          break;
        case 4:
          //Right Arm
          context.beginPath();
          context.moveTo(300, 250);
          context.lineTo(350, 300);
          context.stroke();
          break;
        case 5:
          //Left Leg
          context.beginPath();
          context.moveTo(300, 348);
          context.lineTo(250, 400);
          context.stroke();
          break;
        case 6:
          //Right Leg
          context.beginPath();
          context.moveTo(300, 348);
          context.lineTo(350, 400);
          context.stroke();
          break;
        default:
          break;
      }
    }
  }
};
</script>

<style>
</style>