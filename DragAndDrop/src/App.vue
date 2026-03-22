<script setup>

import {ref} from "vue";

const active = ref(false)
const File = ref(null)

const file = (e) => {
  if (e.dataTransfer.files[0]){
    File.value = e.dataTransfer.files[0]
  }
}

const toggleActive = () => {
  active.value = !active.value
}


</script>

<template>
  <form action="">
    <h2>DragAndDrop</h2>
    <input type="file" name="file" id="file" @change="(e)=>{
      File = e.target.files[0]
      toggleActive()
    }">
    <div class="dropzone"
           @dragenter.prevent="toggleActive"
           @dragleave.prevent="toggleActive"
           @dragover.prevent=""
           @drop.prevent="file"
           :class="{'active':active}"
    >
      <label for="file">Выберите файл </label>
      <span>или перетащите его в область</span>
    </div>
    <div v-if="File!==null">
      <button @click.prevent="()=>{
        File = null
        toggleActive()
      }">Reset</button>

      <div class="info">
        <h2>Информация о файле</h2>
        <span>Название: {{File.name}}</span>
        <span>Размер: ~ {{Math.round(File.size / 1024  )}} Кбайт</span>
        <span>Тип: {{File.type}}</span>
      </div>
    </div>
  </form>
</template>

<style scoped>
.active{
  background: #73c249;
}
.info{
  display: flex;
  flex-direction: column;
}
form{
  width: 80%;
  display: flex;
  flex-direction: column;
}
input#file{
  display: none;
}
label{
  cursor: pointer;
}

div.dropzone{
  transition: all 0.3s ease-in-out;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 500px;
  height: 500px;
  box-sizing: border-box;
  border: 1px dashed black;
  border-radius: 15px;
  padding: 10px;

}
.dropzone:hover{
  border: 1px solid black;
}
</style>
