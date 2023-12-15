<template>
    <div class="note-list-item" @click="$emit('editNote', $.vnode.key)">
        <div class="d-flex flex-column">
            <h4 class="note__title">{{ note.title }}</h4>
            <p class="text-muted m-0">{{ trancute(note.content, 20) }}</p>
        </div>
        <button class="btn btn-danger" @click="$emit('deleteNote', $.vnode.key)">
            <i class="bi bi-trash2"></i>
        </button>
    </div>
</template>

<script setup>
    defineEmits(['deleteNote', 'editNote'])
    defineProps(['note']);

    function trancute(str, size) {
        return str.slice(0, size) + (str.length > size ? '...' : '');
    }
</script>

<style scoped>
    .note__title {
        user-select: none;
    }
    .note-list-item {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 100%;
        transition: background-color .2s;
        padding: 10px;
        border-bottom: 1px solid #ccc;
    }

    .note-list-item .btn-danger {
        width: 36px;
        height: 36px;
        padding: 0;
    }

    .note-list-item:hover {
        background-color: white;
        cursor: pointer;
    }
</style>