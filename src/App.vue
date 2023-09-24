<script setup>
import HeaderComponent from './components/HeaderComponent.vue';
import AddNote from './components/AddNote.vue';
import DisplayNotes from './components/DisplayNotes.vue';
import { ref } from 'vue'

const darkTheme = ref(true)
const switchTheme = () => {
  darkTheme.value = !darkTheme.value
}

</script>

<template>
  
                        <header>
                        <HeaderComponent @switch-theme="switchTheme"/>
                        </header>
                        <main>
                            <AddNote :dark-theme="darkTheme.value"/>
                            <DisplayNotes :dark-theme="darkTheme.value"/>
                </main>


    <!-- <div>
<
/div> -->
</template>

<style scoped>

header {
  margin-bottom: 150px;
}

.red {
  background: #EEEEEE;
  color: #053B50;
  border: solid 2px #FCAEAE;
}
/*  *//*  */


</style>
