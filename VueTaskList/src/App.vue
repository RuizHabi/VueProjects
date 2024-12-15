<script setup>
import { ref } from 'vue';
// with this import add ref to line 6 to 8 and this.status to status.value

// export default {
//   setup() {no longer needed because I can make it shorter by putting it on line 1
const name = ref('Javier Ruiz');
const status = ref('active');
const tasks = ref(['Task One', 'Task Two', 'Task Three']);
const newTask = ref('');

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending';
  } else if (status.value === 'pending') {
    status.value = 'inactive';
  } else {
    status.value = 'active';
  }
};

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
    newTask.value = '';
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};
</script>
<template>
  <h1>{{ name }}</h1>
  <p v-if="status ==='active'">User is active</p>
  <p v-else-if="status === 'pending'"> User is pending</p>
  <p v-else>User is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>
  <h3>Tasks:</h3>
  <ul>
    <li v-for='(task, index) in tasks' :key="task">
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>
  <br/>

  <button v-on:click="toggleStatus"> Change Status</button>

</template>
