<script setup>
import { ref, onMounted, nextTick, watch } from 'vue';
defineProps({
  blueTheme: {
    type: Boolean,
    req: true
  }
})

const notes = ref([])
const imagePath = './src/assets/img/'


onMounted(() => {
  if (localStorage.getItem('notes') !== null) {
    notes.value = JSON.parse(localStorage.getItem('notes'))
  } else {
    notes.value = []
  };
})

watch(notes, (note) => {
  localStorage.setItem('notes', JSON.stringify(note))
}, {
  deep: true
})

nextTick(() => {
  notes.value = JSON.parse(localStorage.getItem('notes'))
})

const deleteNote = (note) => {
  notes.value = notes.value.filter((n) => n !== note) || []
}


</script>

<template>
  <div class="note" :class="{ noteImportant: note.noteImportant, noteDone: note.noteDone }" v-for="note in  notes "
    :key="note">
    <div class="note-title">{{ note.noteTitle }}</div>
    <div class="note-content">{{ note.noteContent }}</div>
    <div class="note-important" v-if="note.noteImportant"><img :src="imagePath + 'Nuvola_apps_important.svg'"
        alt="important"></div>
    <div class="note-important2"><input @change="note.noteImportant = !note.noteImportant" class="importantCheckbox"
        type="checkbox" name="important">
      <label id="importantLabel">Important</label>
    </div>
    <div class="note-done"><input @change="note.noteDone = !note.noteDone" class="doneCheckbox" type="checkbox"
        name="done">
      <label class="doneLabel">Done</label>
    </div>
    <div class="note-date">{{ note.noteDate }}</div>
    <div class="note-delete"><button @click="deleteNote(note)">Delete</button></div>
  </div>
</template>
<style scoped></style>
