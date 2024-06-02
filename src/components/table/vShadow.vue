<template>
  <div class="v-shadow" @click="closeModal()"></div>
</template>

<script>
export default {
  name: "vShadow",
  methods: {
    closeModal() {
      this.$emit("closeModal", false);
    },
  },
};
</script>

<style scoped>
.v-shadow {
  background-color: gray;
  display: block;
  height: 100vh;
  opacity: 0.3;
  position: absolute;
  width: 100vw;
  right: 0;
  left: 0;
}
</style>
