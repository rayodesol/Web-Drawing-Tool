<template>
  <div class = "wrap">
    <Menu_left @symbolClick="drawSymbol"/>
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
let clipboard = null;

export default {
  name: "Content-part",

  components: {
    Menu_left,
    Menu_right,
  },

  mounted() {
    const ref = this.$refs.can;
    canvas = new fabric.Canvas(ref, { isDrawingMode: false });
    canvas.add();
  },

  data: () => ({

  }),

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

    drawSymbol(image){
      console.log(image);
      fabric.loadSVGFromURL(image, (objects) => {
        var obj = fabric.util.groupSVGElements(objects)
        canvas.add(obj)
      });
      canvas.renderAll();
    },

    cutSymbol(){
      canvas.getActiveObject().clone(function(cloned) {
        clipboard = cloned;
      });
      var selected = canvas.getActiveObjects(),
      selGroup = new fabric.ActiveSelection(selected, {
        canvas: canvas
      });
      selGroup.forEachObject(function(obj) {
        canvas.remove(obj);
      });
      canvas.renderAll();
    },
    
    copySymbol(){
      canvas.getActiveObject().clone(function(cloned) {
        clipboard = cloned;
      });
    },

    pasteSymbol(){
      // clone again, so you can do multiple copies.
        clipboard.clone(function(clonedObj) {
          canvas.discardActiveObject();
          clonedObj.set({
            left: clonedObj.left + 10,
            top: clonedObj.top + 10,
            evented: true,
          });
          if (clonedObj.type === 'activeSelection') {
              // active selection needs a reference to the canvas.
              clonedObj.canvas = canvas;
              clonedObj.forEachObject(function (obj) {
                  canvas.add(obj);
              });
              // this should solve the unselectability
              clonedObj.setCoords();
          } else {
            canvas.add(clonedObj);
          }
          canvas.setActiveObject(clonedObj);
          canvas.requestRenderAll();
      });
    },

    deleteSymbol(){
      var selected = canvas.getActiveObjects(),
      selGroup = new fabric.ActiveSelection(selected, {
        canvas: canvas
      });

      if (selGroup){
        if (confirm('선택된 객체를 삭제할까요?')) {
          selGroup.forEachObject(function(obj) {
            canvas.remove(obj);
          });
        }
      }else{
        return false;
      }
      canvas.renderAll();
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
