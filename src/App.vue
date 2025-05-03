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
  { id: id++, text: 'Sholat isya', done: false },
  { id: id++, text: 'Belajar', done: false }
])

const filteredTodos = computed(() => {
  return filterStatus.value === 'incomplete'
    ? todos.value.filter(todo => !todo.done)
    : todos.value
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter(t => t !== todo)
}

function changeFilter(status) {
  filterStatus.value = status
}
</script>

<template>
  <div class="container">
    <h1>📝 Kegiatan Sehari hari</h1>

    <form @submit.prevent="addTodo" class="todo-form">
      <input v-model="newTodo" required placeholder="Tambah kegiatan..." />
      <button type="submit">Tambah</button>
    </form>

    <div class="filters">
      <button 
        @click="changeFilter('all')" 
        :class="{ active: filterStatus === 'all' }"
      >Tampilkan Semua</button>
      <button 
        @click="changeFilter('incomplete')" 
        :class="{ active: filterStatus === 'incomplete' }"
      >Belum Selesai</button>
    </div>

    <ul class="todo-list">
      <li v-for="todo in filteredTodos" :key="todo.id" :class="{ doneItem: todo.done }">
        <label>
          <input type="checkbox" v-model="todo.done" />
          <span :class="{ done: todo.done }">{{ todo.text }}</span>
          <button @click="removeTodo(todo)" class="remove-btn">✖</button>
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.container {
  max-width: 600px;
  margin-left: 600px ;
  margin-top: 40px;
  margin-bottom: 40px;
  padding: 60px;
  background-color: #fefefe;
  border-radius: 20px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.5);
  font-family: 'Segoe UI', sans-serif;
  background-image: url('./assets/gambar2.jpg');
}

h1 {
  text-align: center;
  margin-bottom: 20px;
  color: #2c3e50;
}

.todo-form {
  display: flex;
  gap: 10px;
  margin-bottom: 15px;
  
}

.todo-form input {
  flex: 1;
  padding: 10px;
  border-radius: 8px;
  border: 1px solid gray;
  font-size: 16px;
  background-color: white;
  color: black;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
  
}

.todo-form button {
  padding: 10px 16px;
  border: 1px solid gray;
  background-color: #3498db;
  color: white;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
}

.todo-form button:hover {
  background-color: #2980b9;
}

.filters {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 15px;
  
}

.filters button {
  padding: 6px 14px;
  border: 1px solid gray;
  border-radius: 6px;
  background-color: #ecf0f1;
  cursor: pointer;
  transition: all 0.3s;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
}

.filters button.active {
  background-color: #2ecc71;
  color: white;
}

.filters button:hover {
  background-color: #bdc3c7;
}

.todo-list {
  list-style: none;
  padding: 0;
  color: black;
}

.todo-list li {
  background-color: #f7f9fa;
  padding: 10px;
  margin-bottom: 8px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  transition: background-color 0.3s;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);

}

.todo-list li.doneItem {
  background-color: #e1f7e1;
}

.todo-list label {
  display: flex;
  align-items: center;
  gap: 10px;
  width: 100%;
}

.todo-list input[type="checkbox"] {
  transform: scale(1.2);
}

.todo-list .remove-btn {
  background: none;
  border: none;
  color: #e74c3c;
  font-size: 18px;
  cursor: pointer;
  margin-left: auto;
  transition: color 0.2s;
}

.todo-list .remove-btn:hover {
  color: #c0392b;
}

.done {
  text-decoration: line-through;
  color: #7f8c8d;
}

:global(body) {
  margin: 0;
  font-family: 'Segoe UI', sans-serif;
  background-image: url('./assets/gambar1.jpg');
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
}
</style>
