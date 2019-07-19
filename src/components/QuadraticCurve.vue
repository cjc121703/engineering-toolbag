<template>
        <v-shape :config="{
        sceneFunc: function(context, shape) {
          context.beginPath();
          context.moveTo(curve.startX, curve.startY);
          context.quadraticCurveTo(curve.curvePointX, curve.curvePointY, curve.endX, curve.endY);

          // special Konva.js method
            context.setAttr('strokeStyle', 'red');
            context.setAttr('lineWidth', 4);
            context.stroke();
        },
     
      }"/>

</template>
<script>
    export default {
        name: 'QuadCurve',
        props:[
            'curve'
        ]
    }
</script>