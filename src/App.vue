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
      <v-card flat tile class="lighten-1 text-xs-center">
        <v-flex xs10 offset-xs1>
          <v-card-text>This is my CSP project. It was made by me for the Create task, using different algorthims and systems. I wrote Golang serverless functions on AWS using AWS Lambda, and served the API using AWS Api Gateway. The front end is made with Vue and Vuetify components.</v-card-text>
        </v-flex>
        <v-divider></v-divider>
        <v-card-text>@2019</v-card-text>
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
