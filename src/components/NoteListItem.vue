<template>
    <div class="note-list-item" @click="$emit('editNote', $.vnode.key)">
        <div class="d-flex flex-column">
            <h4 class="note__title">{{ note.title }}</h4>
            <div class="d-flex">
                <span v-for="tag in note.tags" class="badge rounded-pill text-bg-primary">
                    {{ tag }}
                </span>
            </div>
            <p class="text-muted m-0">{{ trancute(note.content, 20) }}</p>
        </div>
        <Button class="btn-danger" @click="$emit('deleteNote', $.vnode.key)">
            <i class="bi bi-trash2"></i>
        </Button>
    </div>
</template>

<script setup>
    import Button from './UI/Button.vue';
    
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
        padding: .5rem;
        border-bottom: 1px solid #ccc;
    }

    .note-list-item:hover {
        background-color: white;
        cursor: pointer;
    }
</style>