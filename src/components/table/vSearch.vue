<template>
  <div class="vSearch-block">
    <input
      class="v-search"
      type="search"
      placeholder="Найти по ФИО"
      v-model="searchQuery"
      @input="updateSearchQuery"
    />
  </div>
</template>

<script>
export default {
  name: "vSearch",
  data() {
    return {
      searchQuery: "",
    };
  },
  methods: {
    updateSearchQuery() {
      this.$emit("updateSearchQuery", this.searchQuery);
    },
  },
};
</script>

<style scoped>
.v-search {
  outline: none;
  font-size: 16px;
  max-width: 200px;
  height: 30px;
  padding-left: 15px;
}

input[type="search"]::-webkit-search-cancel-button {
  -webkit-appearance: none;
}
</style>
