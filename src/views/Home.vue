<template>
    <v-container grid-list-xs fluid>
        <v-flex md6 offset-md3>
            <v-card>
                <v-layout row wrap>
                    <v-flex xs12 title text-xs-center>
                        Welcome to the beta site for engineering tools.
                    </v-flex>
                    <v-flex xs12 text-xs-center>
                        Sign in!
                    </v-flex>
                    <v-flex xs12 offset-md1>
                        <v-layout row wrap>
                            <v-flex xs12 md2>
                                <label for="userIdSignIn">User Name:</label>
                            </v-flex>
                            <v-flex xs12 md9>
                                <input id="userIdSignIn" placeholder="User Name">
                            </v-flex>
                        </v-layout>
                    </v-flex>
                    <v-flex xs12 offset-md1>
                        <v-layout row wrap>
                            <v-flex xs12 md2>
                                <label for="passwordSignIn">Password:</label>
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
    </v-container>
</template>
<script>
  export default {
    data () {
      return {
        dialog: false
      }
    }
  }
</script>
<style>
    .myFont{
        font-family: "Karla"
    }
</style>