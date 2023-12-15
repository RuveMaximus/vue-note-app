<template>
    <div v-if="note">
        <input v-model="note.title" type="text" class="title-input fw-bold py-2">
        <textarea v-model="note.content" class="content-input w-100" rows="35"></textarea>
    </div>
</template>

<script setup>
defineProps(['note']);
</script>

<style scoped>
input, textarea, :is(input, textarea):focus {
    border: none;
    outline: none;
}
.title-input {
    font-size: 18px;
}

.content-input {
    resize: none;
}
</style>