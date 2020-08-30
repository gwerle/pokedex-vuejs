<template>
  <div>
    <img
      alt="Snorlax With Laptop"
      src="../assets/HeaderImage.jpeg"
      height="250px"
      width="250px"
    />
    <h1 id="title">Find more informations about your favorite Pokemon!</h1>
    <SearchField @textSubmit="onSubmitValue" :fieldError="fieldError" />
    <div id="flex-div">
      <div v-for="poke in pokemons" :key="poke.name">
        <Pokemon :name="poke.name" :url="poke.url" />
      </div>
    </div>
  </div>
</template>

<script>
import SearchField from "@/components/SearchField.vue";
import Pokemon from "@/components/Pokemon.vue";
import axios from "axios";

export default {
  name: "Home",
  components: {
    SearchField,
    Pokemon
  },
  data() {
    return {
      allPokemons: [],
      pokemons: [],
      searchTextValue: "",
      fieldError: {
        visible: false,
        message: "saasfda"
      }
    };
  },
  created: function() {
    this.getAllPokemonValues();
  },

  methods: {
    onSubmitValue(value) {
      if (value.length <= 2) {
        this.fieldError = {
          visible: true,
          message: "3 characters minimum"
        };
      } else {
        this.fieldError = {
          visible: false,
          message: ""
        };
        this.pokemons = this.allPokemons.filter(pokemon =>
          pokemon.name.includes(value.toLowerCase())
        );
      }
    },
    getAllPokemonValues() {
      axios
        .get("https://pokeapi.co/api/v2/pokemon?limit=200&offset=0")
        .then(response => (this.allPokemons = response.data.results));
    }
  }
};
</script>

<style lang="scss" scoped>
#title {
  font-size: 24px;
}
#flex-div {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  flex-wrap: wrap;
  margin-top: 10px;
}
</style>
