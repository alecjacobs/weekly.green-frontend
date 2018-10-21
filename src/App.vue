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
      <v-layout row justify-center>
        <v-dialog v-model="dialog" width="600px">
          <v-btn slot="activator" color="primary" dark>You're a company. Act like one!</v-btn>
          <v-card>
            <v-card-title>
              <span class="headline">"I'm not a businessman. I'm a business, man." - Jay-Z</span>
            </v-card-title>
            <v-card-text>
              <p>
                <strong>It looks like you drive for Uber.</strong>
              </p>
              <p>
                As a member of the gig economy, you're an independent contractor. This means that you're a <strong>company</strong>, and you should act like one! Let us help you save money by <strong>tracking your business expenses</strong>, like
                <strong>gas</strong>, <strong>car repairs</strong>, <strong>your cell phone plan</strong>, and much more.
              </p>
              <p>
                We can also help you plan for retirement. Open a <a>SEP IRA</a> or sign up for a free EIN from the IRS and
                open a <a>SE 401k</a>.
              </p>
              <p>And did you know that as an independent contractor, the new tax plan lets you write off %20 of your income on your taxes?</p>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="green darken-1" flat="flat" @click="dialog = false">Learn more!</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-layout>

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
