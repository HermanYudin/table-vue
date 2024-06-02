<template>
  <div class="app" id="app">
    <vModal
      v-if="activeModal"
      @closeModal="closeModal"
      @createOrganisation="createOrganisation"
    />
    <vShadow v-if="activeModal" @closeModal="closeModal" />
    <vTitle class="main-title" vTitle="Таблица организаций" />
    <div class="top">
      <v-search @updateSearchQuery="updateSearchQuery" />
      <vButton btnText="Добавить" @openModal="openModal" />
    </div>
    <vTable
      :name="name"
      :director="director"
      :telephone="telephone"
      :organisations="organisations"
      :searchQuery="searchQuery"
      @deleteRow="deleteRow"
    />
  </div>
</template>

<script>
import vTable from "./components/table/vTable";
import vSearch from "./components/table/vSearch";
import vButton from "./components/table/vButton";
import vModal from "./components/table/vModal";
import vShadow from "./components/table/vShadow";
import vTitle from "./components/table/vTitle";

export default {
  name: "App",
  components: {
    vTable,
    vSearch,
    vButton,
    vModal,
    vShadow,
    vTitle,
  },
  data() {
    return {
      name: "Название",
      director: "ФИО Директора",
      telephone: "Номер телефона",
      searchQuery: "",
      modalTitle: "Добавить организацию",
      activeModal: false,
      organisations: [
        {
          id: 1,
          name: "ООО 'ВЕКТОР'",
          director: "Иванов И.И.",
          telephone: "+7 000 123 45 67",
        },
        {
          id: 2,
          name: "ИП Сидоров С.С.",
          director: "Сидоров С.С.",
          telephone: "+7 000 56 78 99",
        },
        {
          id: 3,
          name: "ООО 'ЛАЙТ'",
          director: "Лайтов А.А.",
          telephone: "+7 000 321 48 77",
        },
        {
          id: 4,
          name: "ИП Малинин М.М.",
          director: "Малинин М.М.",
          telephone: "+7 000 88 99 77",
        },
        {
          id: 5,
          name: "ООО 'РОГА И КОПЫТА'",
          director: "Рогокопытов П.П.",
          telephone: "+7 000 441 98 17",
        },
      ],
    };
  },
  methods: {
    updateSearchQuery(newSearchQuery) {
      this.searchQuery = newSearchQuery;
    },
    openModal(data) {
      this.activeModal = data;
    },
    closeModal(data) {
      this.activeModal = data;
    },
    createOrganisation(data) {
      const newOrg = {
        id: this.organisations.length + 1,
        name: data.orgName,
        director: data.orgDir,
        telephone: data.orgPhone,
      };

      const existingOrgIndex = this.organisations.findIndex(
        (org) => org.name === data.orgName
      );

      if (existingOrgIndex === -1) {
        this.organisations.push(newOrg);
        this.activeModal = false;
      } else {
        alert("Организация уже была добавлена");
      }
    },
    deleteRow(organisation) {
      const index = this.organisations.findIndex(
        (org) => org.id === organisation.id
      );
      if (index !== -1) {
        this.organisations.splice(index, 1);
      }
    },
  },
};
</script>

<style>
body {
  padding: 0px;
  margin: 0px;
  position: relative;
}

.app {
  max-width: 900px;
  margin: 0 auto;
}

.top {
  display: flex;
  justify-content: space-between;
}

.main-title {
  font-size: 25px;
  padding-top: 50px;
  padding-bottom: 50px;
  margin-top: 0px;
  text-align: center;
  margin-bottom: 0px;
}
</style>
