<template>
  <v-app dark>
    <v-toolbar app>
      <v-toolbar-side-icon></v-toolbar-side-icon>
      <v-toolbar-title class="headline">
        <span>weekly.<span style="color: green">green</span></span>
      </v-toolbar-title>
      <v-spacer></v-spacer>

      <v-toolbar-items>
        <v-btn flat href="https://weekly-green.herokuapp.com/debug/yodlee">Yodlee Setup</v-btn>
      </v-toolbar-items>
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
