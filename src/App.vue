<!-- composition api -->

<script setup>
import { onMounted, ref } from "vue";

const name = ref("Adnan Khan");
const status = ref("active");
const tasks = ref(["Task1", "Task2", "Task3"]);
const newTask = ref("");

const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await res.json();
    console.log(data);

    tasks.value = data.map((task) => task.title);
  } catch (err) {
    console.log(err);
  }
});
</script>

<template>
  <h1 class="">{{ name }}</h1>
  <p v-if="status === 'active'">User is {{ status }}</p>
  <p v-else-if="status === 'pending'">User is {{ status }}</p>
  <p v-else>User is {{ status }}</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text id" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Add Task</button>
  </form>

  <h3>Tasks:</h3>
  <ul class="">
    <li v-for="(task, index) in tasks" :key="index">
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">X</button>
    </li>
  </ul>
  <br />
  <!-- <a v-bind:href="link">Click for Google</a>  v-bind directive -->

  <!-- //alternate way to do the same thing -->
  <a :href="link">Click for Google</a>

  <!-- <button v-on:click="toggleStatus">change status</button> handling event -->
  <button @click="toggleStatus">change status</button>
  <!-- alternate way to do the same thing -->
</template>
