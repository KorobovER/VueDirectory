<template>
    <table border="1">
        <thead>
            <tr>
                <th @click="$emit('sort-column', 'name')">Название &uarr;&darr;</th>
                <th @click="$emit('sort-column', 'director')">ФИО директора &uarr;&darr;</th>
                <th>Телефон</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(row, index) in data" :key="index">
                <td>{{ row.name }}</td>
                <td>{{ row.director }}</td>
                <td>{{ row.phone }}</td>
            </tr>
        </tbody>
    </table>
</template>

<script>
export default {
    props: {
        data: Array,
    },
    emits: ['sort-column'],
};
</script>