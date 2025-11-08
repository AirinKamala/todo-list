<script setup>
import { ref, onMounted, watch, computed } from 'vue';
const todos = ref([])
const nama = ref('')
const task = ref('')
const category_input = ref('')
const kondisi =('')


watch(nama, (newVal) => {
  localStorage.setItem('nama', newVal)
})

watch(todos, (newVal) => {
  localStorage.setItem('todos', JSON.stringify(newVal))
}, { deep: true })

function saveTodos() {
  localStorage.setItem('todos', JSON.stringify(todos.value))
}
onMounted(() => {

  nama.value = localStorage.getItem('nama') || ""
  const savedTodos = localStorage.getItem('todos')
  todos.value = savedTodos ? JSON.parse(savedTodos) : []
})

function addTodo() {
  if (task.value.trim() === '' || category_input.value.trim() === '') {
    return;
  }
  todos.value.push({
    'tugas': task.value,
    'kategori': category_input.value,
    'done' : false
  })
  saveTodos()
  task.value = ''
  category_input.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter(item => item !== todo)
  saveTodos()
}

</script>

<template>
  <div class="container">
    <h1>Welcome Back, </h1>
    <input type="text" name="nama" id="nama" v-model="nama" placeholder="Your Name">
  </div>
  <form class="card inputed">
    <h2>Simple To Do List</h2>
    <label for="task">Please type your task on the input field </label>
    <input type="text" name="task" id="task" placeholder="e.g. Edit this code" v-model="task">
    <div class="kategori">
      <div class="kategori_input"> <input type="radio" name="inputKategori" value="Bussiness" id="bisnis"
          v-model="category_input">
        <label for="bisnis">Bussiness</label>
      </div>
      <div class="kategori_input"> <input type="radio" name="inputKategori" value="Personal" id="pribadi"
          v-model="category_input">
        <label for="pribadi">Personal</label>
      </div>
    </div>
  </form>
  <button class="submit" type="button" @click="addTodo"> Add Task</button>

  <table class="card">
    <div class="tasked" v-for="(data, index) in todos" :key="index">
      <div class="td"> 
        <input type="checkbox" class="chek" :class="data.kategori==='Personal' ? 'Personal' : 'Bussiness'" v-model="data.done">
        <label for="dataTugas" :class="{ 'completed' : data.done }">{{data.tugas}}</label>
      </div>
      <button class="btn-del" @click="removeTodo(data)">Delete</button>
    </div>
  </table>

</template>

<style scoped></style>
 