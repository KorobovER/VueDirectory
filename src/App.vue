<template>
  <div id="app">
    <h1>Список организаций</h1>
    <ul>
      <li v-for="(org, index) in organizations" :key="index">
        {{ org.name }} - {{ org.director }} - {{ org.phone }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
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
