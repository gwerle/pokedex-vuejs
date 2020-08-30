<template>
  <div id="field-centered">
    <b-input-group>
      <b-form-input
        v-model="text"
        type="search"
        placeholder="Search by name..."
        v-on:keyup.enter="onClickButton()"
        :state="this.fieldError.visible ? false : null"
      ></b-form-input>

      <b-input-group-append>
        <b-btn @click="onClickButton()" variant="outline-primary">Submit</b-btn>
      </b-input-group-append>
    </b-input-group>
    <div id="hint-text-error" v-if="this.fieldError.visible">
      {{ this.fieldError.message }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: ""
    };
  },
  mounted: function() {
    console.log(this.fieldError.visible);
  },
  methods: {
    onClickButton() {
      this.$emit("textSubmit", this.text);
    }
  },
  props: {
    fieldError: Object
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

#hint-text-error {
  text-align: left;
  margin-left: 10px;
  font-size: 11px;
  color: var(--red);
  font-weight: bold;
}
</style>
