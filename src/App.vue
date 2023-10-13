<script setup>
import {ref} from 'vue';

const binding = ref('')
const error = ref(false);
const showModal = ref(false);
const notes = ref([])


function getRandomColor(){
 const color = "hsl(" + Math.random() * 360 + ",100%,75%)";
  return color;
}

const addNotes = () =>{
  if(binding.value.length < 10){
    error.value = true;
    return;
  }
   error.value = false;
    notes.value.push({
      text:binding.value,
      date:new Date(),
      id:Math.floor(Math.random() * 10000000),
      backgroundColor:getRandomColor()
    })

  showModal.value = false;
  binding.value = '';

}

</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea @focus="error = false" v-model.trim="binding" name="notes" id="notes" cols="30" rows="10">
        </textarea>
        <p v-if="error" id="para">Text must be more than 10 characters</p>
        <button @click="addNotes">Add Note</button>
        <div @click="showModal = false" class="close">Close</div>
      </div>

    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes"
        :key="note.id"
         class="card"
         :style="{backgroundColor: note.backgroundColor}"
          >
          <p class="main-text">
            {{ note.text }}
          </p>
          <p class="date">{{ note.date.toLocaleDateString('en-US') }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped >
  main{
    height: 100vh;
    width: 100vw;
  }
  .container{
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }

  header{
    display: flex;
    justify-content: space-between;
    align-items: center ;
  }
  header button{
    color: white;
    cursor: pointer;
    background-color: black;
    border-radius: 50%;
    width:2.5em;
    height:2.5em;
  }
  h1{
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }
  .card{
    width: 200px;
    height: 200px;
    background-color: rgb(237,182,44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin: 0 20px 20px 0;
  }
  .date{
    font-size:12.5px ;
    font-weight: bold;
  }
  .cards-container{
    display: flex;
    flex-wrap: wrap;
    word-break: break-all;
    justify-content:flex-start;
  } 

  @media all and (max-width: 460px){
    .cards-container{
    display: flex;
    flex-wrap: wrap;
    word-break: break-all;
    justify-content:center;
  } 
  }
  .overlay{
    position: absolute;
    width: 100%;
    height: 100%;
    z-index: 10;
    background: rgba(0,0,0,0.75);
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .modal{
    width:750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }
  .modal textarea{
    padding: 1em;
  }
  .modal button{
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  } 
  .modal .close{
    text-align: center;
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color:red;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  } 
  .modal .close:hover{
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color:rgb(238, 61, 61);
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  } 
  .modal button:hover{
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: rgb(171, 99, 238);
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  } 
  #para{
    color: red;
  }
</style>