<script setup>
import { ref, computed } from 'vue'

// unique id untuk tiap todo
let id = 0

const newTodo = ref('')
const filterStatus = ref('all')  

const todos = ref([
  { id: id++, text: 'Sholat subuh', done: false },
  { id: id++, text: 'Olahraga ringan', done: false },
  { id: id++, text: 'Sarapan', done: false },
  { id: id++, text: 'Berangkat Kuliah', done: false },
  { id: id++, text: 'Istirahat siang', done: false },
  { id: id++, text: 'Sholat Zuhur', done: false },
  { id: id++, text: 'Pulang & bersih-bersih', done: false },
  { id: id++, text: 'Sholat Ashar', done: false },
  { id: id++, text: 'Jogging', done: false },
  { id: id++, text: 'Mandi', done: false },
  { id: id++, text: 'Sholat Maghrib', done: false },
  { id: id++, text: 'Makan malam', done: false },
  { id: id++, text: 'Sholat isya', done: false }
])

const filteredTodos = computed(() => {
  if (filterStatus.value === 'incomplete') {
    return todos.value.filter((todo) => !todo.done)
  } else {
    return todos.value
  }
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}

function changeFilter(status) {
  filterStatus.value = status
}
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo" required placeholder="Tambah kegiatan...">
    <button>Tambah</button>
  </form>

  <div>
    <button @click="changeFilter('all')">Tampilkan Semua</button>
    <button @click="changeFilter('incomplete')">Tampilkan Belum Selesai</button>
  </div>

  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <label>
        <input type="checkbox" v-model="todo.done" />
        <span :class="{ done: todo.done }">{{ todo.text }}</span>
        <button @click="removeTodo(todo)">X</button>
      </label>
    </li>
  </ul>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
