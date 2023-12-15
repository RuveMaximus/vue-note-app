<template>
    <div v-if="note">
        <input v-model="note.title" type="text" class="title-input fw-bold py-2">
        <textarea v-model="note.content" class="content-input w-100 border" rows="30"></textarea>

        <div class="btn-group">
            <input class="btn-check" type="checkbox" id="study" value="study" v-model="note.tags">
            <label class="btn btn-outline-primary" for="study">Study</label>

            <input class="btn-check" type="checkbox" id="work" value="work" v-model="note.tags">
            <label class="btn btn-outline-primary" for="work">Work</label>

            <input class="btn-check" type="checkbox" id="personal" value="personal" v-model="note.tags">
            <label class="btn btn-outline-primary" for="personal">Personal</label>
        </div>
    </div>
</template>

<script setup>
defineProps(['note']);
</script>

<style scoped>
input, :is(input, textarea):focus {
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