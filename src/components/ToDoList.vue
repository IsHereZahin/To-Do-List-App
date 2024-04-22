<template>
  <div class="todo-app container">
    <h2 class="app-title">My <span class="vuejs-color">Vue</span> To Do List App</h2>

    <div class="input-container">
      <input type="text" placeholder="Enter task" class="task-input" v-model="newTask">
      <button @click="addTask" class="submit-btn">Submit</button>
    </div>

    <div class="table-container">
      <table v-if="tasks.length > 0" class="task-table">
        <!-- Table header -->
        <thead>
          <tr>
            <th>SL</th>
            <th>Task</th>
            <th>Status</th>
            <th>Action</th>
          </tr>
        </thead>
        <!-- Table body -->
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index" :class="{ 'completed-task': task.completed, 'incomplete-task': !task.completed }">
            <td>{{ index + 1 }}</td>
            <td>
              <div v-if="!task.editing">
                {{ task.name }}
              </div>
              <div v-else>
                <input type="text" class="task-input" v-model="task.name" @keydown.enter="saveEditedTask(index)" @keydown.esc="cancelEdit(index)">
              </div>
            </td>
            <td>
              <button @click="toggleTaskStatus(index)" class="action-btn" :class="{ 'complete-btn': task.completed, 'incomplete-btn': !task.completed }">
                {{ task.completed ? 'Complete' : 'Pending' }}
              </button>
            </td>
            <td>
              <div v-if="!task.editing" class="action-btn-group">
                <button @click="editTask(index)" class="edit-btn"><i class="fas fa-edit"></i></button>
                <button @click="deleteTask(index)" class="delete-btn"><i class="fas fa-trash-alt"></i></button>
              </div>
              <div v-else>
                <button @click="saveEditedTask(index)" class="save-btn">Save</button>
                <button @click="cancelEdit(index)" class="cancel-btn">Cancel</button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
      <!-- Message when no tasks -->
      <p v-else class="green">No tasks available</p>
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
  tasks.value[index].editing = true;
};

// Method to save edited task
const saveEditedTask = (index) => {
  tasks.value[index].editing = false;
};

// Method to cancel editing task
const cancelEdit = (index) => {
  tasks.value[index].editing = false;
};

// Method to delete a task
const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};
</script>

<style scoped>
</style>
