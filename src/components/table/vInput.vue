<template>
  <input
    class="v-input"
    type="text"
    :value="value"
    @input="$emit('input', $event.target.value)"
    :placeholder="placeholder"
  />
</template>

<script>
export default {
  name: "vInput",
  props: {
    value: {
      type: String,
    },
    placeholder: {
      type: String,
    },
  },
};
</script>

<style scoped>
.v-input {
  max-width: 160px;
  margin: 0 auto;
  margin-top: 20px;
  outline: none;
  height: 25px;
  padding-left: 15px;
  font-size: 15px;
  border: 1px solid black;
}
</style>
