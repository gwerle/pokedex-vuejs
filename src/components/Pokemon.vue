<template>
  <div id="card">
    <div id="card-content">
      <img
        :alt="pokemonInfo.name"
        :src="pokemonInfo.sprites ? pokemonInfo.sprites.front_default : ''"
        height="250px"
        width="250px"
      />
      <div>
        Name: <strong>{{ name }}</strong>
      </div>
      Type(s):
      <ul>
        <li v-for="type in pokemonInfo.types" :key="type.type.name">
          {{ type.type.name }}
        </li>
      </ul>
      Games Available:
      <ul>
        <li v-for="game in pokemonInfo.game_indices" :key="game.gameIndex">
          {{ game.version.name }}
        </li>
      </ul>
      <b-button
        variant="outline-primary"
        title="Where can I catch one of this?"
        v-b-modal="pokemonInfo.name"
      >
        <b-icon icon="geo-alt" scale="1"></b-icon>
      </b-button>
      <b-modal :id="pokemonInfo.name" :title="pokemonInfo.name">
        <LocationInfo :url="pokemonInfo.location_area_encounters" />
      </b-modal>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import LocationInfo from "./LocationInfo";

export default {
  name: "Pokemon",
  components: {
    LocationInfo
  },
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

<style>
#card {
  margin: 10px;
  box-shadow: 0px 3px 3px -2px rgba(0, 0, 0, 0.2),
    0px 3px 4px 0px rgba(0, 0, 0, 0.14), 0px 1px 8px 0px rgba(0, 0, 0, 0.12);
}
#card-content {
  padding: 10px;
  text-align: left;
}
</style>
