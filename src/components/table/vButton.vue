<template>
  <button
    class="v-btn"
    @click="openModal(), closeModal(), createOrganisation()"
  >
    {{ btnText }}
  </button>
</template>

<script>
export default {
  name: "vButton",
  props: {
    btnText: {
      type: String,
      required: true,
    },
  },
  methods: {
    openModal() {
      this.$emit("openModal", true);
    },
    closeModal() {
      this.$emit("closeModal", false);
    },
    createOrganisation() {
      this.$emit("createOrganisation");
    },
  },
};
</script>

<style scoped>
.v-btn {
  background-color: white;
  cursor: pointer;
  outline: none;
  border: 1px solid black;
  transition: all 0.2s ease-in-out;
  padding: 5px 10px;
}

.v-btn:hover {
  background-color: grey;
  color: white;
  border-color: gray;
}
</style>
