<script setup>
import { ref, onMounted, watch, nextTick } from 'vue';
defineProps({
  darkTheme: {
    type: Boolean,
    required: true
  }
})

const notes = ref([])
const imagePath = './src/assets/img/'

watch(notes, (note) => {
  localStorage.setItem('notes', JSON.stringify(note))
}, {
  deep: true
})


onMounted(() => {
  if (localStorage.getItem('notes') !== null) {
    notes.value = JSON.parse(localStorage.getItem('notes'))
  } else {
    notes.value = []
  };
})

nextTick(() => {
  notes.value = JSON.parse(localStorage.getItem('notes'))
})


const deleteNote = (note) => {
  notes.value = notes.value.filter((n) => n !== note) || []
  location.reload() // ← nödlösning

}


</script>

<template>
  <div v-for="note in notes " :key="note" class="note" :class="{light: !darkTheme ,noteImportant: note.noteImportant, noteDone: note.noteDone, lightImportant: !darkTheme && note.noteImportant}">
    <div class="note-title">{{ note.noteTitle }}</div>
    <div class="note-content">{{ note.noteContent }}</div>
    <div class="note-important" v-if="note.noteImportant"><img :src="imagePath + 'Nuvola_apps_important.svg'" alt="important"></div>
    <div class="note-important2"><input @change="note.noteImportant = !note.noteImportant" class="checkbox" type="checkbox" :checked="note.noteImportant" name="important">
      <label>Important</label>
    </div>
    <div class="note-done"><input @change="note.noteDone = !note.noteDone" class="checkbox" :checked="note.noteDone" type="checkbox" name="done">
      <label>Done</label>
    </div>
    <div class="note-date">{{ note.noteDate }}</div>
    <div class="note-delete">
      <button :class="{lightButton: !darkTheme}" @click="deleteNote(note)">Delete</button>
    </div>
  </div>
</template>

<style scoped>
.note {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: auto;
  background: #EEEEEE;
  color: #053B50;
  border: solid 2px #053B50;
  border-radius: 5px;
  width: fit-content;
  max-width: 400px;
  margin-top: 5px;
  padding: 5px;
}

.note-title {
  grid-column: 1 / span 3;
  margin-bottom: 10px;
  font-weight: 600;
  font-size: large;
}

.note-content {
  grid-column: 1 / span 4;
  margin-bottom: 10px;
  font-size: medium;
}

.note-date {
  grid-column: 3 / span 1;
  font-style: italic;
  opacity: 0.7;
}

.note-important {
  grid-row: 1 / span 1;
  grid-column: 4 / span 1;
  justify-self: end;
}


.noteImportant {
  background: linear-gradient(600deg, #EEEEEE, #f0c2c2);
}

.note-important img {
  width: 25px;
}

.note-important2 {
  grid-column: 1 / span 1;
}

.note-delete {
  grid-column: 4 / span 1;
  justify-self: end;
  align-self: end;
}

.noteDone {
  opacity: 0.5;
  text-decoration: line-through;
}

button {
  font-size: small;
  font-weight: bold;
  background: #053B50;
  color: #EEEEEE;
  border-radius: 5px;
}

.checkbox {
  accent-color: #053B50;
  width: 20px;
  height: 20px;
  vertical-align: middle;
}

.light {
  background: #053B50;
  color: #EEEEEE;
  border: solid 1px #EEEEEE;
}

.lightImportant {
  background: linear-gradient(600deg, #f8f8f8, #ffb2b2);
  color: #053B50;
}

.lightButton {
  background: #EEEEEE;
  color: #053B50;
}
</style>
