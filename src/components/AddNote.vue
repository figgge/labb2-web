<script setup>
import { ref, watch, onMounted } from 'vue';
defineProps({
  blueTheme: {
    type: Boolean,
    req: true
  }
})

const notes = ref([])
const noteTitle = ref('')
const noteContent = ref('')
const noteIndex = ref(0);
const noteImportant = ref(false)
const noteDone = ref(false)
const imagePath = './src/assets/img/'

const addNote = () => {
  if (noteTitle.value.length !== 0) {
    notes.value.push({
      noteIndex: noteIndex.value,
      noteTitle: noteTitle.value,
      noteContent: noteContent.value,
      noteDate: new Date().toLocaleString('se-sv'),
      noteImportant: noteImportant.value,
      noteDone: noteDone.value
    })
    noteIndex.value++
    noteTitle.value = ''
    noteContent.value = ''
    noteImportant.value = null
  }
}

watch(notes, (newNote) => {
  localStorage.setItem('notes', JSON.stringify(newNote))
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


</script>

<template>
  <div class="form">

    <div class="noteHeadline">
      <h3>Add note:</h3>
    </div>

    <form @submit.prevent="addNote">
      <div class="titleLabel">
        <label>Title: </label>
      </div>
      <div class="titleInput">
        <input type="text" v-model="noteTitle" placeholder="Title..">
      </div>

      <div class="content">
        <label>Content: </label>
        <textarea v-model="noteContent" placeholder="Note.."></textarea>
      </div>
      <!-- <div class="important">
    <input v-model="noteImportant" type="checkbox" id="important" value="false" name="important">
    <label id="importantLabel"> Important</label>
  </div> -->
      <div class="submit">
        <label id="submit-image">
          <input id="btn" type="submit" value="Add note">
          <img :src="imagePath + 'Gartoon_actions_hexwrite.svg.png'" alt="pen">
        </label>
      </div>
    </form>
  </div>
</template>

<style scoped></style>
