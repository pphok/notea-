<script setup>
import { ref } from 'vue';

const showmodal = ref(false);
const note = ref('');
const inf_note = ref([]);

function getRandomColor() {
  const letters = '0123456789ABCDEF';
  let color = '#';
  for (let i = 0; i < 6; i++) {
    color += letters[Math.floor(Math.random() * 16)];
  }
  return color;
}

const addnote = () => {
  inf_note.value.push({
    id: inf_note.value.length + 1,
    text: note.value,
    date: new Date().toLocaleDateString(), // Format the date as a string
    backgroundColor: getRandomColor()
  });
  note.value = ''; // Clear the note input after adding
  showmodal.value = false; // Close the modal after adding the note
}
</script>

<template>
  <main>
    <div v-if="showmodal" class="overlay">
      <div class="modal">
        <textarea id="note" name="note" cols="30" rows="10" v-model="note"></textarea>
        <button @click="addnote">Add Note</button>
        <button class="cancel" @click="showmodal=false">Cancel</button>
      </div>
    </div>
    <div class="container">
      <header class="header">
        <h1 class="title">Note</h1>
        <button @click="showmodal=true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in inf_note" :key="note.id" class="card" :style="{ backgroundColor: note.backgroundColor }">
          <p class="maintext">{{ note.text }}</p>
          <p class="date">{{ note.date }}</p>
        </div>
      </div>
    </div>
  </main>
</template>


<style scoped>
main {
  height: 100vh;
  width: 100vw;
}

.container {
  max-width: 800px;
  padding: 10px;
  margin: 0 auto;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.title {
  font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
  font-size: 100px;
}

header button {
  border: none;
  background-color: black;
  color: white;
  border-radius: 50%;
  font-size: 15px;
  cursor: pointer;
  height: 50px;
  width: 50px;
}

.card {
  margin: 20px 0 0 20px;
  padding: 20px;
  background-color: aquamarine;
  border-radius: 20px;
  height: 200px;
  width: 300px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.date {
  font-size: 15px;
}
.cards-container {
  display: flex;
  flex-wrap: wrap;
}
.overlay{
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 10;
  background-color:rgba(0,0,0,0.77);
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal{
  width: 750px;
  border-radius: 10px;
  background-color: whitesmoke;
  padding: 30px;
  display: flex;
  flex-direction: column;
  position: relative;
}
.modal button{
  margin-top: 20px;
  padding: 10px;
  border: none;
  background-color: greenyellow;
  color: black;
  cursor: pointer;
  border-radius: 5px;
}
.modal button.cancel{
  background-color: red;
}
</style>
