<script setup>
import { ref } from 'vue';
import NoteListItem from './components/NoteListItem.vue';
import NoteForm from './components/NoteForm.vue';
import NoteEditing from './components/NoteEditing.vue';


const notes = ref([]);
const currentNote = ref(null);

const createNote = (note) => {
  let lastID = notes.value[notes.value.length - 1]?.id ?? 0;
  notes.value.unshift({
    id: lastID + 1,
    ...note
  });
}

const deleteNote = (key) => {
  const index = notes.value.findIndex(note => note.id === key);
  if (index == -1) return;
  notes.value.splice(index, 1);
}

const editNote = (key) => {
  const index = notes.value.findIndex(note => note.id === key);
  if (index == -1) return;
  currentNote.value = notes.value[index];
}
</script>

<template>
  <div class="container-fluid">
    <div class="row">
      <div class="p-0 bg-light overflow-y-auto col-md-3 col-sm-6 border-end shadow-sm" style="height: 100vh;">
        <h2 class="fw-bold py-2 text-center">My notes</h2>
        <NoteListItem v-for="note in notes" 
          :note=note
          :key=note.id
          @deleteNote="deleteNote"
          @editNote="editNote"/>
        <NoteForm @createNote="createNote" style="bottom:2px;position: absolute;width:inherit;"/>
      </div>
      <div class="col">
        <NoteEditing :note="currentNote"/>
      </div>
    </div>
  </div>
</template>
