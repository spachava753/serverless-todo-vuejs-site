<template>
  <v-layout row justify-end>
    <v-flex xs12 sm6 offset-sm3>
      <div v-for="todo in todoList" :key="todo.Id">
        <v-card hover>
          <v-card-title primary-title>
            <div>
              <h3 class="headline mb-0">{{ todo.Title }}</h3>
              <div>{{ todo.Description }}</div>
            </div>
          </v-card-title>
          <v-card-actions>
            <v-btn flat color="error" @click="deleteItem(todo.Id)">Delete</v-btn>
          </v-card-actions>
        </v-card>
      </div>
    </v-flex>
    <v-dialog v-model="dialog" persistent max-width="600px">
      <template v-slot:activator="{ on }">
        <!-- <v-btn color="primary" dark v-on="on">Open Dialog</v-btn> -->
        <v-flex xs12 sm12 md6>
          <v-btn fab color="orange" v-on="on" absolute bottom right>
            <v-icon>add</v-icon>
          </v-btn>
        </v-flex>
      </template>
      <v-card>
        <v-card-title>
          <span class="headline">Add a new Todo</span>
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout justify-end column>
              <v-flex xs12 sm6 md4>
                <v-text-field label="Title*" required v-model="titleInput"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-textarea label="Description" required bottom v-model="descInput"></v-textarea>
              </v-flex>
            </v-layout>
          </v-container>
          <small>*indicates required field</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" flat @click="dialog = false">Close</v-btn>
          <v-btn
            color="blue darken-1"
            flat
            @click="dialog = false"
            v-on:click="createItem(titleInput, descInput)"
          >Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-layout>
</template>

<script>
import { log } from "util";
import axios from "axios";

export default {
  data() {
    return {
      todoList: [],
      dialog: false,
      titleInput: "",
      descInput: ""
    };
  },
  created() {
    log("Created!!!");
    axios
      .get("https://pzsvbhabdl.execute-api.us-east-1.amazonaws.com/dev/list")
      .then(response => (this.todoList = response.data));
  },
  methods: {
    fetchList: function() {
      axios
        .get("https://pzsvbhabdl.execute-api.us-east-1.amazonaws.com/dev/list")
        .then(response => (this.todoList = response.data));
    },
    deleteItem: function(id) {
      log("Called deleteItem()");
      log("id is ", id);

      axios
        .delete(
          "https://pzsvbhabdl.execute-api.us-east-1.amazonaws.com/dev/delete/" +
            id
        )
        .then(() => this.fetchList());
    },
    createItem: function(titleInput, descInput) {
      log("createItem called");
      log("title: ", titleInput);
      log("description: ", descInput);
      axios
        .put(
          "https://pzsvbhabdl.execute-api.us-east-1.amazonaws.com/dev/create",
          {
            Title: titleInput,
            Description: descInput
          }
        )
        .then(() => {
          this.fetchList();
        });
      this.titleInput = "";
      this.descInput = "";
    }
  }
};
</script>