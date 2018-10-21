<template>
  <v-app dark>
    <v-toolbar app>
      <v-toolbar-title class="headline">
        <span>weekly.green</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>

    <v-content>
      <Home/>
    </v-content>
  </v-app>
</template>

<script>
import Home from './views/Home'

export default {
  name: 'App',
  components: {
    Home
  }
}
</script>
