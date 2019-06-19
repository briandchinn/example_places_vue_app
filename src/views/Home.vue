<template>
  <div class="home">

    <div v-for="place in places">
      <h3>Name: {{ place.name }}</h3>
      <h4>Address: {{ place.address }}</h4>
      <hr>
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
      message: "Places App",
      places: [],
      currentRecipe: {},
      errors: []
    };
  },
  created: function() {
    axios.get("/api/places").then(response => {
      this.places = response.data;
      console.log(this.places);
    });
  },
  methods: {
    showRecipe: function(recipe) {
      if (this.currentRecipe === recipe) {
        this.currentRecipe = null;
      } else {
        this.currentRecipe = recipe;
      }
    },
    destroyRecipe: function(recipe) {
      // send an axios delete request to the backend to remove recipe from database
      axios.delete("/api/recipes/" + recipe.id).then(response => {
        console.log("Success!", response.data);
        // find index of recipe in recipes array
        var index = this.recipes.indexOf(recipe);
        // splice recipes array at index
        this.recipes.splice(index, 1);
      });
    }
  }
};
</script>