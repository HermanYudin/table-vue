<template>
  <form class="v-modal" @submit.prevent>
    <vTitle class="modal-title" vTitle="Добавить организацию" />
    <vInput v-model="orgName" placeholder="Название" />
    <vInput v-model="orgPhone" placeholder="Номер телефона" />
    <vInput v-model="orgDir" placeholder="ФИО Директора" />
    <div class="modal-btns">
      <vButton @closeModal="closeModal" btnText="Отмена" />
      <vButton
        :disabled="!(orgName && orgPhone && orgDir)"
        @createOrganisation="createOrganisation"
        btnText="Ок"
      />
    </div>
  </form>
</template>

<script>
import vInput from "./vInput";
import vButton from "./vButton";
import vTitle from "./vTitle";

export default {
  name: "vModal",
  components: {
    vInput,
    vButton,
    vTitle,
  },
  data() {
    return {
      orgName: "",
      orgPhone: "",
      orgDir: "",
    };
  },
  methods: {
    closeModal(data) {
      this.$emit("closeModal", data);
    },
    createOrganisation() {
      this.$emit("createOrganisation", {
        orgName: this.orgName,
        orgPhone: this.orgPhone,
        orgDir: this.orgDir,
      });
    },
  },
};
</script>

<style scoped>
.v-modal {
  display: flex;
  max-width: 220px;
  background-color: white;
  flex-direction: column;
  justify-content: center;
  padding-bottom: 20px;
  border: 1px solid black;
  animation-duration: 0.55s;
  animation-fill-mode: both;
  animation-name: fadeInDown-7f688c73;
  left: 0;
  margin: 0 auto;
  position: fixed;
  right: 0;
  top: 29%;
  z-index: 2;
  animation-duration: 0.55s;
  animation-fill-mode: both;
  animation-name: fadeInDown;
}

.modal-btns {
  display: flex;
  justify-content: center;
  margin-top: 25px;
  gap: 10px;
}

.modal-title {
  margin-top: 20px;
  font-size: 17px;
  text-align: center;
  margin-bottom: 0px;
}

@keyframes fadeInDown {
  0% {
    opacity: 0;
    transform: translate3d(0px, -100%, 0px);
  }
  100% {
    opacity: 1;
    transform: none;
  }
}
</style>
