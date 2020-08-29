<template>
  <div>
    <img
      :alt="pokemonInfo.name"
      :src="pokemonInfo.sprites.front_default"
      height="250px"
      width="250px"
    />
    <div>{{ name }}</div>
    <div>{{ url }}</div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Pokemon",
  props: {
    name: String,
    url: String
  },
  data() {
    return {
      pokemonInfo: {}
    };
  },
  created: function() {
    axios.get(this.url).then(resp => (this.pokemonInfo = resp.data));
  }
};
</script>

<style></style>
