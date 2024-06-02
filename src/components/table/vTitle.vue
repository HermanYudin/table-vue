<template>
  <h2 class="v-title">{{ vTitle }}</h2>
</template>

<script>
export default {
  name: "vTitle",
  props: {
    vTitle: {
      type: String,
    },
  },
};
</script>

<style scoped></style>
