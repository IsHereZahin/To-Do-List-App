<template>
  <div class="todo-app container">
    <h2 class="app-title">My <span class="vuejs-color">Vue</span> To Do List App</h2>

    <div class="input-container">
      <input type="text" placeholder="Enter task" class="task-input" v-model="newTask">
      <button @click="addTask" class="submit-btn">Submit</button>
    </div>

    <div class="table-container">
      <table class="task-table">
        <thead>
          <tr>
            <th>SL</th>
            <th>Task</th>
            <th>Status</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index" :class="{ 'completed-task': task.completed, 'incomplete-task': !task.completed }">
            <td>{{ index + 1 }}</td>
            <td>{{ task.name }}</td>
            <td>
              <button @click="toggleTaskStatus(index)" class="action-btn" :class="{ 'complete-btn': task.completed, 'incomplete-btn': !task.completed }">
                {{ task.completed ? 'Complete' : 'Pending' }}
              </button>
            </td>
            <td>
              <div class="action-btn-group">
                <button @click="editTask(index)" class="edit-btn"><i class="fas fa-edit"></i></button>
                <button @click="deleteTask(index)" class="delete-btn"><i class="fas fa-trash-alt"></i></button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import '../assets/todolist.css'; // Import the external CSS file

// Sample demo data
const tasks = ref([
  { name: 'Finish homework', completed: false },
  { name: 'Go grocery shopping', completed: true },
  { name: 'Call mom', completed: false },
  { name: 'Exercise', completed: true },
  { name: 'Read a book', completed: false },
]);

// New task input
const newTask = ref('');

// Method to add a new task
const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push({ name: newTask.value, completed: false });
    newTask.value = ''; // Clear the input field after adding the task
  }
};

// Method to toggle task completion status
const toggleTaskStatus = (index) => {
  tasks.value[index].completed = !tasks.value[index].completed;
};

// Method to edit a task
const editTask = (index) => {
  // Implement edit functionality here
};

// Method to delete a task
const deleteTask = (index) => {
  // Implement delete functionality here
};
</script>

<style scoped>
</style>
