<script setup>
import { ref } from 'vue';
import NewTaskInput from '../components/NewTaskInput.vue';
import NewColumnInput from '../components/NewColumnInput.vue';
import Task from '../components/Task.vue';

//state
const storageTasks = JSON.parse(localStorage.getItem('tasks')) || [];
const storageColumns = JSON.parse(localStorage.getItem('columns')) || [];
const tasks = ref(storageTasks);
const columns = ref(storageColumns);

//methods
const saveTasksLS = () => {
  localStorage.setItem('tasks', JSON.stringify(tasks.value))
}

const saveColumnsLS = () => {
  localStorage.setItem('columns', JSON.stringify(columns.value))
}


const getTask = (value) => {
  if(value != ''){
    tasks.value.push({id: tasks.value.length, title: value, list: 0})
  }
  saveTasksLS()
}

const getColumn = (value) => {
  if(value != ''){
    columns.value.push({id: columns.value.length, title: value})
  }
  saveColumnsLS()
}

const deleteColumn = (id, columns) => {
  columns.forEach((el, idi) =>{
        if(el.id == id){
            columns.splice(idi, 1);
        }
  })
  saveColumnsLS()
}

const deleteTask = (id, tasks) => {
  tasks.forEach((el, idi) =>{
        if(el.id == id){
            tasks.splice(idi, 1);
        }
  })
  saveTasksLS()
}

const onDragStart = (event, task) => {
    console.log(task);
    event.dataTransfer.dropEffect = 'move';
    event.dataTransfer.effectAllowed = 'move';
    event.dataTransfer.setData('taskID', task.id);
}

const onDrop = (event, list) => {
  const taskID = event.dataTransfer.getData('taskID');
  const task = tasks.value.find((task) => task.id == taskID);
  task.list = list
}
</script>

<template>
  <header class="header">
    <NewTaskInput @on-get-task="getTask"/>
    <NewColumnInput @on-get-column="getColumn"/>
  </header>
  <main >
    <div class="column-list">
      <div class="column"
        @drop="onDrop($event, column.id)"
        @dragenter.prevent
        @dragover.prevent
        v-for="column in columns"
        :key="column.id"
      >
      <div class="column__block-name">
        <div class="column__name">
          {{ column.title }}
        </div>
        <div class="close-x" 
          @click="deleteColumn(column.id, columns)"
        >X</div>
      </div>
        <div class="column__block"
          v-for="task in tasks.filter((task) => task.list == column.id)"
          :key="task.id"
          draggable="true"
          @dragstart="onDragStart($event, task)"
          >
          <Task 
            :title="task.title" 
            @on-delete-task="deleteTask(task.id, tasks)"
          />
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped lang="scss">
.header {
  display: flex;
  justify-content: space-between;
  width: 600px;
  margin: 60px auto;
}

.column-list {
  width: 1000px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;

  .column__block-name {
    display: flex;
    
    .close-x {
      margin-left: 5px;
      visibility: hidden;
      opacity: 0;
      z-index: -1;
      transition: 0.2s;
    }
  }

  .column__block-name:hover .close-x {
    visibility: visible;
    opacity: 1;
    z-index: 99;
    cursor: pointer;
  }
}

.column__name {
        width: fit-content;
        height: fit-content;
        background-color: #32a89d;
        border: 3px solid #277a73;
        font-size: 20px;
        display: flex;
        align-items: center;
        color: #fff;
        padding: 5px;
        cursor: pointer;
    }

    .column__block {
        width: fit-content;
        word-wrap: break-word;
        height: auto;
    }
</style>