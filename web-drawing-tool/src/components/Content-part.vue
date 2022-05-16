<template>
  <div class = "wrap">
    <Menu_left/>
    <v-container>
      <canvas id = "canvas" class ="canvas" ref="can" width="900" height="600"></canvas>
    </v-container>
    <Menu_right/>
  </div>
</template>

<script>


import Menu_left from './Menu-left.vue';
import Menu_right from './Menu-right.vue';
import {fabric} from "fabric"

export default {
  name: 'Content-part',
  props: {
    new_canvas_width: {type:Number, default:900}
  },

  components: {
    Menu_left,
    Menu_right,
  },

  mounted() {
    const ref = this.$refs.can;
    let canvas = new fabric.Canvas(ref , { isDrawingMode: true});
    canvas.add();
  },
  
  watch: {
    'new_canvas_width': function(){
      alert(this.new_canvas_width);
      alert(document.getElementById("canvas").style.width);
      this.canvas_width = this.new_canvas_width;
      alert(this.canvas_width);
      document.getElementById("canvas").style.width = this.canvas_width;
      alert(document.getElementById("canvas").style.width);
    },

  },
  data(){
    return {
      canvas_width: null,
    }
  },
/*
  method: {
    changeSize() {
      alert("실행");
      document.getElementById("canvas").style.width = this.canvas_width;
    }
  }
  */
};

</script>

<style scoped>
div {
  flex: 3;
  background-color: #E0E0E0;
}
.canvas {
  width: 900;
  background-color: white;

}
</style>>