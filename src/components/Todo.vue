<script setup>
import { ref } from "vue";

const Data = ref("");
const Todos = ref([]);

function Add() {
  Todos.value.push({
    title: Data.value,
    complete: false,
  });
  Data.value = "";
}

function Check(todoIndex) {
  Todos.value.map((todo, index) => {
    if (index === todoIndex) {
      todo.complete = !todo.complete;
    }
    return todo;
  });
}
function deleteData(todo) {
  Todos.value = Todos.value.filter((t) => t != todo);
}
</script>

<template>
  <div>
    <input v-model="Data" placeholder="Add task" />
    <button @click="Add">➕</button>
  </div>

  <ul>
    <li v-for="(todo, index) in Todos" :key="index">
      <span :class="{ completed: todo.complete }">
        {{ todo.title }}  <button @click="Check(index)">✅</button>
      
      </span>
     <button @click="deleteData(todo)">❌</button>
    </li>
  </ul>
</template>

<style>
* {
  list-style-type: none;
  }
  body{
    width: 100%;
    height: 100vh;
    margin: 0;
    padding: 15px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-image: 
    linear-gradient(
        45deg,
        rgb(226, 54, 105) 0%,
        rgb(120, 68, 179) 100%);
    font-family: 'DM Sans', sans-serif;
    overflow: hidden;
}

ul{
    list-style: none;
    padding: 0;
}

li {
  padding: 10px;
  margin-right: 14px;
}
span {
  padding: 10px;
  color: #fff;
}

.completed {
 opacity: 30%;
 font-weight: bold;
 text-decoration: line-through;
 color: rgb(219, 219, 219);
}

button{
    background: transparent;
    border: none;
}

</style>
