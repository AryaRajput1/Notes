<script setup>
import { ref } from 'vue'

const openModel =ref(false);
const notes=ref([]);
const currNote=ref("");
function getRandomColor() {
  const color = "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  return color;
}
const deleteNote=(id)=>{
console.log(id);
notes.value.splice(id,1);
}
const addNote=()=>{
  console.log(currNote.value);
  if(currNote.value.length==0){
    alert("Please Write Something.....");
  }else{
    notes.value.push({
    id:Math.floor(Math.random()*100000),
    text:currNote.value,
    date:new Date(),
    color:getRandomColor()
  })
  currNote.value="";
  openModel.value=false;
  }
  
  // console.log(notes.value);
}
</script>

<template>
  <main>
    <div v-show="openModel" class="overlay">
      <div class="note-sec">
        <textarea type="text" placeholder="Add Notes" v-model="currNote"/>
        <button @click="addNote" id="addNoteBtn">Add Note</button>
        <button @click="openModel=false" id="closeNoteBtn">Close</button>

      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button id="addbtn" @click="openModel=true">Add Notes +</button>
      </header>
      <div class="card-section">
        <h2 id="noNotesHeading" v-if="notes.length==0">Hey Hey, Nothing is here.......!</h2>
        <div class="card" v-for="(n,k) in notes" :key="k" v-bind:style="{backgroundColor:n.color}">
          <p>{{n.text}}</p>
          <strong>{{n.date.getDate()}}/{{n.date.getMonth()+1}}/{{n.date.getFullYear()}}
            <button @click="deleteNote(k)">Delete</button>
          </strong>

        </div>
      </div>
    </div>
  </main>
</template>
<style scoped>
main{
  height: 100vh;
  width: 100vw;
}
.container{
  height: 100%;
  width: 100%;
}
header{
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 100%;
  height: 70px;
  background-color: blueviolet;
  color: white;
}
button{
  padding: 10px;
  cursor: pointer;
  border-radius: 20px;
  border: none;
  font-weight: bold;
  margin:0px 10px;
}
#noNotesHeading{
  margin: 20px;
  font-size: 3em;
  color: blueviolet;
}
header > button{
  width: 150px;
  height: 40px;
  background-color: white;
  color: blueviolet;
  
  
}
.card-section{
  display: flex;
  padding: 0px 40px;
}
.card{
  text-transform: capitalize;
  min-height: 200px;
  padding: 10px;
  margin: 10px;
  width: 200px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  background-color: aqua;
}
#addNoteBtn{
background-color: blueviolet;
color: white;

}
#closeNoteBtn{
background-color: red;
color: white;
}
.overlay{
  position: absolute;
  top: 0px;
  bottom: 0px;
  left: 0px;
  right: 0px;
  background-color:rgba(0,0,0,0.5) ;
  display: flex;
  justify-content: center;
  align-items: center;
}
.note-sec{
  display: flex;
  flex-direction: column;
  padding: 20px;
  justify-content: space-around;
  height: 400px;
  width: 25vw;
  background-color:white ;
}
textarea{
  height: 50%;
  min-height: 20%;
  max-height: 70%;
  width: 100%;
  resize: vertical;
  padding: 5px;

}
p{
  width: 100%;
  word-wrap: break-word;
}
</style>