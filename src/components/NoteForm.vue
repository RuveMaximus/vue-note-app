<template>
    <form class="d-flex" @submit.prevent="createNote">
        <div class="input-group">
            <input class="form-control" v-model="title" type="text" placeholder="Note title...">
            <Button class="btn-primary">
                <i class="bi bi-plus-circle-fill"></i>
            </Button>
        </div>
    </form>
</template>

<script setup>
import { ref } from 'vue';
import Button from '../components/UI/Button.vue';

const title = ref();

const emit = defineEmits(['createNote']);

const createNote = () => {
    if (title.value.trim() === '') {
        return alert('Fill the note title!');
    }
    emit("createNote", {
        title: title.value,
        content: '',
        tags: []
    });
    title.value = '';
}
</script>