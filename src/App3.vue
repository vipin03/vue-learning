<template>
    hiii {{ name }}
    <br />
    user is {{ status }}
    
  <br/>
    <button @click="toggleSatus">toggele</button>
    <br />
    <form @submit.prevent="addTask">
      <label>
          Add task
      </label>
      <input type="text" id="newTask" name="newtask" v-model="newTask">
      <button type="submit"> submit</button>
    </form>
    <h3>Tasks:</h3>  
    <ul id="test">
      <li v-for="(task,index) in tasks" :key="task"> <span>{{ task.title }}</span> <button @click="deleteTask(index)">x</button> </li>
    </ul>
  </template>
  
  <script setup>
  import {onMounted, ref} from 'vue';
  
      const name = ref('vipin b');
      let  status = ref('active');
      const  tasks = ref(['task 1','tasl2']);
      const newTask = ref('');
      const toggleSatus = () => {
        if(status.value == "active") {
          status.value = "pending"
        } else if (status.value == "pending") {
          status.value = "inactive";
        } else {
          status.value = "active";
        }
      }
  
      const addTask = () => {
        if(newTask.value.trim() != '') {
          tasks.value.push(newTask.value)
          newTask.value = '';
        }
      }
  
      const deleteTask = (index) => {
        tasks.value.splice(index,1);
      } 
  
      onMounted(async () => {
        try {
          const response = await fetch("https://jsonplaceholder.typicode.com/todos")
          const data = await response.json();
          tasks.value = data,map((task) => task.title);
        } catch (error) {
          console.log('error  fetching')
        }
      })
  
  </script>