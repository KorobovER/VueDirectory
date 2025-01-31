<template>
    <div class="modal-overlay" @click.self="$emit('close')">
        <div class="modal">
            <h2>Добавить организацию</h2>
            <form @submit.prevent="handleSubmit">
                <label>
                    Название:
                    <input v-model="newOrg.name" required />
                </label>
                <label>
                    ФИО директора:
                    <input v-model="newOrg.director" required />
                </label>
                <label>
                    Телефон:
                    <input v-model="newOrg.phone" required />
                </label>
                <button type="submit" :disabled="!isValid">OK</button>
                <button type="button" @click="$emit('close')">Отмена</button>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            newOrg: { name: '', director: '', phone: '' },
        };
    },
    computed: {
        isValid() {
            return this.newOrg.name && this.newOrg.director && this.newOrg.phone;
        },
    },
    methods: {
        handleSubmit() {
            if (this.isValid) {
                this.$emit('add-row', { ...this.newOrg });
                this.newOrg = { name: '', director: '', phone: '' };
            }
        },
    },
};
</script>

<style scoped>
.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 999;
}

.modal {
    background: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    width: 300px;
}

label {
    display: block;
    margin-bottom: 10px;
}

input {
    width: 100%;
    padding: 8px;
    margin-top: 5px;
    box-sizing: border-box;
}

button {
    padding: 8px 12px;
    margin-right: 10px;
}
</style>