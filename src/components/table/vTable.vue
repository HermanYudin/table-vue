<template>
  <div class="v-table">
    <div class="v-table__header">
      <p @click="sortByName()">
        {{ name }} <span class="material-icons"> south </span>
      </p>
      <p @click="sortByDirector()">
        {{ director }}<span class="material-icons"> south </span>
      </p>
      <p>{{ telephone }}</p>
      <p></p>
    </div>
    <div class="v-table__body">
      <vTableRow
        v-for="organisation in filteredOrganisations"
        :key="organisation.id"
        :organisation="organisation"
        @deleteRow="deleteRow"
      />
    </div>
    <div class="v-table__pagination" v-if="!searchQuery && pages > 1">
      <div
        class="page"
        v-for="page in pages"
        :key="page"
        :class="{ page__selected: page === pageNumber }"
        @click="pageClick(page)"
      >
        {{ page }}
      </div>
    </div>
    <div
      class="v-table__arrows"
      v-if="localOrganisations.length && !searchQuery && pages > 1"
    >
      <div class="left-arrow" @click="prevPage()">
        <span class="material-icons left"> south </span>
      </div>
      <div>
        <p class="page-number">
          {{ pageNumber }}
        </p>
      </div>
      <div class="right-arrow" @click="nextPage()">
        <span class="material-icons right"> south </span>
      </div>
    </div>
  </div>
</template>

<script>
import vTableRow from "../table/vTableRow";

export default {
  name: "vTable",
  components: {
    vTableRow,
  },
  props: {
    organisations: {
      type: Array,
      default: () => [],
    },
    searchQuery: {
      type: String,
      default: "",
    },
    name: {
      type: String,
    },
    director: {
      type: String,
    },
    telephone: {
      type: String,
    },
  },
  data() {
    return {
      localOrganisations: [],
      organisationsPerPage: 2,
      pageNumber: 1,
    };
  },
  created() {
    this.localOrganisations = [...this.organisations];
  },
  methods: {
    pageClick(page) {
      this.pageNumber = page;
    },
    sortByDirector() {
      this.localOrganisations.sort((a, b) =>
        a.director.toLowerCase().localeCompare(b.director.toLowerCase())
      );
    },
    sortByName() {
      this.localOrganisations.sort((a, b) =>
        a.name.toLowerCase().localeCompare(b.name.toLowerCase())
      );
    },
    nextPage() {
      if (this.pageNumber >= this.pages) {
        return;
      }
      this.pageNumber++;
    },
    prevPage() {
      if (this.pageNumber === 1) {
        return;
      }
      this.pageNumber--;
    },
    deleteRow(organisation) {
      const index = this.localOrganisations.findIndex(
        (org) => org.id === organisation.id
      );
      if (index !== -1) {
        this.localOrganisations.splice(index, 1);
        if (this.localOrganisations.length === 0 && this.pageNumber > 1) {
          this.pageNumber = -1;
        } else if (this.localOrganisations.length === 0) {
          this.pageNumber = 1;
        } else if (this.pageNumber > this.pages) {
          this.pageNumber = this.pages;
        }
      }
      this.$emit("deleteRow", organisation);
    },
  },
  computed: {
    pages() {
      return Math.ceil(this.localOrganisations.length / 2);
    },
    paginatedOrganisations() {
      let from = (this.pageNumber - 1) * this.organisationsPerPage;
      let to = from + this.organisationsPerPage;
      return this.localOrganisations.slice(from, to);
    },
    filteredOrganisations() {
      if (this.searchQuery) {
        return this.organisations.filter((organisation) => {
          return (
            organisation.name
              .toLowerCase()
              .includes(this.searchQuery.toLowerCase()) ||
            organisation.director
              .toLowerCase()
              .includes(this.searchQuery.toLowerCase()) ||
            organisation.telephone.includes(this.searchQuery)
          );
        });
      } else {
        return this.paginatedOrganisations;
      }
    },
  },
  watch: {
    organisations(newVal) {
      this.localOrganisations = [...newVal];
    },
  },
};
</script>

<style scoped>
.v-table__header {
  display: flex;
  justify-content: space-around;
}

.v-table__header p {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-basis: 33%;
  text-align: left;
  padding: 8px 16px;
  border: solid 1px black;
  margin-bottom: 0px;
  cursor: pointer;
}

.v-table__header p:nth-child(1) {
  border-right: none;
}

.v-table__header p:nth-child(3) {
  border-left: none;
  cursor: default;
}

.v-table__header p:nth-child(4) {
  border-left: none;
  cursor: default;
  max-width: 20px;
}

.v-table__pagination {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 5px;
}

.page {
  padding: 5px 10px;
  border: solid 1px black;
  margin-top: 10px;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
}

.page:hover {
  background-color: gray;
  color: white;
  border-color: gray;
}

.page__selected {
  background-color: gray;
  color: white;
  border-color: gray;
}

.material-icons {
  margin-left: 10px;
  cursor: pointer;
}

.v-table__arrows {
  display: flex;
  justify-content: end;
  align-items: center;
  margin-right: 10px;
}

.left-arrow {
  margin-right: 10px;
}

.left {
  transform: rotate(90deg);
}

.right {
  transform: rotate(-90deg);
}
</style>
