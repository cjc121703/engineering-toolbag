<template>
  <v-layout>
    <home/>
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
