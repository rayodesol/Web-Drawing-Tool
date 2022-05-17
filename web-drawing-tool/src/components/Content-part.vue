<template>
  <div class = "wrap">
    <Menu_left/>
      <v-container>
      <canvas class="canvas" ref="can" width="900" height="600"></canvas>
      <v-btn @click = "mode_change">모드변경</v-btn>
      </v-container>
    <Menu_right/>
  </div>
</template>

<script>
import { fabric } from "fabric";
import { data } from "../data";
import Menu_left from './Menu-left.vue';
import Menu_right from './Menu-right.vue';
let canvas;

export default {
  name: "Content-part",

  components: {
    Menu_left,
    Menu_right,
  },

  mounted() {
    const ref = this.$refs.can;
    canvas = new fabric.Canvas(ref, { isDrawingMode: true });
    canvas.add();
  },

  methods: {
    mode_change(){
      canvas.isDrawingMode = !canvas.isDrawingMode;
      //alert(canvas.isDrawingMode);
      canvas.renderAll();
    },
    
    export_to_png(){
      const dataURL = canvas.toDataURL({
        width: canvas.width,
        height: canvas.height,
        left: 0,
        top: 0,
        format: 'png',
      });
      const link = document.createElement('a');
      link.download = 'image.png';
      link.href = dataURL;
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    },

    add_content_to_canvas(content){
      alert('호출됨');
      canvas.add(content);
    },
  },
};

setInterval(() => {
  canvas.setWidth(data.width);
  canvas.setHeight(data.height);
}, 100);
</script>

<style scoped>
div {
  flex: 4;
  background-color: #e0e0e0;
}
.canvas {
  background-color: white;
}
</style>
>
