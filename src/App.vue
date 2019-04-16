<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span class="font-weight-light">CSP Project</span>
      </v-toolbar-title>
    </v-toolbar>
    <v-content>
      <TodoList/>
    </v-content>

    <v-footer height="auto">
      <v-card flat tile class="text-xs-center shadow" elevation="15" width="100%">
        <v-card-text>This is my CSP project for computer science principles. I built the backend with Golang using AWS Lambda and connected it to AWS Api Gateway to serve my API. The front end is built with Vuejs and Vuetify. Please give me a 5.</v-card-text>

        <v-divider></v-divider>

        <v-card-text class="black--text">
          &copy;2018 —
          <strong>Vuetify</strong>
        </v-card-text>
      </v-card>
    </v-footer>
  </v-app>
</template>

<script>
//import HelloWorld from './components/HelloWorld'
import TodoList from "./components/TodoList";

export default {
  name: "App",
  components: {
    TodoList
  },
  data() {
    return {
      //
    };
  }
};
</script>
