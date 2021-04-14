<template>
  <div>
    <canvas id="stickman" width="500" height="500" />
  </div>
</template>

<script>
export default {
  name: "HangmanDrawing",
  props:['mistakesMade'],
  mounted() {
      let canvas = document.getElementById("stickman");
      let context = canvas.getContext('2d');
      context.lineWidth = 10;
      context.lineCap = "round";

      //Bottom Frame Line
      context.beginPath();
      context.moveTo(350, 490);
      context.lineTo(490, 490);
      context.stroke();

      //Vertical Frame Line
      context.beginPath();
      context.moveTo(450, 130);
      context.lineTo(450, 490);
      context.stroke();

      //Horizontal Frame Line
      context.beginPath();
      context.moveTo(450, 150);
      context.lineTo(285, 150);
      context.stroke();

      //Noose
      context.beginPath();
      context.moveTo(300, 190);
      context.lineTo(300, 150);
      context.stroke();
      //Shadowed Body
      context.strokeStyle = "#D1CFCF";
      //Head
      context.beginPath();
      context.arc(300, 225, 30, 0, 2 * Math.PI);
      context.stroke();
      //Body Line
      context.beginPath();
      context.moveTo(300, 260);
      context.lineTo(300, 350);
      context.stroke();
      //Left Arm
      context.beginPath();
      context.moveTo(300, 255);
      context.lineTo(250, 300);
      context.stroke();
      //Right Arm
      context.beginPath();
      context.moveTo(300, 255);
      context.lineTo(350, 300);
      context.stroke();
      //Left Leg
      context.beginPath();
      context.moveTo(300, 348);
      context.lineTo(250, 420);
      context.stroke();
      //Right Leg
      context.beginPath();
      context.moveTo(300, 348);
      context.lineTo(350, 420);
      context.stroke();

  },
  watch: {
    mistakesMade() {
      let canvas = document.getElementById("stickman");
      let context = canvas.getContext('2d');
      context.lineWidth = 10;
      context.lineCap = "round";
      context.strokeStyle = "#181818";
      context.fillStyle = "#181818";

        switch (this.mistakesMade) {
          case 1:
            //Head
            context.beginPath();
            context.arc(300, 225, 30, 0, 2 * Math.PI);
            context.stroke();
          break;
        case 2:
            //Body Line
            context.beginPath();
            context.moveTo(300, 260);
            context.lineTo(300, 350);
            context.stroke();
          break;
        case 3:
          //Left Arm
          context.beginPath();
          context.moveTo(300, 255);
          context.lineTo(250, 300);
          context.stroke();
          break;
        case 4:
          //Right Arm
          context.beginPath();
          context.moveTo(300, 255);
          context.lineTo(350, 300);
          context.stroke();
          break;
        case 5:
          //Left Leg
            context.beginPath();
            context.moveTo(300, 348);
            context.lineTo(250, 420);
            context.stroke();
          break;
        case 6:
          //Right Leg
            context.beginPath();
            context.moveTo(300, 348);
            context.lineTo(350, 420);
            context.stroke();
          break;
        default:
          break;
      }
    }
  }
};
</script>

<style scoped>
canvas {
  margin-top: -100px;
  margin-left: -110px;
}

@media screen and (max-width: 39.9375em) {
  canvas {
    margin-top: 0px;
    width: 70%;
  }
}


</style>