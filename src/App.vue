<script setup>
import { onMounted, onUnmounted, ref, watch } from 'vue';
import NoteListItem from './components/NoteListItem.vue';
import NoteForm from './components/NoteForm.vue';
import NoteEditing from './components/NoteEditing.vue';


const notes = ref([]);
if (localStorage.getItem('notes')) {
  notes.value = JSON.parse(localStorage.getItem('notes'));
}

const currentNote = ref(null);


const save = () => {
  localStorage.setItem('notes', JSON.stringify(notes.value));
  console.log('saved')
}

const createNote = (note) => {
  let lastID = notes.value[notes.value.length - 1]?.id ?? 0;
  notes.value.unshift({
    id: lastID + 1,
    ...note
  });
  save();
  currentNote.value = notes.value[0];
}

const deleteNote = (key) => {
  const index = notes.value.findIndex(note => note.id === key);
  if (index == -1) return;
  notes.value.splice(index, 1);
  currentNote.value = null;
  save();
}

const editNote = (key) => {
  const index = notes.value.findIndex(note => note.id === key);
  if (index == -1) return;
  currentNote.value = notes.value[index];
}

const saveTimerRef = ref(null);
onMounted(() => {
  saveTimerRef.value = setInterval(save, 10_000);
});

onUnmounted(() => {
  clearInterval(saveTimerRef.value);
  saveTimerRef.value = null;
});

watch(notes.value, (newValue) => {
  notes.value = newValue;
})

const clearStorage = () => {
  localStorage.clear();
  currentNote.value = null;
  notes.value = [];
}
</script>

<template>
  <div class="container-fluid">
    <div class="row">
      <div class="p-0 bg-light overflow-y-auto col-sm-4 border-end shadow-sm" style="height: 100vh;">
        <div class="d-flex justify-content-around">
          <h2 class="fw-bold py-2">My notes</h2>
          <button class="btn btn-danger" @click="clearStorage">Clear All!</button>
        </div>
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
