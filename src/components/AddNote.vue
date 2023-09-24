<script setup>
import { ref, watch, onMounted } from 'vue';
defineProps({
  darkTheme: {
    type: Boolean,
    req: true
  }
})

const notes = ref([])
const noteTitle = ref('')
const noteContent = ref('')
const noteIndex = ref(0);
const imagePath = './src/assets/img/'

const addNote = () => {
  if (noteTitle.value.length !== 0) {
    notes.value.push({
      noteIndex: noteIndex.value,
      noteTitle: noteTitle.value,
      noteContent: noteContent.value,
      noteDate: new Date().toLocaleString('se-sv'),
      noteImportant: false,
      noteDone: false
    })
    noteIndex.value++
    noteTitle.value = ''
    noteContent.value = ''
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

                                      <form :class="{ light: !darkTheme }" @submit="addNote">

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

                              <div class="submit">
                                <label id="submit-image">
                                <input id="btn" type="submit" value="Add note">
                                <img :src="imagePath + 'Gartoon_actions_hexwrite.svg.png'" alt="pen">
                                </label>
                          </div>
                              </form>
                              </div>
                          <!--  -->
</template>

<style scoped>
form {
  display: grid;
  grid-template-columns: repeat(4, 100px);
  gap: 10px;
  background: #EEEEEE;
  border: solid 2px #053B50;
  width: 400px;
  padding: 10px;
  border-radius: 10px;
}

input {
  border: solid 1px black;
}

#submit-image img {
  border: solid 1px black;
  border-radius: 10px;
  background: #053B50;
  opacity: 1;
  transition: 0.3s;
  width: 40px;
}

#btn {
  display: none;
}




</style>
