<template>
  <div>
    <input name="searchTerm" @input="textChange" />
  </div>
</template>

<script>
export default {
  name: "SearchBar",
  methods: {
    textChange: function(e) {
      this.$emit("termChange", e.target.value);
    }
  }
};
</script>

<style scoped>
input {
  width: 75%;
}
div {
  text-align: center;
  margin: 20px;
}
</style>
