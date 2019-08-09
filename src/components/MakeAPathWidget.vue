<template>            
    <v-card>
        <v-layout row wrap>
            <v-flex xs3>
                <div class="pointInputs">
                    <label 
                    for="startX">Starting X Point</label>                
                    <input 
                    v-if="!startPointSubmitted"
                    id="startX" v-model="startX" type="number" min="0" >
                    <div v-if="startPointSubmitted">
                        {{startX}}
                    </div>
                </div>
            </v-flex>
            <v-flex xs1>
            </v-flex> 
            <v-flex xs3>
                <div class="pointInputs">                        
                    <label 
                    for="startY">Starting Y Point</label>                
                    <input 
                    v-if="!startPointSubmitted"
                    id="startY" 
                    v-model="startY" 
                    type="number" min="0">
                    <div v-if="startPointSubmitted">
                        {{startY}}
                    </div>
                </div>
            </v-flex>
            <v-flex xs1>
            </v-flex>
            <v-flex xs1>
                <v-btn 
                    v-on:click="submitStartPosition()"
                    flat
                    icon
                    color = "green"
                    :disabled="startPointSubmitted"
                    >
                        <v-icon>check_circle_outline</v-icon>
                </v-btn>
            </v-flex>
            <v-flex xs1>
                <v-btn 
                    v-if="startPointSubmitted" 
                    v-on:click="clearStartPosition()"
                    flat
                    icon
                    color="red"
                    >
                        <v-icon>highlight_off</v-icon>
                    </v-btn>                        
            </v-flex>
        </v-layout>
        <v-flex>
            <div v-if="travelPoints.length > 0">
                <div> 
                    X, Y
                </div>
                <div 
                    v-for="(coord, index) in travelPoints"
                    :key="index"
                >
                {{coord.x}},{{coord.y}}
                </div>

            </div>
        </v-flex>
        <v-flex>
            <div v-if="startPointSubmitted">
                <label>Next X</label>
                <input
                    type="number"
                    min="0"
                    v-model="nextX"
                >
                <label>Next Y</label>
                <input
                    type="number"
                    min="0"
                    v-model="nextY"

                >
                <v-btn
                    v-if="!curveIt"
                    flat
                    icon
                    color="blue"
                    v-on:click="curveIt = true"
                >
                    <v-icon>redo</v-icon>
                </v-btn>
            <v-flex xs 5 v-if="curveIt">
                <label
                    v-if="curveIt"
                >
                Curve X
                </label>
                <input
                    v-if="curveIt"
                    type="number"
                    min=0
                    v-model="curveX"
                >
                                <label
                    v-if="curveIt"
                >
                Curve Y
                </label>
                <input
                    v-if="curveIt"
                    type="number"
                    min=0
                    v-model="curveY"
                >
            </v-flex>
                <v-btn 
                    v-on:click="addLines()"
                    flat
                    icon
                    color = "green"
                    >
                        <v-icon>check_circle_outline</v-icon>
                </v-btn>
            </div>
        </v-flex>
        <DrawLinesOnAPicture 
            :imageSrc='field' 
            :imageHeight="fieldHeight" 
            :imageWidth="fieldWidth"
            :points="points"
            :lines="lines"
            :curves="curves"
            :arcs="arcs"
            @clicked="onImageClicked"
        >
        </DrawLinesOnAPicture>
    </v-card>
</template>
<script>
import DrawLinesOnAPicture from "@/components/DrawLinesOnAPicture"

  export default {
    name:"MakeAPath",
    components: {
      DrawLinesOnAPicture
    },
    data () {
      return {
          field: require('@/assets/field.jpg'),
          fieldHeight: 500,
          fieldWidth:500,
          startPointSubmitted: false,
          startX:0,
          startY:0,
          startingPoint:null,
          points: [],
          lines: [],
          curves: [],
          arcs: [],
          nextX: 0,
          nextY:  0,
          curveX: 0,
          curveY: 0,
          curveIt: false,
          travelPoints: []

      }
    },
    methods:{
        submitStartPosition : function() {
          this.startingPoint = {
                x: parseInt(this.startX),
                y: parseInt(this.startY),
                width: 10,
                height: 10,
                fill: "red"
          };
            this.points = [this.startingPoint]
          this.startPointSubmitted = true;
        },
        clearStartPosition : function() {
            this.startPointSubmitted = false ; 
            this.lines = [];
            this.points = []; 
            this.curves = [];
            this.arcs = [];
        },
        addLines : function(){
            var lineXStart = 0;
            var lineYStart = 0;
            if(this.lines.length === 0 && this.curves.length === 0){
                lineXStart = parseInt(this.startX),
                lineYStart = parseInt(this.startY)
                this.travelPoints.push({
                    x: lineXStart,
                    y:lineYStart
                })
            }
            else{
                lineXStart = this.points[this.points.length - 1].x ;
                lineYStart = this.points[this.points.length - 1].y ;
            }
            if(this.curveIt){
                this.curves.push({
                    startX: lineXStart,
                    startY: lineYStart,
                    curvePointX: parseInt(this.curveX),
                    curvePointY: parseInt(this.curveY),
                    endX: parseInt(this.nextX),
                    endY: parseInt(this.nextY)
                });
                this.points.push({
                    x: parseInt(this.curveX),
                    y: parseInt(this.curveY),
                    width: 10,
                    height: 10,
                    fill: "purple"
                })
                this.arcs.push({
                    x: lineXStart - 70,
                    y: lineYStart,
                    innerRadius:70,
                    outerRadius:70,
                    angle:70,
                    fill: 'yellow',
                    stroke: 'black',
                    strokeWidth: 4
                })
            }
            else{
                this.lines.push(
                {
                    x: 0,
                    y: 0,
                    points: [lineXStart,lineYStart,this.nextX, this.nextY],
                    stroke: 'black'
                });
            }
            this.points.push({
                x: this.nextX,
                y: this.nextY,
                width: 10,
                height: 10,
                fill: "red"
            })
            this.travelPoints.push({
                x: parseInt(this.nextX),
                y: parseInt(this.nextY)
            })
            this.curveIt = false;            
        },
        onImageClicked(mousePosition) {
            if(!this.startPointSubmitted){
                this.startX = mousePosition.x;
                this.startY = mousePosition.y;
                this.startingPoint = {
                    x: parseInt(this.startX),
                    y: parseInt(this.startY),
                    width: 10,
                    height: 10,
                    fill: "red"
                };
                this.points = [this.startingPoint]
            }
            else{
                this.nextX = mousePosition.x;
                this.nextY = mousePosition.y;
            }
        }      
    },

  }
</script>
<style>
    input{
        border-bottom:1px solid black;
        width: 100%;
        font-size: 16px;
    }
    .pointInputs{
        padding-left: 10px
    }
</style>