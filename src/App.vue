<template>
  <v-layout>
    <home/>
    <happy-dog-page-error/>
  </v-layout>
</template>

<script>
import Home from "./views/Home"

export default {
  name: 'App',
  components: {
    Home

  },
  data () {
    return {
      //
    }
  }
}
</script>
