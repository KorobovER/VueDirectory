<template>
  <div id="app">
    <h1>Справочник организаций</h1>
    <input v-model="searchQuery" placeholder="Найти по ФИО" />
    <Table :data="filteredData" @sort-column="sortColumn" />
  </div>
</template>

<script>
import Table from './components/Table.vue';

export default {
  components: { Table },
  data() {
    return {
      organizations: [
        { name: 'Организация 1', director: 'Иванов Иван Иванович', phone: '123-456' },
        { name: 'Организация 2', director: 'Петров Петр Петрович', phone: '789-012' },
      ],
      searchQuery: '',
      sortBy: 'name',
      sortOrder: 'asc',
    };
  },
  computed: {
    filteredData() {
      // Фильтрация данных
      let data = this.organizations.filter((org) =>
        org.director.toLowerCase().includes(this.searchQuery.toLowerCase())
      );

      // Сортировка данных
      return this.sortData(data, this.sortBy, this.sortOrder);
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
  },
};
</script>