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
        </v-flex>
        <v-flex xs6 text-xs-center offset-lg3>
        <MakeAPath>
        </MakeAPath>
        <pack-chart
            :tweetData = loadData
        />
        </v-flex>
    </v-container>
</template>
<script>
import MakeAPath from "@/components/MakeAPathWidget"
import PackChart from "@/components/Chart"
import * as d3 from "d3";

  export default {
    components: {
        MakeAPath,
        PackChart
    },
    data () {
      return {
          loadData: []
      }
    },
    mounted(){
        console.log("App Loaded");
        this.fetchData();
    },
    methods:{
        async fetchData() {
            let data = await d3.json("./tweets.json");
            this.loadData = data;
            console.log("data loaded");
        }
    },
    created() {
    }
  }
</script>
<style>
</style>