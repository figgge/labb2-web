<script setup>
import { ref } from 'vue';

const darkTheme = ref(true)
const emit = defineEmits(['switchTheme'])

const switchTheme = () => {
  darkTheme.value = !darkTheme.value
  emit('switchTheme', darkTheme.value)
}
//


</script>

<template>
        <div class="header" :class="{ light: !darkTheme }">
        <div>
        <img alt="Logo" class="logo" src="../assets/img/Notepad_icon.svg" />
        </div>
        <div id="headline">
        <h1 :class="{ light: !darkTheme }">Super-Notes</h1>
      </div>
      <div class="button">
      <button v-if="darkTheme" :class="{ light: darkTheme }" @click="switchTheme" >Switch theme</button>
      <button v-else :class="{ light: darkTheme }" @click="switchTheme">Switch theme</button>
      </div>
      </div>
  <!--
 -->     
<!--  -->
</template>

<style scoped>
.header {
  position: fixed;
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  /* background: v-bind('theme.background'); */
  background: #053B50;
  gap: 20px;
  padding: 10px;
  top:0;
  left: 0;
  width: 100%;
}
#headline {
  grid-column: 2 /span 2;
  align-self: center;
}

h1 {
   /* color: v-bind('theme.color'); */
  color: #EEEEEE;
  font-style: italic;
}
.logo {
  height: 125px;
}

button {
background: #053B50;
color: #EEEEEE;
border-radius: 10px;
font-size: 20px;
font-weight: 600;
/* background: v-bind('theme.background'); */
/* color: v-bind('theme.color'); */
}

.button {
  grid-column: 7;
  align-self: center;
}

.light {
  background: #EEEEEE;
  color: #053B50;
  /* border: solid 2px #FCAEAE; */
}

/*  */
/*  */

</style>
