<template>
  <div>
    <nuxt-link to="/jokes">Back to Jokes</nuxt-link>
    <h2>{{this.joke.length > 0 ? this.joke : "Loading..."}}</h2>
    <hr />
    <small>Joke ID: {{$route.params.id}}</small>
  </div>
</template>

<script>
import axios from "axios";

export default {
  async created() {
    try {
      const config = {
        headers: {
          Accept: "application/json"
        }
      };

      const res = await axios.get(
        `https://icanhazdadjoke.com/j/${this.$route.params.id}`,
        config
      );
      this.joke = res.data.joke;
    } catch ({ message }) {
      console.log(message);
    }
  },
  data() {
    return {
      joke: {}
    };
  }
  // head() {
  //   return {
  //     title: "this.joke",
  //     meta: [
  //       {
  //         hid: "description",
  //         name: "description",
  //         content: "Best place for corny dad jokes"
  //       }
  //     ]
  //   };
  // }
};
</script>

<style>
</style>