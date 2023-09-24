<script setup>
import HeaderComponent from './components/HeaderComponent.vue';
import AddNote from './components/AddNote.vue';
import DisplayNotes from './components/DisplayNotes.vue';
import { ref } from 'vue'

const blueTheme = ref(true)
const switchTheme = () => {
  blueTheme.value = !blueTheme.value
  console.log('test2' + blueTheme.value)
}

</script>

<template>
  
                        <header>
                        <HeaderComponent @switch-theme="switchTheme"/>
                        </header>
                        <main>
                        <AddNote :blue-theme="blueTheme.value"/>
                        <DisplayNotes :blue-theme="blueTheme.value"/>
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
  background: #FF6666;
  color: #FFEADD;
  border: solid 2px #FCAEAE;
}
/*  *//*  */


</style>
