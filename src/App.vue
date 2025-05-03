<script setup>
import { ref } from 'vue'

// unique id untuk tiap todo
let id = 0

const newTodo = ref('')
const todos = ref([
  { id: id++, text: 'Sholat subuh' },
  { id: id++, text: 'Olahraga ringan' },
  { id: id++, text: 'Sarapan' },
  { id: id++, text: 'Berangkat Kuliah' },
  { id: id++, text: 'Istirahat siang' },
  { id: id++, text: 'Sholat Zuhur' },
  { id: id++, text: 'Pulang & bersih-bersih' },
  { id: id++, text: 'Sholat Ashar' },
  { id: id++, text: 'Jogging' },
  { id: id++, text: 'Mandi' },
  { id: id++, text: 'Sholat Maghrib' },
  { id: id++, text: 'Makan malam' },
  { id: id++, text: 'Sholat isya' }
])

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo" required placeholder="Tambah kegiatan...">
    <button>Tambah</button>
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      <label>
        <input type="checkbox" v-model="todo.done" />
          {{ todo.text }}
        <button @click="removeTodo(todo)">X</button>
      </label>
    </li>
  </ul>
</template>