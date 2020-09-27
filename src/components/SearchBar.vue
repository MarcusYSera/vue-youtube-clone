<template>
  <div>
    Search Bar
    <!-- <input v-on:input="onInput" /> -->
    <input @input="onInput" />
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  methods: {
    onInput(event) {
      this.$emit('term-change', event.target.value);
    },
  },
};
</script>

<style scoped>
input {
  width: 75%;
  color: black;
}
div {
  text-align: center;
  margin: 20;
}
</style>
