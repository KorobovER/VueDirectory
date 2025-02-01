<template>
  <div id="app">
    <h1>Справочник организаций</h1>
    <Table :data="organizations" />
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
    };
  },
};
</script>

<style scoped></style>
