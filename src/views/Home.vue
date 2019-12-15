<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <p>Name: <input type="text" v-model="newName"></p>
    <p>Address: <input type="text" v-model="newAddress"></p>
    <button v-on:click="addPlace()">Add Place</button>


    <div v-for="place in places">
      <p>Name: {{ place.name }}</p>
      <p>Address: {{ place.address }}</p>
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      places: [],
      newName: "",
      newAddress: ""
    };
  },
  created: function() {
    console.log("in created");
    axios.get("/api/places").then(response => {
      console.log(response.data);
      this.places = response.data;
    });
  },
  methods: {
    addPlace: function() {
      console.log("adding place");

      var params = {
        name: this.newName,
        address: this.newAddress
      };

      axios.post("/api/places", params).then(response => {
        console.log(response.data);
        this.newName = "";
        this.newAddress = "";
      });
    }
  }
};
</script>

