<template>
  <div class = "wrap">
    <Menu_left/>
    <v-container>
      <v-btn @click = "export_to_png">출력</v-btn>
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
    new_canvas_height: {type:String, default:'600px'},
    //export_file_png: {type:Boolean, default: false},
    //export_file_pdf: {type:Boolean, default: false},
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
       //alert(canvas.style.width);
      this.canvas_width = this.new_canvas_width + "px";
      let canvas = document.getElementById("canvas");
      canvas.style.width = this.canvas_width;
      canvas.requestRenderAll();
      delete this.canvas;
    },

    'new_canvas_height': function(){
      //alert(this.new_canvas_height);
      this.canvas_height = this.new_canvas_height + "px";
      let canvas = document.getElementById("canvas");
      canvas.style.height = this.canvas_height;
    },
/*
    'export_file_png': function(){
      alert(this.checking_png);
      if (this.export_file_png == true){
        alert("png로 내보냄");
      }
      alert(this.export_file_png);
    },*/

  },
  data(){
    return {
      canvas_width: '900px',
      canvas_height: '600px',
      canvas: null,
      checking_png: false,
      checking_pdf: false,
      dataURL: document.canvas.toDataURL({
        width: document.canvas.width,
        height: document.canvas.height,
        left: 0,
        top: 0,
        format: 'png',
      }),
      
    }
  },

  method: {
    export_to_png(){
      alert('dd');
      //const link = document.createElement('a');
      //link.download = 'image.png';
      //link.href = this.dataURL;
      //document.body.appendChild(link);
      //link.click();
      //document.body.removeChild(link);
    },
  }

};

</script>

<style scoped>
div {
  flex: 3;
  background-color: #E0E0E0;
}
#canvas {
  background-color: white;

}
</style>>