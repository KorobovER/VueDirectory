<template>
  <div id="app">
    <h1>Справочник организаций</h1>
    <input v-model="searchQuery" placeholder="Найти по ФИО" />
    <button @click="showModal = true">Добавить</button>
    <Table :data="paginatedData" @sort-column="sortColumn" />
    <Pagination :total-pages="totalPages" :current-page="currentPage" @page-changed="changePage" />
    <Modal v-if="showModal" @close="showModal = false" @add-row="addRow" />
  </div>
</template>

<script>
import Table from './components/Table.vue';
import Pagination from './components/Pagination.vue';
import Modal from './components/Modal.vue';

export default {
  components: { Table, Pagination, Modal },
  data() {
    return {
      organizations: [
        { name: 'Организация 1', director: 'Иванов Иван Иванович', phone: '123-456' },
        { name: 'Организация 2', director: 'Петров Петр Петрович', phone: '789-012' },
        { name: 'Организация 2', director: 'Петров Петр Петрович', phone: '789-012' },
        { name: 'Организация 2', director: 'Петров Петр Петрович', phone: '789-012' },
      ],
      searchQuery: '',
      sortBy: 'name',
      sortOrder: 'asc',
      currentPage: 1,
      itemsPerPage: 3,
      showModal: false,
    };
  },
  computed: {
    filteredData() {
      let data = this.organizations.filter((org) =>
        org.director.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
      return this.sortData(data, this.sortBy, this.sortOrder);
    },
    paginatedData() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.filteredData.slice(start, end);
    },
    totalPages() {
      return Math.ceil(this.filteredData.length / this.itemsPerPage);
    },
  },
  methods: {
    sortColumn(key) {
      if (this.sortBy === key) {
        this.sortOrder = this.sortOrder === 'asc' ? 'desc' : 'asc';
      } else {
        this.sortBy = key;
        this.sortOrder = 'asc';
      }
    },
    sortData(data, key, order) {
      const modifier = order === 'asc' ? 1 : -1;
      return [...data].sort((a, b) => {
        const valueA = a[key]?.toString().toLowerCase() || '';
        const valueB = b[key]?.toString().toLowerCase() || '';
        return valueA.localeCompare(valueB) * modifier;
      });
    },
    changePage(page) {
      this.currentPage = page;
    },
    addRow(newOrg) {
      this.organizations.push(newOrg);
      this.showModal = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  margin: 20px;
}
</style>