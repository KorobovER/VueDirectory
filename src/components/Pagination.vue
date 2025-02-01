<template>
    <div>
        <button :disabled="currentPage === 1" @click="$emit('page-changed', currentPage - 1)">
            ❮ Предыдущая
        </button>
        <span>Страница {{ currentPage }} из {{ totalPages }}</span>
        <button :disabled="currentPage === totalPages" @click="$emit('page-changed', currentPage + 1)">
            Следующая ❯
        </button>
    </div>
</template>

<script>
export default {
    props: {
        currentPage: Number,
        totalPages: Number,
    },
    emits: ['page-changed'],
};
</script>

<style>
button {
    padding: 8px 12px;
    margin: 0 5px;
    background-color: #8fdc92;
    color: white;
    border: none;
    cursor: pointer;
}

button:disabled {
    background-color: #ccc;
}
</style>