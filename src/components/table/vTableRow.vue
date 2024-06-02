<template>
  <div class="v-table-row">
    <div class="row row-name">{{ organisation.name }}</div>
    <div class="row row-director">{{ organisation.director }}</div>
    <div class="row row-telephone">{{ organisation.telephone }}</div>
    <div class="row row-close" @click="deleteRow()">
      <img class="close" :src="deleteCross" alt="close" />
    </div>
  </div>
</template>

<script>
export default {
  name: "vTableRow",
  data() {
    return {
      deleteCross: require("@/assets/close.png"),
    };
  },
  props: {
    organisation: {
      type: Object,
      required: true,
    },
  },
  methods: {
    deleteRow() {
      this.$emit("deleteRow", this.organisation);
    },
  },
};
</script>

<style scoped>
.v-table-row {
  display: flex;
  justify-content: space-around;
  border: solid 1px black;
  border-top: none;
}

.row {
  flex-basis: 33%;
  padding: 8px 16px;
  text-align: left;
}

.row:nth-child(1) {
  border-right: solid 1px black;
}

.row:nth-child(3) {
  border-left: solid 1px black;
}

.row:last-child {
  border-left: solid 1px black;
}

.row-close {
  max-width: 20px;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
}

.row-close:hover {
  background-color: brown;
}

.close {
  max-width: 20px;
  max-height: 20px;
}
</style>
