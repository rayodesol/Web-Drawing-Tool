<template>
  <div class = "wrap">
    <Menu_left/>
    <v-container>
      <canvas id = "canvas" class ="canvas" ref="can"
      width="900px" height="600px"></canvas>
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
    new_canvas_width: {type:String, default:'900px'},
    new_canvas_height: {type:String, default:'600px'}
  },

  components: {
    Menu_left,
    Menu_right,
  },

  mounted() {
    const ref = this.$refs.can;
    let canvas = new fabric.Canvas(ref , { isDrawingMode: true});
    canvas.add();
    this.canvas.addEventListener('')
  },
  
  watch: {
    'new_canvas_width': function(){
      //alert(this.new_canvas_width);
      this.canvas_width = this.new_canvas_width + "px";
      let canvas = document.getElementById("canvas");
      canvas.style.width = this.canvas_width;
    },

    'new_canvas_height': function(){
      //alert(this.new_canvas_height);
      this.canvas_height = this.new_canvas_height + "px";
      let canvas = document.getElementById("canvas");
      canvas.style.height = this.canvas_height;
    }
  },
  data(){
    return {
      canvas_width: '900px',
      canvas_height: '600px'
    }
  },

  /*method: {
    changeSize() {
      alert("실행", this.canvas_width);
      let size = document.getElementById("canvas");
      size.style.width = this.canvas_width;
    }
  }*/

};

</script>

<style scoped>
div {
  flex: 3;
  background-color: #E0E0E0;
}
#canvas {
  width: 900px;
  height: 600px;
  background-color: white;

}
</style>>