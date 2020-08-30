<template>
  <div>
    <ul v-if="!loading && pokemonLocationDetails.length > 0">
      <li
        v-for="location in pokemonLocationDetails"
        :key="location.location_area.name"
      >
        {{ location.location_area.name }}
      </li>
    </ul>
    <div v-if="!loading && pokemonLocationDetails.length === 0">
      This Pokémon can't be catched anywhere. It's an evolution of another
      Pokémon or very rare.
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "LocationInfo",
  props: {
    url: String
  },
  data() {
    return {
      pokemonLocationDetails: {},
      loading: false
    };
  },
  created: function() {
    this.loading = true;
    axios
      .get(this.url)
      .then(
        response => (this.pokemonLocationDetails = response.data),
        (this.loading = false)
      )
      .catch(() => (this.loading = false));
  }
};
</script>

<style></style>
