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
const noteImportant = ref()
const noteDone = ref()
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
      <h2 :class="{lightText: !darkTheme}">Add note:</h2>
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
      <div class="submit" >
        <label class="submitImage" :class="{lightImage: !darkTheme}">
          <input id="btn" type="submit" value="Add note" >
          <img :src="imagePath + 'Gartoon_actions_hexwrite.svg.png'" alt="pen">
        </label>
      </div>
    </form>
  </div>
</template>

<style scoped>

.noteHeadline {
  color: #053B50
}

form {
display: grid;
grid-template-columns: repeat(4, 1fr);
gap: 10px;
background: #EEEEEE;
border: solid 2px #053B50;
width: 300px;
padding: 10px;
border-radius: 10px;
}
label {
font-weight: 600;
}

input {
border: solid 1px #053B50;
border-radius: 5px;
width: 290px;
}

.submitImage img {
border: solid 1px #053B50;
border-radius: 10px;
background: #053B50;
opacity: 1;
transition: 0.3s;
width: 40px;
}

.titleLabel {
grid-column: 1 / span 3;
justify-self: start;
}

.titleInput {
grid-column: 1 / span 4;
justify-self: start;
}

.content {
  grid-column: 1 / span 4;
  grid-row: span 2;
}

.content textarea{
  grid-column: 1 / span 4;
  border: solid 1px #053B50;
  height: 72px;
  width: 290px;
  border-radius: 5px;
  font-size: 15px;
  margin-top: 5px;
}


#btn {
display: none;
}

.submit {
  grid-column: 4 / span 1;
  justify-self: end;
}

.light {
  background: #053B50;
  color: #EEEEEE;
  border: solid 2px #EEEEEE;
}

.lightImage img{
  background: #EEEEEE;
}
.lightText {
  color: #EEEEEE;
}

@media (min-width: 450px) {
  form {
    width: 400px;
  }

  input {
    width: 300px;
  }
  
  .content textarea {
    width: 390px;
  }
  
}
</style>
