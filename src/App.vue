<script setup>
import HeaderComponent from './components/HeaderComponent.vue';
import AddNote from './components/AddNote.vue';
import DisplayNotes from './components/DisplayNotes.vue';
import { ref } from 'vue'

const darkTheme = ref(true)
const theme = ref({
  background: '#EEEEEE'
})

const switchTheme = () => {
  darkTheme.value = !darkTheme.value
  if (darkTheme.value === true) {
    theme.value.background = '#EEEEEE'
  } else {
    theme.value.background = '#053B50'
  }
}

</script>

<template>
  <div :class="{light: !darkTheme}">
  <header>
    <HeaderComponent @switch-theme="switchTheme"/>
  </header>
  
  <main>
    <div id="add">
      <AddNote :dark-theme="darkTheme"/>
    </div>
    <div id="display">   
      <DisplayNotes :dark-theme="darkTheme"/>
    </div>
  </main>
</div>
</template>

<style scoped>

main {
  background: v-bind('theme.background');
  margin: -10px;
  padding: 10px;
  min-height: 800px;
  height: fit-content;
  margin-top: 150px;
}


header {
  position: fixed;
}

@media (min-width: 900px) {
  main {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }

  #add {
    grid-column: 1 / span 1;
  }

  #display {
    grid-column: 2 / span 1;
    margin-top: 50px;
  }

}
</style>

<!-- Färger: https://colorhunt.co/palette/053b50176b8764ccc5eeeeee -->