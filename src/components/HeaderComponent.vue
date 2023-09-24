<script setup>
import { ref } from 'vue';

const blueTheme = ref(true)
const emit = defineEmits(['switchTheme'])

const switchTheme = () => {
  blueTheme.value = !blueTheme.value
  console.log('test' + blueTheme.value)
  emit('switchTheme', blueTheme.value)
}
//


</script>

<template>
        <div class="header" :class="{ red: !blueTheme }">
        <div>
        <img alt="Logo" class="logo" src="../assets/img/Notepad_icon.svg" />
      </div>
    <div id="headline">
    <h1 :class="{ red: !blueTheme }">Super-Notes</h1>
    </div>
    <div class="button">
    <button v-if="blueTheme" :class="{ red: blueTheme }" @click="switchTheme" >Switch theme</button>
    <button v-else :class="{ red: blueTheme }" @click="switchTheme">Switch theme</button>
    </div>
    </div>
    <!-- 

       -->
</template>

<style scoped>
.header {
  position: fixed;
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  /* background: v-bind('theme.background'); */
  background: #4682A9;
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

.header h1 {
   /* color: v-bind('theme.color'); */
  color: #F6F4EB;
  font-style: italic;
}
.logo {
  height: 125px;
}

button {
background: #4682A9;
color: #F6F4EB;
border-radius: 5px;
font-size: 20px;
font-weight: 600;
/* background: v-bind('theme.background'); */
/* color: v-bind('theme.color'); */
}

.button {
  grid-column: 7;
  align-self: center;
}

.red {
  background: #FF6666;
  color: #FFEADD;
  /* border: solid 2px #FCAEAE; */
}

/*  */
/*  */

</style>
