<template>
    <v-container grid-list-xs fluid>
        <v-flex lg4 md6 offset-lg4 offset-md3>
            <v-card>
                <v-layout row wrap>
                    <v-flex xs12 title text-xs-center>
                        Welcome to the beta site for engineering tools.
                    </v-flex>
                    <v-flex class="subheading" xs12 text-xs-center>
                        Sign in!
                    </v-flex>
                    <v-flex xs12 offset-md1 >
                        <v-layout row wrap>
                            <v-flex xs12 md2>
                                <label class="body-1 font-weight-bold" for="userIdSignIn">User Name:</label>
                            </v-flex>
                            <v-flex xs12 md9>
                                <input id="userIdSignIn" placeholder="User Name">
                            </v-flex>
                        </v-layout>
                    </v-flex>
                    <v-flex xs12 offset-md1>
                        <v-layout row wrap>
                            <v-flex xs12 md2>
                                <label class="body-1 font-weight-bold" for="passwordSignIn">Password:</label>
                            </v-flex>
                            <v-flex xs12 md9>
                                <input type="password" placeholder="Password">
                            </v-flex>
                        </v-layout>
                    </v-flex>
                    <v-flex text-xs-center>
                        New User? Sign Up!
                    </v-flex>
                </v-layout>
            </v-card>
            <v-card>
                <v-layout row wrap>
                    <v-flex xs3>
                        <div class="pointInputs">
                            <label for="startX">Starting X Point</label>                
                            <input id="startX" v-model="startX" type="number" min="0" >
                        </div>
                    </v-flex>
                    <v-flex xs1>
                    </v-flex> 
                    <v-flex xs3>
                        <div class="pointInputs">                        
                            <label for="startY">Starting Y Point</label>                
                            <input id="startY" v-model="startY" type="number" min="0">
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
                            >
                                <v-icon>check_circle_outline</v-icon>
                            </v-btn>
                    </v-flex>
                    <v-flex xs1>
                        <v-btn 
                            v-if="startPointSumbitted" 
                            v-on:click="clearStartPosition()"
                            flat
                            icon
                            color="red"
                            >
                                <v-icon>highlight_off</v-icon>
                            </v-btn>                        
                    </v-flex>
                </v-layout>
                <DrawLinesOnAPicture 
                    :imageSrc='field' 
                    :imageHeight="fieldHeight" 
                    :imageWidth="fieldWidth"
                    :configPoint="configPoint"
                >
                </DrawLinesOnAPicture>
            </v-card>
        </v-flex>
    </v-container>
</template>
<script>
import DrawLinesOnAPicture from "@/components/DrawLinesOnAPicture"

  export default {
    components: {
      DrawLinesOnAPicture
    },
    data () {
      return {
          field: require('@/assets/field.jpg'),
          fieldHeight: 500,
          fieldWidth:500,
          startPointSumbitted: false,
          startX:0,
          startY:0,
          configPoint:{
                x: this.startX,
                y: this.startY,
                width: 10,
                height: 10,
                fill: "red"
          }

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
          this.startPointSumbitted = true;
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