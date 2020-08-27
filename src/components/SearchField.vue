<template>
  <div id="field-centered">
    <b-input-group>
      <b-form-input
        v-model="text"
        type="text"
        placeholder="Search by name..."
      ></b-form-input>

      <b-input-group-append>
        <b-btn @click="onClickButton()" variant="outline-primary">Submit</b-btn>
      </b-input-group-append>
    </b-input-group>
  </div>
</template>

<script>
export default {
  name: "SearchField",
  data() {
    return {
      text: ""
    };
  },
  methods: {
    onClickButton() {
      this.$emit("textSubmit", this.text);
    }
  }
};
</script>

<style scoped lang="scss">
#field-centered {
  margin-top: 30px;
  max-width: 500px;
  margin-left: auto;
  margin-right: auto;
}
</style>
