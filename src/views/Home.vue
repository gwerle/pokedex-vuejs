<template>
  <div>
    <img
      alt="Snorlax With Laptop"
      src="../assets/HeaderImage.jpeg"
      height="250px"
      width="250px"
    />
    <h1 id="title">Find more informations about your favorite Pokemon!</h1>
    <SearchField @textSubmit="onSubmitValue" />
    <div v-for="(poke, index) in pokemons" :key="index">
      <h1>{{ poke.name }}</h1>
    </div>
  </div>
</template>

<script>
import SearchField from "@/components/SearchField.vue";
import axios from "axios";

export default {
  name: "Home",
  components: {
    SearchField
  },
  data() {
    return {
      pokemons: [],
      searchTextValue: ""
    };
  },
  created: function() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=200&offset=0")
      .then(response => (this.pokemons = response.data.results));
  },
  methods: {
    onSubmitValue(value) {
      this.searchTextValue = value;
    }
  }
};
</script>

<style lang="scss" scoped>
#title {
  font-size: 24px;
}
</style>
