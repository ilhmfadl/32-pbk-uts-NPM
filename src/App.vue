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

</script>

<template>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
    </li>
  </ul>
</template>