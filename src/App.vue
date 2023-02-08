<script setup>
import { ref } from "vue";
let newTodo = ref("");
let allTasks = ref([]);

function addNewTodo() {
  if(!newTodo.value) return;
  allTasks.value.push({
    id: allTasks.value.length + 1,
    done: false,
    task: newTodo.value,
  });
  newTodo.value = "";
}

function clearAllTasks() {
  allTasks.value = [];
}

function setTaskDone(task) {
  task.done = true;
}

function removeTask(task) {
  allTasks.value = allTasks.value.filter((t) => t.id !== task.id);
}
</script>

<template>
  <h1>Voeg een nieuwe taak toe</h1>
  <form @submit.prevent="addNewTodo">
    <input type="text" v-model="newTodo" />
    <button class="btn btn-primary">Add</button>
  </form>
  <br />

  <h1>Alle taken {{allTasks.length}}</h1>
  <button
    v-show="allTasks.length"
    @click="clearAllTasks"
    class="btn btn-danger"
  >
    Clear alle taken
  </button>

  <ul>
    <li
      :class="{ taskDone: task.done }"
      @click="setTaskDone(task)"
      v-for="task in allTasks"
      :key="task"
    >
      {{ task.task }}
      <button class="btn-close" @click="removeTask(task)"></button>
    </li>
  </ul>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
}
.taskDone {
  text-decoration: line-through;
}
</style>

