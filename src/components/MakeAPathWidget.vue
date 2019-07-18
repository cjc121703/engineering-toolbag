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
            :configPoint="configPoint"
            :lines="lines"
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
          configPoint:{
                x: this.startX,
                y: this.startY,
                width: 10,
                height: 10,
                fill: "red"
          },
          lines: [],
          nextX: 0,
          nextY:  0

      }
    },
    methods:{
        submitStartPosition : function() {
          this.configPoint = {
                x: parseInt(this.startX),
                y: parseInt(this.startY),
                width: 10,
                height: 10,
                fill: "red"
          };
          this.startPointSubmitted = true;
        },
        clearStartPosition : function() {
            this.startPointSubmitted = false ;  
        },
        addLines : function(){
            var lineXStart = 0;
            var lineYStart = 0;
            if(this.lines.length === 0){
                lineXStart = this.startX,
                lineYStart = this.startY
            }
            this.lines.push(
            {
                x: 0,
                y: 0,
                points: [lineXStart,lineYStart,this.nextX, this.nextY],
                stroke: 'black'
            })
        }
    },
    created() {
    }
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